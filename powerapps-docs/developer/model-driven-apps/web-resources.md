---
title: Web リソース (モデル駆動型アプリ) | MicrosoftDocs
description: Web リソースは、アプリ用 CDS データベースに保存されている仮想ファイルで、一意の URL アドレスを使用して取得できます。
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
# <a name="web-resources-in-model-driven-apps"></a>モデル駆動型アプリの Web リソース

<!-- https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/web-resources -->


Web リソースはアプリ用 Common Data Service データベースに保存されている*仮想ファイル*で、一意の URL アドレスを使用して取得できます。  
  
<a name="BKMK_CapabilitiesOfWebResources"></a>   
## <a name="capabilities-of-web-resources"></a>Web リソースの機能  
 Web リソースとは、html ファイル、JavaScript および CSS などの アプリ用 CDS Web アプリケーションの拡張に使用できるファイル、またいくつかの画像の形式を意味します。 Web リソースは URL 構文を使用して参照できるので、フォームのカスタマイズ、`SiteMap`、またはアプリケーション リボンに使用できます。  
  
 Web リソースの URL 構文では、相対パス参照が許可されています。 開発ツールで、Web リソースと互換性のあるファイル タイプを使用することにより、開発サーバー上に相互依存ファイルのグループを作成できます。 一貫した命名規則と相対パス参照を使用する場合、すべてのファイルをアプリ用 CDS にアップロードした後で、Web サイトが機能します。
  
 Web リソースはアプリ用 CDS に保存されており、ソリューション コンポーネントなので、簡単にエクスポートして、他のアプリ用 CDS 組織にインストールできます。 Web リソースは、ユーザーのデータと同期している場合、オフライン アクセス対応 Microsoft Office Outlook のアプリ用 CDS のユーザーも使用できます。  
  
 フォーム エディターを使用して、フォーム対応の Web リソースをエンティティ フォームに追加し、構成できます。  
  
 Web リソースはレコードとしてデータベースに保存されているので、レコードを作成、取得、更新する標準的な手法を使用して、プログラムによって管理できます。 テキストベースの Web リソース (JScript、CSS、XML、RESX、HTML) は、アプリケーションで編集して保存できます。  
  
<a name="BKMK_LimitationsOfWebResources"></a>   
### <a name="limitations-of-web-resources"></a>Web リソースに関する制限事項  
 サーバー上でコードを実行するための ASP.NET (.aspx) ページの機能をサポートしている Web リソースの種類はありません。 Web リソースは、ブラウザーで処理される静的ファイルに限られています。 Web リソースには、Web サービス呼び出しを実行してアプリ用 CDS データを操作するためにブラウザーで処理されるコードを含めることができます。
  
 Web リソースは、アプリ用 CDS Web アプリケーションのセキュリティ コンテキストを使用してのみ、使用できます。 スクリプト Web リソースにアクセスできるのは、必要な特権を持つ、ライセンスを受けたアプリ用 CDS ユーザーだけです。  
  
#### <a name="size-limitations"></a>サイズ制限  
アップロードできる最大ファイル サイズは、Organization.MaxUploadFileSize プロパティによって決まります。 このプロパティは、Dynamics 365 アプリケーションのシステム設定の電子メールタブで設定します。 この設定で電子メール メッセージ、メモ、および Web リソースに添付できるファイルのサイズを制限します。 既定の設定は 5 MB です。
  
<a name="BKMK_WebResourceTypes"></a>   
## <a name="web-resource-types"></a>Web リソースの種類  
 web リソースの作成には 10 種類のファイル形式を使用できます。 次の表は、それぞれで使用する各ファイル形式、許可されているファイル拡張子、種類の値の一覧を示します。  
  
|ファイル|ファイル拡張子|種類|  
|----------|---------------------|----------|  
|Web ページ (HTML)|.htm、.html|1|  
|スタイル シート (CSS)|.css|2|  
|スクリプト (JScript)|.js|3|  
|データ (XML)|.xml|4|  
|イメージ (PNG)|.png|5|  
|イメージ (JPG)|.jpg|6|  
|イメージ (GIF)|.gif|7|  
|Silverlight (XAP)|.xap|8|  
|スタイルシート (XSL)|.xsl、.xslt|9|  
|イメージ (ICO)|.ico|10|  
|ベクター形式 (SVG)|.svg|11|  
|文字列 (RESX)|.resx|12|  
  
<a name="BKMK_ReferencingWebResources"></a>   
## <a name="reference-web-resources"></a>Web リソースの参照  
 Web リソースの参照に使用できる方法はいくつかあります。  
  
> [!NOTE]
>  -   可能な場合は、`$webresource` ディレクティブを使用してください。 依存関係が確立されるのは、サイト マップまたはリボン コマンドで `$webresource` ディレクティブを使用している参照のみです。 Web リソースが相互参照している場合、依存関係は作成されません。  
>       - Silverlight Web リソースをエンティティ フォームまたはグラフの外側に表示するには、その Silverlight Web リソースのホスト ページとなる HTML Web リソースを作成します。 その後、$webresource: ディレクティブを使用して HTML Web リソースを開きます。
  
<a name="BKMK_WebResourceDirective"></a>   
### <a name="webresource-directive"></a>$webresource ディレクティブ  
 リボン コントロール、または`SiteMap`のサブ領域から Web リソースを参照する場合は、常に `$webresource` ディレクティブを使用する必要があります。 XML が URL 値を許可している場合は常に `$webresource` ディレクティブを使用してください。 次のサンプルは、その使用方法を示しています。  
  
```xml  
$webresource:<name of Web Resource>  
```  
  
> [!NOTE]
>  `$webresource` ディレクティブを使用すると、アプリ用 CDS によってソリューションの依存関係が作成または更新されます。  
  
### <a name="xrmnavigationopenwebresource"></a>Xrm.Navigation.openWebResource  
 Xrm.Navigation.[openWebResource](clientapi/reference/Xrm-Navigation/openWebResource.md) 関数は、Web リソースの名前を渡すパラメーター、データ パラメーターで渡されるいずれかのクエリ文字列データ、およびウィンドウの高さや幅に関するおよび情報を含む、新しいウィンドウで HTML Web リソースをオープンします。  
  
 生成された URL には、キャッシュされた web リソースを読み込まれるように、一意の GUID にトークンが含まれます。  
  
<a name="BKMK_RelativeUrl"></a>   
### <a name="relative-url"></a>相対 URL  
 `$webresource:` ディレクティブの使用をサポートしていない領域から Web リソースを参照する場合は、相対 URL を使用できます。 相対 URL を使用できるようにするため、仮想ファイル構造を反映した Web リソースに一貫した命名規則を使用することをお勧めします。 ソリューション発行者のカスタマイズの接頭辞は、Web リソース名の接頭辞として常に含まれます。 これは、その発行者が追加するすべての Web リソースの仮想 "root" フォルダーを意味します。 スラッシュ (/) を使用して、Web サーバーが受け入れるフォルダー構造をシミュレートできます。  
  
 相互参照のため、常に別の Web リソースからの相対 URL を使用する必要があります。 たとえば、Web ページ Web リソース `new_/content/contentpage.htm` が CSS Web リソース `new_/Styles/styles.css` を参照するには、次のようにリンクを作成します。  
  
```html  
<link rel="stylesheet" type="text/css" href="../styles/styles.css" />  
```  
  
 Web ページ Web リソース `new_/content/contentpage.htm` が Web ページ Web リソース `isv_/foldername/dialogpage.htm` を開くには、次のようにリンクを作成します。  
  
```html  
<a href="../../isv_/foldername/dialogpage.htm">Dialog Page</a>  
```  
  
> [!NOTE]
>  WebResources フォルダーを URL のルート パスとして使用する相対 URL は使用しないでください。 たとえば、`/WebResources/<name of web resource>` は使用しないでください。 ユーザーがサーバー上の複数の組織に属している場合、このパスは常にユーザーの既定の組織を参照します。 ユーザーが既定の組織を使用しない場合、および想定される Web リソースがユーザーの既定の組織に含まれていない場合は、Web リソースがユーザーの現在作業している組織内にあっても、ファイルが見つからないエラーが発生します。  
  
<a name="BKMK_FullUrl"></a>   
### <a name="full-url"></a>完全 URL  
 次のサンプルでは、Web リソースの表示に使用できる URL の形式を示しています。  
  
```  
<CDS for Apps URL>/WebResources/<name of web resource>  
```  
  
 アプリケーションによりこの URL が処理され、Web リソースの最新版が含まれるファイルが返されます。 この URL は次のように表示されます。  
  
```  
<CDS for Apps URL>/%7B<version value>%7D/WebResources/<name of web resource>  
```  
  
 カスタマイズを公開するとバージョン値が更新され、ブラウザーで最新のキャッシュ済み Web リソースが確実に使用されます。 このため、Web リソースの相対パスか、Xrm.Navigation.[openWebResource](clientapi/reference/Xrm-Navigation/openWebResource.md) 関数、または可能であれば [$webresource ディレクティブ](web-resources.md#BKMK_WebResourceDirective) を使用します (バージョン値が自動的に含められるためです)。 大きな Web リソースの場合、ファイルのキャッシュされたバージョンを使用しないと、パフォーマンスにかなりの影響がある場合があります。  
  
 次のサンプルは、アプリ用 CDS の URL を示しており、ここで、`MyOrganization` は組織名で、`new_/test/test.htm` は web リソース名です。  
  
```  
https://MyOrganization.crm.dynamics.com/WebResources/new_/test/test.htm  
```  
  
> [!NOTE]
>  Web リソース名に '/' 文字とファイル名拡張子を含めることは、任意のベスト プラクティスです。  
  
  
 アプリ用 CDS に対して機能する必要がある Web リソースを参照するコードを記述する場合は、[getClientUrl](clientapi/reference/Xrm-Utility/getGlobalContext/getClientUrl.md) 関数を使用する必要があります。

## <a name="community-tools"></a>コミュニティ ツール

**WebResources マネージャー**は、アプリ用 CDS に XrmToolbox コミュニティが開発したツールです。 コミュニティ開発ツールのトピック、[開発者ツール](developer-tools.md) を参照してください。

> [!NOTE]
> コミュニティ ツールはアプリ用 CDS の製品ではなく、コミュニティ ツールに対するサポートは提供されません。 このツールに関するご質問は、その発行元にお問い合わせください。 詳細: [XrmToolBox](https://www.xrmtoolbox.com)。 
  
### <a name="see-also"></a>関連項目  

 [アクセス可能な Web リソースの作成](create-accessible-web-resources.md)<br />
 [Web ページ (HTML) の Web リソース](webpage-html-web-resources.md)<br />
 [スクリプト (JScript) Web リソース](script-jscript-web-resources.md)<br />
 [画像 Web リソース](image-web-resources.md)<br />
 [スタイルシート (XSL) Web リソース](stylesheet-xsl-web-resources.md)<br />
 [データ (XML) Web リソース](data-xml-web-resources.md)<br />
 [スタイル シート (CSS) Web リソース](css-web-resources.md)<br />
 [Web リソース エンティティの参照](../common-data-service/reference/entities/webresource.md)<br />
 [サンプル: データ パラメーターを使用した Web リソースへの複数の値の引き渡し](sample-pass-multiple-values-web-resource-through-data-parameter.md)<br />
 [サンプル: Web リソースとしてのファイルのインポート](sample-import-files-web-resources.md)<br />
 [Fiddler の AutoResponder を使用して Web リソース開発を合理化する](streamline-javascript-development-fiddler-autoresponder.md)
