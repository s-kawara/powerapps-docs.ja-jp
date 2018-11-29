---
title: イメージ Web リソース (モデル駆動型アプリ) | MicrosoftDocs
description: 'カスケード スタイル シート (CSS) web リソースを使用して、webページ web リソースで使用するスタイル シートを作成します。 '
keywords: ''
ms.date: 10/31/2018
ms.service:
  - powerapps
ms.custom:
  - ''
ms.topic: article
ms.assetid: a4e98fa7-930d-e320-5384-9f773775639b
author: JimDaly
ms.author: jdaly
manager: shilpas
ms.reviewer: null
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---

# <a name="css-web-resources"></a>CSS Web リソース

<!-- https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/css-web-resources -->

カスケード スタイル シート (CSS) web リソースを使用して、webページ web リソースで使用するスタイル シートを作成します。  
  
## <a name="capabilities-of-css-web-resources"></a>CSS web リソースの機能  
 CSS web リソースを使用すると、webページ Web リソースを CSS スタイルの共有ライブラリにリンクして、その外観を管理できます。  
  
### <a name="limitations-of-css-web-resources"></a>CSS web リソースの制限  
 すべての web リソースと同様、CSS web リソースもセキュリティ コンテキストでのみ使用できます。 スクリプト Web リソースにアクセスできるのは、必要な特権を持つ、ライセンスを受けたユーザーだけです。
  
## <a name="referencing-a-style-sheet-web-resource-from-a-webpage-web-resource"></a>webページ web リソースからのスタイル シート web リソースの参照  
 すべての Web リソースは相対 URL を使用して相互に参照できます。 次の例で、webページ web リソース `sample_/content/contentpage.htm` からスタイル シート web リソース `sample_/styles/styles.css` を参照するには、次の例を sample_/content/contentpage.htm の head 要素に追加します。  
  
```html  
<link rel="stylesheet" type="text/css" href="../styles/styles.css" />  
```  
  
 別の発行者からのスタイル シートを参照するには、パスにソリューション発行者のカスタマイズ接頭辞を含める必要があります。 たとえば、`sample_/content/contentpage.htm` ページから `MyIsv_/styles/styles.css` ページを参照するには、href パラメーター値を `../../MyIsv_/styles/styles.css` にする必要があります。  
  
> [!NOTE]
>  web リソース間のコードに含まれる参照は、ソリューションの依存関係として追跡されません。  
  
### <a name="see-also"></a>関連項目  
 [Web リソース](web-resources.md)   
 [Web ページ (HTML) の Web リソースの使用](webpage-html-web-resources.md)   
 [スクリプト (JScript) Web リソースの使用](script-jscript-web-resources.md)   
 [データ (XML) Web リソースの使用](data-xml-web-resources.md)   
 [画像 (JPG、PNG、GIF) Web リソースの使用](image-web-resources.md)   
 [Silverlight (XAP) Web リソースの使用](/dynamics365/customer-engagement/developer/silverlight-xap-web-resources)  
 [スタイルシート (XSL) Web リソースの使用](stylesheet-xsl-web-resources.md)   
 [WebResource エンティティ](../common-data-service/reference/entities/webresource.md)
