---
title: フォーム上で IFRAME および Web リソース コントロールを使用する (モデル駆動型アプリ) | Microsoft Docs
description: 'IFRAME および Web リソース コントロールでは、HTML IFRAME 要素を使用して、ページ内に別の場所からコンテンツを埋め込みます。  '
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
# <a name="use-iframe-and-web-resource-controls-on-a-form"></a>フォーム上で IFRAME および Web リソース コントロールを使用する

<!-- https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/use-iframe-and-web-resource-controls-on-a-form -->


IFRAME および Web リソース コントロールでは、HTML IFRAME 要素を使用して、ページ内に別の場所からコンテンツを埋め込みます。  

> [!NOTE]
>  フォーム用に選択したデザインは Dynamics 365 for Outlook の閲覧ウィンドウや Dynamics 365 for tablets のフォームにも使用されます。 Web リソースおよび IFRAME の閲覧ウィンドウは Dynamics 365 for Outlook の閲覧ウィンドウを使用して表示されません。しかし Dynamics 365 for tablets ではサポートされています。 IFRAME がページの `Xrm` オブジェクトやフォーム イベント ハンドラーへのアクセスに依存する場合は、IFRAME を既定で表示しないように構成してください。  

 ASP.NET ページのように、別の Web サイトのコンテンツをフォームに表示するには IFRAME を使用します。 別のエンティティ フォームに埋め込まれた IFrame 内のエンティティ フォームの表示はサポートされていません。  

 Web リソースのコンテンツをフォームに表示するには、次のいずれかの Web リソースを使用できます。  

-   [Web ページ (HTML) の Web リソース](webpage-html-web-resources.md)  

-   [画像 (JPG、PNG、GIF、ICO) の Web リソース](image-web-resources.md)  


 以降のセクションでは、これらのコントロールで静的コンテンツ以外も表示させるために使用するオプションについて説明します。  

<a name="BKMK_IframeSecurity"></a>   
## <a name="select-whether-to-restrict-cross-frame-scripting"></a>クロスフレーム スクリプトを制限するかどうかを選択する  
 IFRAME で表示されるコンテンツを完全には信頼しない場合は、**サポートされている場合はクロスフレーム スクリプトを制限します**オプションを使用します。 このオプションを選択すると、次の表に示す属性が IFRAME で設定されます。  


|        属性        |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        説明                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|-------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `security="restricted"` |                                                                                                                                                                                                                                                                                                    この属性はバージョン 6 以降の Internet Explorer でのみサポートされます。 この security 属性により、ユーザーの [制限付きサイト] のセキュリティ設定が IFRAME のソース ファイルに適用されます  (ゾーンの設定は**インターネット オプション**ダイアログ ボックスの**セキュリティ**タブにあります)。規定では、制限付きサイト ゾーンでは、スクリプトは無効になっています。 ゾーンのセキュリティ設定を変更すると、スクリプトの実行が許可されるなど、さまざまな悪い結果を招くことがあります。 詳細については、「[security 属性](https://msdn.microsoft.com/library/ie/ms534622.aspx)」を参照してください。                                                                                                                                                                                                                                                                                                     |
|      `sandbox=""`       | この属性をサポートするブラウザーで、IFRAME のコンテンツが基本的に情報の表示だけに制限されます。 次の制限が適用されます。<br /><br /> -   ブラウザーのプラグインが無効になります。<br />-   フォームとスクリプトが無効になります。<br />-   他の参照コンテキストへのリンクが無効になります。<br />-   同じドメインのコンテンツの場合でも別のドメインのコンテンツとして扱われます。<br /><br /> これは W3C が定義した属性で、次のブラウザーでサポートされます。<br /><br /> - Internet Explorer 10、Internet Explorer 11 および Microsoft Edge <br />- Google Chrome<br />- Apple Safari<br />- Mozilla Firefox<br /><br /> 属性の詳細については、以下を参照してください。<br /><br /> -   [How to Safeguard your Site with HTML5 Sandbox (HTML5 Sandbox を使用してサイトを保護する方法)](https://msdn.microsoft.com/hh563496)<br />-   [WC3 Sandbox 属性](http://dev.w3.org/html5/spec-author-view/the-iframe-element.html)<br />-   [サンドボックス](https://msdn.microsoft.com/library/ie/hh673561.aspx) |

<a name="BKMK_EnableIFrameCommunicationAcrossDomains"></a>   

### <a name="enabling-iframe-communication-across-domains"></a>ドメイン間での IFRAME 通信の有効化  
 異なるドメインにコンテンツを含む IFRAME の通信を有効化する場合があります。 `Window.postMessage` は Internet Explorer 8 以降のバージョンでこの機能を提供するブラウザー メソッドです。 Google Chrome、Mozilla Firefox および Apple Safari でもサポートされます。 `postMessage` の使用方法の詳細については、次のブログ記事を参照してください。  

-   [親フォームに対するクロス ドメイン呼び出し](http://blogs.msdn.com/b/devkeydet/archive/2012/02/14/cross-domain-calls-to-the-parent-crm-2011-form.aspx)  

-   [Cross-Document Messaging and RPC (クロス ドキュメント メッセージングと RPC)](https://msdn.microsoft.com/magazine/ff800814.aspx)  

<a name="BKMK_PassContextualInformation"></a>   

## <a name="pass-contextual-information-about-the-record"></a>レコードに関するコンテキスト情報を渡す  
 コントロール内で定義される URL にパラメーターを渡すことで、コンテキスト情報を提供できます。 フレームに表示されるページは、渡されるパラメーターを処理できる必要があります。 IFRAME または Web リソースが、**パラメーターとして、レコードのオブジェクトの種類コードおよび一意の識別子を渡します。** オプションを使用して構成されている場合は、次の表のすべてのパラメーターが渡されます。  

 次の表のすべてのパラメーターが渡されるかどうかを指定できます。  


| パラメーター  |        名前        |                                 説明                                 |
|------------|--------------------|-----------------------------------------------------------------------------|
| `typename` |    エンティティ名     |                           エンティティの名前。                           |
|   `type`   |  エンティティの種類コード  | 特定の組織内のエンティティを一意に識別する整数です。 |
|    `id`    |    オブジェクトの GUID     |                      レコードを表す GUID です。                       |
| `orgname`  | 組織名  |                    組織の一意の名前です。                     |
| `userlcid` | ユーザー言語コード |    現在のユーザーが使用している言語コードの識別子です。     |

 [!INCLUDE[languagecode](../../includes/languagecode.md)]  

> [!NOTE]
>  ユーザー定義エンティティの種類コードはアプリ用 CDS の組織ごとに異なる可能性があるため、種類コードではなくエンティティ名を使用することをお勧めします。  

### <a name="example"></a>例  
 次のサンプルは、パラメーターのない URL の表示方法を示しています。  

```  
http://myserver/mypage.aspx  
```  

 次のサンプルは、パラメーターのない URL の表示方法を示しています。  

```  
http://myserver/mypage.aspx?id=%7bB2232821-A775-DF11-8DD1-00155DBA3809%7d&orglcid=1033&orgname=adventureworkscycle&type=1&typename=account&userlcid=1033  
```  

### <a name="read-passed-parameters"></a>渡されたパラメーターを読み取る  

 通常、渡されたパラメーターは、ターゲットの .aspx ページで **HttpRequest.QueryString** プロパティを使用して読み取られます。 HTML ページでは JavaScript の **window.location.search** プロパティを使用してパラメータにアクセスできます。 詳細については、「[HttpRequest.QueryString プロパティ](http://msdn2.microsoft.com/library/system.web.httprequest.querystring.aspx)」および「[検索文字](http://msdn2.microsoft.com/library/ms534620.aspx)」を参照してください。  

<a name="BKMK_PassFormData"></a>  

## <a name="pass-form-data"></a>フォーム データを渡す  

 他の Web サイトに渡すデータが格納されている属性で [getValue](clientapi/reference/controls/getValue.md) メソッドを使用し、他のページが使用できるクエリ文字列引数の文字列を構成します。 次に、[Field OnChange Event](clientapi/reference/events/attribute-onchange.md), [IFRAME OnReadyStateComplete Event](clientapi/reference/events/onreadystatecomplete.md)、または [Tab TabStateChange Event](clientapi/reference/events/tabstatechange.md) 、および [setSrc](clientapi/reference/controls/setSrc.md) メソッドを使用して、IFRAME または Web リソースの `src` プロパティにパラメーターを追加します。  

 Silverlight Web リソースにデータを渡すためにデータ パラメーターを使用している場合は、 [getData](clientapi/reference/controls/getData.md) および [setData](clientapi/reference/controls/setData.md) メソッドを使用してデータ パラメーターを通じて渡される値を操作できます。 Web ページ (HTML) の Web リソースの場合は、[setSrc](clientapi/reference/controls/setSrc.md) メソッドを使用して `querystring` パラメーターを直接操作します。  

 [OnLoad Event](clientapi/reference/events/form-onload.md) は使用しないでください。 IFRAME と Web リソースは非同期に読み込みを行うため、`Onload` イベント スクリプトが終了する前に、フレームの読み込みが終了しないことがあります。 この場合、変更した IFRAME または Web リソースの `src` プロパティが、IFRAME または Web リソースの URL プロパティの既定値で上書きされる可能性があります。  

<a name="BKMK_ChangeThePage"></a>   

## <a name="change-the-url"></a>URL を変更する  

 フォーム内のデータや、ユーザーがオフラインかどうかなどの考慮事項に応じて、IFRAME のターゲットを変更すると有効な場合があります。 IFRAME のターゲットは動的に設定できます。  

> [!NOTE]
>  IFRAME のターゲット ページを変更しても、パラメーターは新しい URL に自動的には渡されません。 `setSrc` メソッドを使用する前に、クエリ文字列のパラメーターを URL に追加する必要があります。  

### <a name="example"></a>例  

 次のサンプルで、オプション セット フィールドの `onChange` イベントを使用して、IFRAME の `src` プロパティおよび任意のパラメーターを設定する方法を示します。  

```javascript  
//Get the value of an option set attribute  
var value = Xrm.Page.data.entity.attributes.get("new_pagechooser").getValue();  
var newTarget = "";  
//Set the target based on the value of the option set  
switch (value) {  
    case 100000001:  
        newTarget = "http://myServer/test/pageOne.aspx";  
        break;  
    default:  
        newTarget = "http://myServer/test/pageTwo.aspx";  
        break;  
}  
//Get the default URL for the IFRAME, which includes the   
// query string parameters  
var IFrame = Xrm.Page.ui.controls.get("IFRAME_test");  
var Url = IFrame.getSrc();  
// Capture the parameters  
var params = Url.substr(Url.indexOf("?"));  
//Append the parameters to the new page URL  
newTarget = newTarget + params;  
// Use the setSrc method so that the IFRAME uses the  
// new page with the existing parameters  
IFrame.setSrc(newTarget);  
```  

## <a name="see-also"></a>関連項目  

 [JavaScript を使用したクライアント スクリプト](client-scripting.md)   
 

