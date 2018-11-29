---
title: イメージ Web リソース (モデル駆動型アプリ) | MicrosoftDocs
description: イメージ Web リソースを使用して、イメージを利用可能にする方法について説明します。
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: KumarVivek
ms.author: kvivek
manager: shilpas
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="image-web-resources"></a>イメージ Web リソース

<!-- https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/image-web-resources -->

イメージ Web リソースを使用して、モデル駆動型アプリでイメージを利用可能にします。  

イメージ Web リソースには 5 つの種類があります。 
* PNG 形式
* JPG 形式
* GIF 形式
* ICO 形式
* ベクター形式 (SVG)

> [!NOTE]
> ベクター形式 (SVG) Web リソースは、モデル駆動型アプリにより追加されました。

  
<a name="BKMK_Capabilities"></a>   
## <a name="capabilities-of-image-web-resources"></a>イメージ Web リソースの機能  
 イメージ Web リソースを使用すると、必要な場所にイメージを追加できます。 一般には、以下のもので使用されます。  
  
- ユーザー定義エンティティのアイコン  
- ユーザー定義のリボン コントロールおよび`SiteMap`のサブ領域用のアイコン  
- エンティティ フォーム用および Web ページの Web リソース用の装飾的なグラフィック  
- CSS Web リソースが使用するバックグラウンド イメージ。  

アプリケーションに表示されるすべてのアイコンにベクター形式 (SVG) Web リソースを使用します。 ベクター イメージは、スケーラブル ベクター グラフィックス (SVG) (XML ベースのベクター イメージ形式) として定義されます。 他のイメージ Web リソースに対するベクター イメージの利点は、拡大縮小できることです。 サイズ別に複数のイメージを用意するのではなく、1 つのベクター イメージを定義して再利用できます。 これらを新しい <xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata>.<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata.IconVectorName> で使用します `IconLargeName`、`IconMediumName`、または `IconSmallName` プロパティではなく、ユーザー定義エンティティのアイコンを定義するプロパティ。
  
<a name="BKMK_Limitations"></a>   
## <a name="limitations-of-image-web-resources"></a>イメージ Web リソースの制限  
 他のすべての Web リソースと同様、イメージ Web リソースはセキュリティ コンテキストを使用します。 スクリプト Web リソースにアクセスできるのは、必要な特権を持つ、ライセンスを受けたユーザーだけです。  
 
  
<a name="BKMK_ReferenceFromWebPageWebResource"></a>   
## <a name="reference-an-image-web-resource-from-a-webpage-web-resource"></a>Web ページの Web リソースからイメージ Web リソースを参照する  
 すべての Web リソースは相対 URL を使用して相互に参照できます。 以下の例では、Web ページ (HTML) の Web リソース new_/content/contentpage.htm からイメージ Web リソース new_/Images/image1.png を参照し、次の HTML コードを new_/content/contentpage.htm に追加します。  
  
```html  
<img src="../Images/image1.png" />  
```  
  
<a name="BKMK_ReferenceFromForm"></a>   
## <a name="reference-an-image-web-resource-from-a--form"></a> フォームからのイメージ Web リソースの参照  
  
#### <a name="add-an-image-to-an-entity-form"></a>イメージをエンティティ フォームに追加する  
  
1.  エンティティのフォーム エディターに移動します。  
  
2.  フォーム内の、イメージを追加する場所をクリックします。  
  
3.  **挿入**タブで、**Web リソース**をクリックします。  
  
4.  **全般**タブで、追加する Web リソース イメージを選択します。  
  
5.  Web リソースの名前を指定します。 ラベルや代替テキストも指定できます。  
  
6.  **形式**タブで、次の項目を定義できます。  
  
    -   イメージが使用する列の数。  
  
    -   イメージが使用する行の数、または自動的に展開して使用可能な領域を使用するかどうか。  
  
    -   以下のオプションを使用するイメージのサイズ  
  
        - **使用可能な領域の使用 (サイズに合わせて伸縮)**  
  
        - **使用可能な領域の使用 (縦横比を固定)**  
  
        - **元の画像サイズ**  
  
        - **Specific**  
  
    -   [特定のサイズ] を選択した場合、高さと幅をピクセル単位で入力できます。  
  
7.  **OK** をクリックします。  
  
8.  フォーム内のイメージをユーザーが表示できるようにするには、変更を保存してフォームを公開する必要があります。  
  
<a name="BKMK_ReferenceWithWebResourcedirective"></a>   
## <a name="reference-an-image-web-resource-from-a-ribbon-element-or-from-the-site-map-subarea"></a>リボン要素またはサイト マップのサブ領域からイメージ Web リソースを参照する  
 Web リソース イメージを、リボンのアイコンとして、またはサイト マップを使用したアプリケーション ナビゲーションのアイコンとして使用するように指定するには、`$webresource:` ディレクティブを使用します。 次のサンプルに、リボンのボタンのアイコンを指定する方法を示します。  
  
```xml  
<Button Id="MyISV.opportunity.form.actions.FlyoutAnchor.Button.1" Image16by16="$webresource:new_/icons/oneIcon16.png" Image32by32="$webresource:new_/icons/oneIcon32.png"/>  
```  
  
> [!NOTE]
>  `$webresource:` ディレクティブを使用してソリューションの依存関係を追加し、参照されているイメージ Web リソースが、他のソリューション コンポーネントで使用されている間は削除されないようにします。  
  
### <a name="see-also"></a>関連項目  
 [Web リソース](web-resources.md)   
 [Web ページ (HTML) の Web リソースの使用](webpage-html-web-resources.md)   
 [スタイル シート (CSS) Web リソースの使用](css-web-resources.md)   
 [スクリプト (JScript) Web リソースの使用](script-jscript-web-resources.md)   
 [データ (XML) Web リソースの使用](data-xml-web-resources.md)   
 [Silverlight (XAP) Web リソースの使用](/dynamics365/customer-engagement/developer/silverlight-xap-web-resources)  
 [スタイル シート (XSL) Web リソースの使用](stylesheet-xsl-web-resources.md)
