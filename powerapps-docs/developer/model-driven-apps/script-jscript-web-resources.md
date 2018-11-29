---
title: スクリプト (JScript) Web リソース | MicrosoftDocs
description: どこからでもアクセスできる JavaScript 関数のライブラリを作成するために使用する JavaScript Web リソースについて説明します。
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
# <a name="script-jscript-web-resources"></a>スクリプト (JScript) Web リソース

<!-- https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/script-jscript-web-resources -->

どこからでもアクセスできる JavaScript 関数のライブラリを作成するには、スクリプト (JScript) Web リソースを使用します。  
  
<a name="BKMK_capabilties"></a>   
## <a name="capabilities-of-script-web-resources"></a>スクリプト Web リソースの機能  
 JavaScript Web リソースを使用すると、フォーム スクリプト、Web ページ (HTML) Web リソース、またはリボン コマンドで使用するコードを JavaScript 関数の共有ライブラリにリンクすることにより、より効率的に管理できます。  
  
<a name="BKMK_limitations"></a>   
## <a name="limitations-of-script-web-resources"></a>スクリプト web リソースの制限事項  
 すべての Web リソースと同様に、JavaScript Web リソースはモデル駆動型アプリのセキュリティ コンテキストを使用します。 スクリプト Web リソースにアクセスできるのは、必要な特権を持つ、ライセンスを受けたユーザーだけです。  
  
> [!NOTE]
>  web リソース間のコードに含まれる参照は、ソリューションの依存関係として追跡されません。  
  
<a name="BKMK_Using"></a>   
## <a name="using-javascript-libraries"></a>JavaScript ライブラリの使用  
 JavaScript ライブラリの開発とテスト、およびリボン コマンドとフォーム イベントへの関連付け方法については、「[JavaScript を使用したクライアント スクリプト](client-scripting.md)」を参照してください。  
  
<a name="BKMK_Referencing"></a>   
## <a name="referencing-a-script-web-resource-from-a-webpage-web-resource"></a>web ページ web リソースからのスクリプト web リソースの参照  
 すべての Web リソースは相対 URL を使用して相互に参照できます。 以下の例では、Web ページ Web リソース `new_/content/contentpage.htm` が JavaScript Web リソース `new_/scripts/myScript.js` を参照するため、以下の HTML コードを `new_/content/contentpage.htm` の head 要素に追加します。  
  
```html  
<script type="text/jscript" src="../scripts/myScript.js"></script>  
```  
  
 異なる発行者から JavaScript を参照するには、パスにその発行者のカスタマイズの接頭辞を含める必要があります。 たとえば、`new_/content/contentpage.htm` ページが `MyIsv_/scripts/customscripts.js` ページを参照するには、`src` 属性値を `../../MyIsv_/scripts/customscripts.js` にする必要があります。  
  
### <a name="see-also"></a>関連項目  
 [JavaScript を使用したクライアント スクリプト](client-scripting.md)   
 [Web リソース](web-resources.md)   
 [Web ページ (HTML) の Web リソースの使用](webpage-html-web-resources.md)   
 [スタイル シート (CSS) Web リソースの使用](css-web-resources.md)   
 [データ (XML) Web リソースの使用](data-xml-web-resources.md)   
 [画像 (JPG、PNG、GIF、ICO) Web リソースの使用](image-web-resources.md)   
 [スタイルシート (XSL) Web リソースの使用](stylesheet-xsl-web-resources.md)   
 [Fiddler の AutoResponder を使用して Web リソース開発を合理化する](streamline-javascript-development-fiddler-autoresponder.md)    
