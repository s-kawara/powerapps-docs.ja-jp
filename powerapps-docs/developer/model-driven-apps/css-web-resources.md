---
title: CSS ウェブ リソース (モデル駆動型 アプリケーション) | Microsoft Docs
description: 'カスケーディング スタイル シート (CSS) のウェブリソースを使用して、ウェブページのウェブリソースにて使用するスタイル シートを作成します。 '
keywords: ''
ms.date: 10/31/2018
ms.service: powerapps
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

<!-- https://docs.microsoft.com/dynamics365/customer-engagement/developer/css-web-resources -->

カスケーディング スタイル シート (CSS) のウェブリソースを使用して、ウェブページのウェブリソースにて使用するスタイル シートを作成します。  
  
## <a name="capabilities-of-css-web-resources"></a>CSS ウェブ リソースの機能  
 CSS ウェブリソースでは、 CSS 形式の共有ライブラリにリンクすることで、webpage ウェブリソースの外観を管理することができます。  
  
### <a name="limitations-of-css-web-resources"></a>CSS ウェブ リソースの制限事項  
 一般的なウェブ リソースと同様に、 CSS のウェブ リソースはセキュリティのコンテキストにおいてのみ使用が可能です。 スクリプト Web リソースにアクセスできるのは、必要な特権を持つ、ライセンスを受けたユーザーだけです。
  
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
