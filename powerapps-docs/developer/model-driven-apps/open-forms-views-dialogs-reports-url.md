---
title: URL を使用してフォーム、ビュー、ダイアログ、およびレポートを開く (モデル駆動型アプリ) | MicrosoftDocs
description: 他のアプリケーションにフォーム、ビュー、ダイアログ、およびリポートへのリンクを含めることができる URL アドレス指定が可能な要素の詳細を説明します。
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
# <a name="open-forms-views-dialogs-and-reports-with-a-url"></a>URL を使用してフォーム、ビュー、ダイアログ、およびレポートを開く

<!-- https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/open-forms-views-dialogs-reports-url -->

URL アドレス指定が可能な要素を使用すると、他のアプリケーションにフォーム、ビュー、ダイアログ、およびリポートへのリンクを含めることができます。 これにより、他のアプリケーション、レポート、または Web サイトを容易に拡張できるため、ユーザーはアプリケーションを切り替えなくても情報を表示したりアクションを実行したりできるようになります。  

> [!NOTE]
> - URL アドレス指定が可能なフォーム、ビュー、ダイアログ、およびレポートは、 セキュリティを回避することはできません。 セキュリティ ロールに基づいて、ライセンスを受けた ユーザーだけが、表示されるデータとレコードにアクセスできます。  
>   -   アプリケーション内で Web リソースを使用して、エンティティ フォームをプログラムで開くときは、`Xrm.Navigation.`[openForm](clientapi/reference/Xrm-Navigation/openForm.md) を使用します。 `window.open` は使用しないでください。  
>   -   ページが `Xrm.Navigation.`[openForm](clientapi/reference/Xrm-Navigation/openForm.md) 関数にアクセスできないそれ以外のアプリケーションでは、`window.open` またはリンクを使用してエンティティの特定のレコードまたはフォームを開きます。  

<a name="BKMK_URLAddressableFormsAndViews"></a>

## <a name="url-addressable-forms-and-views"></a>URL アドレス指定が可能なフォームとビュー

 すべてのエンティティ フォームとビューが main.aspx ページに表示されます。 このページに渡されたクエリ文字列パラメーターによって、表示される内容が制御されます。 たとえば、次のようになります。  

<!-- To open a new account entity record form for on-premises [!INCLUDE[pn_microsoftcrm](../includes/pn-microsoftcrm.md)]:  
 ```  
http://mycrm/myOrg/main.aspx?etn=account&pagetype=entityrecord  
 ```  -->

 id が {91330924-802A-4B0D-A900-34FD9D790829} の取引先企業エンティティ レコード フォームを開く場合:  
 ```  
http://myorg.crm.dynamics.com/main.aspx?etn=account&pagetype=entityrecord&id=%7B91330924-802A-4B0D-A900-34FD9D790829%7D  
 ```  

 **クローズされた営業案件** ビューを開く場合:  
 ```  
http://myorg.crm.dynamics.com/main.aspx?etn=opportunity&pagetype=entitylist&viewid=%7b00000000-0000-0000-00AA-000010003006%7d&viewtype=1039  
 ```  

 ナビゲーション バーやコマンド バーなしで、 **アクティブな連絡先** ビューを開くには  
 ```  
http://myorg.crm.dynamics.com/main.aspx?etn=contact&pagetype=entitylist&viewid={00000000-0000-0000-00AA-000010001004}&viewtype=1039&navbar=off&cmdbar=false  
 ```  

> [!NOTE]
>  [showModalDialog](https://msdn.microsoft.com/library/ie/ms536759.aspx) または [showModelessDialog](https://msdn.microsoft.com/library/ie/ms536761.aspx) を使用してダイアログ ウィンドウでエンティティ フォームを開くことはできません。  
>   
>  別のエンティティ フォームに埋め込まれた IFrame 内のエンティティ フォームの表示はサポートされていません。  

 通常は、[getClientUrl](clientapi/reference/Xrm-Utility/getGlobalContext/getClientUrl.md) メソッドを使用して、モデル駆動型アプリ用の組織のルート URL を取得します。  

<a name="BKMK_QueryStringParametersForMainForm"></a>   
### <a name="query-string-parameters-for-the-mainaspx-page"></a>Main.aspx ページのクエリ文字列パラメーター  

> [!TIP]
>  レコードの ID 値を取得するには、コマンド バーの**リンクの送信**ボタンを使用します。 電子メール アプリケーションで開かれる例を次に示します。  
>   
>  `<http://mycrm/myOrg/main.aspx?etc=4&id=%7b899D4FCF-F4D3-E011-9D26-00155DBA3819%7d&pagetype=entityrecord>`。  
>   
>  URL に渡される id パラメーターは、レコードのエンコードされた id 値です。 この例では、id 値は `{899D4FCF-F4D3-E011-9D26-00155DBA3819}` です。 GUID のエンコードされたバージョンは、開く中カッコ "{" と閉じる中カッコ "}" をそれぞれ "%7B" と "%7D" で置換します。  

 次に、エンティティ フォームやビューを開くために main.aspx ページで使用されるクエリ文字列パラメーターを示します。  


|  パラメーター   |                                                                                                                                                                                                                                                                                                                                            内容                                                                                                                                                                                                                                                                                                                                            |
|--------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   **etn**    |                                                                                                                                                                                                                                    エンティティの論理名。 **重要:** エンティティに整数コードを含む **etc** (エンティティの種類コード) パラメーターは使用しないでください。 この整数コードは、異なる組織のユーザー定義エンティティでは異なります。                                                                                                                                                                                                                                     |
| **extraqs**  |     フォームではオプションです。 このパラメーターには、このパラメータ内のエンコードされたパラメーターが含まれます。<br /><br /> このパラメーターを使用してフォームに値を渡します。 詳細については、「[フォームに渡すパラメーターを使用してフィールド値を設定する](set-field-values-using-parameters-passed-form.md)」を参照してください。<br /><br /> エンティティに複数のフォームが定義されている場合は、このパラメーターを使用して、フォームの ID 値と等しい値を持つエンコードされたパラメーター `formid` を渡すことで、開くフォームを指定できます。 たとえば、"6009c1fe-ae99-4a41-a59f-a6f1cf8b9daf" という ID のフォームを開くには、`extraqs` パラメーターに `formid%3D6009c1fe-ae99-4a41-a59f-a6f1cf8b9daf%0D%0A` という値を含めます。     |
| **pagetype** |                                                                                                                                                                                                                                                        ページの種類です。 指定できる値は 2 つあります。<br /><br /> - **entityrecord**<br />     エンティティ レコード フォームを表示します。<br />- **entitylist**<br />     エンティティ ビューを表示します。                                                                                                                                                                                                                                                         |
|    **id**    |                                                                                                                                                                      フォームではオプションです。 特定のエンティティ レコードを開く場合に使用します。 エンティティのエンコードされた GUID 識別子を渡します。 GUID のエンコードされたバージョンは、開く中カッコ "{" と閉じる中カッコ "}" をそれぞれ "%7B" と "%7D" で置換します。たとえば、`{91330924-802A-4B0D-A900-34FD9D790829}` は `%7B91330924-802A-4B0D-A900-34FD9D790829%7D` です。                                                                                                                                                                      |
|  **viewid**  |                                                                                                                                                                                                        ビューでは必須です。 これは、ビューを定義する `savedquery` または `userquery` エンティティ レコードの ID です。 ビューの URL を取得する最も簡単な方法は、その URL をコピーすることです。 詳細については、「[ビューの URL のコピー](open-forms-views-dialogs-reports-url.md#BKMK_CopyViewURL)」を参照してください。                                                                                                                                                                                                         |
| **viewtype** |                                                                                                                                                                                                        ビューの種類を定義します。 使用できる値は次のとおりです。<br /><br /> - **1039**<br />     システム ビューに使用します。 `viewid` は `savedquery` レコードの ID を表します。<br />- **4230**<br />     個人用ビューに使用します。 `viewid` は `userquery` レコードの ID を表します。                                                                                                                                                                                                         |
|   `navbar`   | サイト マップで定義されているエリアとサブエリアを使用して、ナビゲーション バーを表示するかどうか、およびアプリケーションのナビゲーションを使用可能にするかどうかを制御します。<br /><br /> -   `on`<br />     ナビゲーション バーが表示されます。 `navbar`パラメーターが使用されていない場合の既定の動作です。<br />-   `off`<br />     ナビゲーション バーが表示されません。 他のユーザー インターフェイス要素、または戻るボタンと進むボタンを使用して移動できます。<br />-   `entity`<br />     エンティティ フォームでは、関連するエンティティのナビゲーション オプションのみが利用可能です。 関連エンティティへの移動の後は、ナビゲーション バーに [戻る] ボタンが表示され、元のレコードに戻ることができます。 |
|   `cmdbar`   |                                                                                                                コマンド バーを表示するかどうかを制御します。 **注:** この機能は Unified Service Desk アプリケーションの要件をサポートしています。 これを使用して別のエンティティ フォームに埋め込まれた IFrame 内のエンティティ フォームを表示することは、サポートされていません。 <br /><br /> -   `true`<br />     コマンド バーが表示されます。 これが既定です。<br />-   `false`<br />     コマンド バーが非表示になります。                                                                                                                |

<a name="BKMK_CopyViewURL"></a>   
### <a name="copy-the-url-for-a-view"></a>ビューの URL のコピー  
 モデル駆動型アプリの多くのビューには、特定のビューの URL をコピーしたり、電子メールのメッセージに特定のビューの URL を埋め込んで送信したりできる機能が備えられています。 この機能により、ユーザー間のやり取りが容易になり、ユーザーが別のアプリケーション (SharePoint サイトなど) に含めることのできるビューの URL にもアクセスできるようになります。  

> [!NOTE]
>  この URL は、サイト マップを使用してアプリケーション ナビゲーションにビューを含めるときは使用しないでください。 詳細については、「[サイト マップを使用したアプリケーション ナビゲーションへのビューの表示](open-forms-views-dialogs-reports-url.md#BKMK_DisplayViewInApplicationUsingSiteMap)」を参照してください。  

 URL で表示されるページにはビュー全体が含まれます。 これにはリボンが含まれますが、アプリケーション ナビゲーションは含まれません。  

##### <a name="get-the-url-for-a-view"></a>ビューの URL の取得  

1. 使用するビューを開きます。  

2. コマンド バーで、**リンクの送信**をクリックし、次に**現在のビュー**をクリックします。  

3. リンクをメモ帳に貼り付けて編集し、テキストから必要な URL 部分のみ抽出します。  

> [!NOTE]
> - ユーザー コンテキストをパラメーターとして使用するビュー (**自分の取引先企業**など) はコピーできません。  
>   - システム エンティティのシステム ビューを表す GUID は、どのバージョンをインストールした場合でも同じになります。 ユーザー定義エンティティおよびユーザー定義ビューの GUID は、 のインストールごとに一意になります。  

<a name="BKMK_DisplayViewInApplicationUsingSiteMap"></a>   
### <a name="display-a-view-in-the-application-navigation-using-the-site-map"></a>サイト マップを使用したアプリケーション ナビゲーションへのビューの表示  
 サイト マップを使用してアプリケーション ナビゲーションをカスタマイズするときは、URL の設定に、「[ビューの URL のコピー](open-forms-views-dialogs-reports-url.md#BKMK_CopyViewURL)」の手順に従ってアプリケーションからコピーしたビューの URL を使用しないでください。 これはリボンを含むページを表示する URL であり、`<SubArea>` Url 属性で使用すると望ましくない結果が生じます。  

 SubArea のアプリケーションに含まれるエンティティ レコードの一覧を表示するには、Entity 属性の値を設定します。 これにより、そのエンティティの既定のビューが正しいタイトルとアイコンで表示されます。  

 ただし、SubArea 要素の既定の初期ビューとして特定のビューを使用する場合は、次の Url のパターンを使用します。  

```xml  
Url=“/_root/homepage.aspx?etn=<entity logical name >&amp;viewid=%7b<GUID value of view id>%7d”  
```  

 この URL を使用するときは、さらに、`<Titles>` と `<Descriptions>` に適切な値を指定し、エンティティのアイコンを指定する必要があります。  

> [!NOTE]
>  `/_root/homepage.aspx` ページを使用してビューを指定した場合も、ビュー セレクターは表示されます。 ユーザーがビューを変更した場合、ユーザーが最後に選択したビューがモデル駆動型アプリで記憶され、ブラウザーを閉じて次に開いたときに既定の初期ビューが表示されます。  

<a name="BKMK_OpenADialogProcess"></a>   
## <a name="opening-a-dialog-process-by-using-a-url"></a>URL を使用してダイアログ プロセスを開く  
 一般的なカスタマイズは、ユーザーが特定のレコードのコンテキストで特定のダイアログ プロセスを開けるようにすることです。 たとえば、現在のレコードの id 値をダイアログ プロセスの入力パラメーターとして使用して、特定のエンティティのリボンにカスタム ボタンを追加できます。  

 ダイアログを開くには、以下が必要です。  

-   ダイアログの一意識別子。  

-   ダイアログの作成対象のエンティティの論理名。  

-   ダイアログの実行対象のレコードの一意識別子。  

> [!TIP]
>  ダイアログの一意識別子を取得するには、**設定**に移動し、既定のソリューションで**プロセス**を選択します。 プロセスを選択し、コマンド バーの**アクション**オプションで、**リンクのコピー**をクリックします。 これにより、たとえば *[organization url]*`/sfa/workflow/edit.aspx?id=%7b6A6E93C9-1FE6-4C07-91A9-E0E2A7C70976%7d` のように、ダイアログを編集するためのリンクがクリップボードにコピーされます。  

 次の例では、ダイアログを開くための URL とクエリ文字列パラメーターを示します。  

```
[organization url]/cs/dialog/rundialog.aspx?DialogId=[dialog unique identifier]&EntityName=[entity logical name]&ObjectId=[unique identifier for the record]  
```  

 たとえば、ID ={6A6E93C9-1FE6-4C07-91A9-E0E2A7C70976}、取引先企業レコード ID = {40C9ADFD-90A8-DF11-840E-00155DBA380F} のダイアログを開くには、次の例の URL を使用します。  

```
[organization url]/cs/dialog/rundialog.aspx?DialogId=%7b6A6E93C9-1FE6-4C07-91A9-E0E2A7C70976%7d&EntityName=account&ObjectId=%7b40C9ADFD-90A8-DF11-840E-00155DBA380F%7d  
```  

> [!TIP]
>  Internet Explorer 以外のブラウザーでは、ダイアログ プロセスをリンクから開いた場合に、 **完了** ボタンが機能しないことがあります。 この場合、データは保存されますが、ウィンドウの**閉じる**ボタンをクリックしないとウィンドウが閉じません。 これは、他のブラウザーでは、別のウィンドウから JavaScript を使用してウィンドウを開いた場合に `window.close` メソッドが提供されないためです。 可能なら、ダイアログ プロセスを開くときは、単にリンクを用意するのではなく、 JavaScript と `window.open` メソッドを使用するようにしてください。  

 次の例に示すように、ダイアログを開くための JavaScript 関数を作成できます。  

```javascript  
function openDialogProcess(dialogId, entityName, objectId)  
{  
 var url = Xrm.Page.context.getClientUrl() +  
  "/cs/dialog/rundialog.aspx?DialogId=" +  
  dialogId + "&EntityName=" +  
  entityName + "&ObjectId=" +  
  objectId;  
 window.open(url);  
}  
```  

<a name="BKMK_OpenReportWithURL"></a>   
## <a name="opening-a-report-by-using-a-url"></a>URL を使用してレポートを開く  
 URL `[organization url]/crmreports/viewer/viewer.aspx` に適切なパラメーター値の渡すことでレポートを開くことができます。  

 この URL は、次のパラメーターを受け取ります。  

 **操作**  
 このパラメーターに可能な 2 つの値は `run` または `filter` のいずれかです。 `run` が使用される場合、レポートは既定のフィルターを使用して表示されます。 `filter` を使用する際、**レポートの実行**ボタンを選択してレポートを表示する前に、レポートにはユーザーが編集できるフィルターが表示されます。  

 **helpID**  
 このパラメータは任意です。 モデル駆動型アプリに含まれているレポートでは、**このページのヘルプ**を選択すると、このパラメータの値は**ヘルプ**ボタンを使用してこのレポートについて適切な内容を表示できます。 値は、レポートの `FileName` 属性値に対応する必要があります。  

 **id**  
 このパラメーターは、レポートの `ReportId` 属性値です。  

 次の例は MDA でレポートを開くために使用できる URL を示します。  

 既定のフィルターを使用して**放置されたサポート案件**レポートを開きます。  
 ```  
 [organization url]/crmreports/viewer/viewer.aspx?action=run&helpID=Neglected%20Cases.rdl&id=%7b8c9f3e6f-7839-e211-831e-00155db7d98f%7d  
 ```  

 **上位のサポート情報記事**レポートを開いて、ユーザーにフィルターの値を設定すよう促します。  
 ```  
 [organization url]/crmreports/viewer/viewer.aspx?action=filter&helpID=Top%20Knowledge%20Base%20Articles.rdl&id=%7bd84ec390-7839-e211-831e-00155db7d98f%7d  
 ```  

 次の機能は、適切に URL の値をエンコードする方法を示しています。  

```javascript  
function getReportURL(action,fileName,id) {  
 var orgUrl = GetGlobalContext().getClientUrl();  
 var reportUrl = orgUrl +   
  "/crmreports/viewer/viewer.aspx?action=" +  
  encodeURIComponent(action) +  
  "&helpID=" +  
  encodeURIComponent(fileName) +  
  "&id=%7b" +  
  encodeURIComponent(id) +  
  "%7d";  
 return reportUrl;  
}  
```  

### <a name="see-also"></a>関連項目   
 [フォームに渡すパラメーターを使用してフィールド値を設定する](set-field-values-using-parameters-passed-form.md)   
 [カスタム クエリストリング パラメーターが許可されるフォームの構成](configure-form-accept-custom-querystring-parameters.md)    
 [リボンのカスタマイズ](customize-commands-ribbon.md)<br/>
 [JavaScript を使用したクライアント スクリプト](client-scripting.md)<br/>
 [Web リソース](web-resources.md)<br/> 
 [クライアントの拡張](/dynamics365/customer-engagement/developer/extend-client)<br/> 
 [SiteMap を使用したアプリケーション ナビゲーションの変更](/dynamics365/customer-engagement/developer/customize-dev/change-application-navigation-using-sitemap)<br/> 
 [URL によるダイアログの起動](/dynamics365/customer-engagement/developer/actions-dialogs#StartDialog)
