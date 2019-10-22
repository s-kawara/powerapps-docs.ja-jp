---
title: リボンの有効化ルールを定義する (モデル駆動型アプリ) | MicrosoftDocs
description: リボン要素の構成中にそのリボン要素をいつ有効化するかを制御する、特定のルールを定義することについて学習します。
keywords: ''
ms.date: 02/08/2019
ms.service: powerapps
ms.custom:
  - ''
ms.topic: article
ms.assetid: 201f5db9-be65-7c3b-8202-822d78338bd6
author: JesseParsons
ms.author: jeparson
manager: annbe
ms.reviewer: kvivek
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---

# <a name="define-ribbon-enable-rules"></a>リボンの有効化ルールの定義

リボン要素を構成する場合は、そのリボン要素をいつ有効にするかを制御する特定のルールを定義できます。 `<EnableRule>` 要素は、次のように使用します。  

-   リボン要素をいつ有効にする必要があるかを制御するルールを定義するには、`/RuleDefinitions/EnableRules/EnableRule` 要素を使用します。  

-   コマンド定義に対して特定の有効化ルールを関連付けるには、`/CommandDefinitions/CommandDefinition/EnableRules/EnableRule` 要素を使用します。  

## <a name="what-does-enabled-mean"></a>有効になっているとはどういう意味か。  
 コマンド バーでは、無効なコマンドは非表示です。 リボンでは、無効なコマンドは表示されますが、イベントに応答しません。  

## <a name="control-when-ribbon-elements-are-enabled"></a>リボン要素をいつ有効にするかをコントロール  
 有効化ルールは再利用することを前提としています。 ルール定義と一緒に定義することで、同じ有効化ルールを複数のコマンド定義で使用できます。 1 つのコマンド定義に対して複数の有効化ルールを定義した場合、有効化するリボン要素に対してすべての有効化ルールを true と評価する必要があります。  

 すべての有効化ルールには、ルールの既定値が true か false かを指定するための属性、およびテスト対象のアイテムが true を返す場合に負の結果を返せるようにするための `InvertResult` 属性があります。どちらの属性も省略可能です。  

 `/RuleDefinitions/EnableRules/EnableRule` 要素では、次の種類のルールがサポートされています。  

### <a name="command-client-type-rule"></a>コマンド クライアントの種類のルール
 `<CommandClientTypeRule>` 要素を使用します。 [!INCLUDE[ribbon_element_CommandClientTypeRule](../../includes/ribbon-element-commandclienttyperule.md)]  

 `Type` の値は、次に対応します。  


|   Value   |                                                                               プレゼンテーション                                                                               |
|-----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `Modern`  |                                       コマンド バーは、[!INCLUDE[pn_moca_full](../../includes/pn-moca-full.md)]を使用して表現されます。                                       |
| `Refresh` |                                                      コマンド バーは、更新されたユーザー インターフェイスを使用して表示されます。                                                      |
| `Legacy`  | リボンは、更新されなかったエンティティのフォーム、または [!INCLUDE[pn_crm_for_outlook_full](../../includes/pn-crm-for-outlook-full.md)]のリスト ビューで表示されます。 |

### <a name="crm-client-type-rule"></a>Crm クライアントの種類のルール
`<CrmClientTypeRule>` 要素を使用して、使用するクライアントの種類に応じてルールの定義を許可します。 種類のオプションは次のとおりです。  

-   `Web`  

-   `Outlook`  

### <a name="crm-offline-access-state-rule"></a>Crm オフライン アクセス状態ルール
 `<CrmOfflineAccessStateRule>` 要素を使用します。 この条件は、[!INCLUDE[pn_crm_outlook_offline_access](../../includes/pn-crm-outlook-offline-access.md)] が現在オフラインであるかどうかに基づいてリボン要素を有効にする場合に使用します。  

### <a name="crm-outlook-client-type-rule"></a>Crm Outlook クライアントの種類のルール
 `<CrmOutlookClientTypeRule>` 要素を使用します。 特定の種類の [!INCLUDE[pn_crm_for_outlook_full](../../includes/pn-crm-for-outlook-full.md)] でのみボタンを表示する場合は、このルールを使用します。 種類のオプションは次のとおりです。  

-   `CrmForOutlook`  

-   `CrmForOutlookOfflineAccess`  

### <a name="custom-rule"></a>カスタム ルール
 `<CustomRule>` 要素を使用します。 Promise (統一インターフェイス) またはブール値 (統一インターフェイスおよび Web クライアント) を返す JavaScript ライブラリ内の関数を呼び出すには、この種類のルールを使用します。

```JavaScript
function EnableRule()
{
    const value = Xrm.Page.getAttribute("field1").getValue();
    return value === "Active";
}
```

> [!NOTE]
>  すぐに値を返さないユーザー定義ルールは、リボンのパフォーマンスに影響を与える可能性があります。 完了するまで時間がかかることがあるロジックを実行する必要がある場合 (例えば、ネットワーク要求)、次の方式を使用してユーザー定義ルールを非同期にしてください。

 統一インターフェイス ルールは、非同期ルール評価用にブール値よりも Promise を返すことをサポートします。 Promise が 10 秒以内に解決されない場合は、ルールは false 値に解決されます。
 > [!NOTE]
>  Promise ベースのルールは統一インターフェイスでのみ実行されるので、従来の Web クライアントがまだ使われている場合は使用できません。
 ```JavaScript
function EnableRule()
{
    const request = new XMLHttpRequest();
    request.open('GET', '/bar/foo');

    return new Promise((resolve, reject) =>
    {
        request.onload = function (e)
        {
            if (request.readyState === 4)
            {
                if (request.status === 200)
                {
                    resolve(request.responseText === "true");
                }
                else
                {
                    reject(request.statusText);
                }
            }
        };
        request.onerror = function (e)
        {
            reject(request.statusText);
        };

        request.send(null);
    });
}
```


### <a name="entity-rule"></a>エンティティ ルール
 `<EntityRule>` 要素を使用します。 エンティティ ルールでは、現在のエンティティを評価できます。 これは、特定のエンティティではなくエンティティ テンプレートに適用するユーザー定義アクションを定義する場合に有効です。 たとえば、一部の特定のエンティティを除くすべてのエンティティへのリボン要素の追加が必要な場合があります。 この場合、すべてのエンティティに適用するエンティティ テンプレート用のユーザー定義のアクションを定義してから、除外する必要のあるアクションをエンティティ ルールを使用して除外すると簡単です。  

 また、エンティティ ルールには、フォームまたはリストにエンティティが表示されるかどうかを指定するための省略可能なコンテキスト属性 (HomePageGrid) が含まれています。 省略可能な `AppliesTo` 属性を `PrimaryEntity` または `SelectedEntity` に設定すると、エンティティがサブグリッドに表示されているかどうかを識別できます。  

### <a name="form-state-rule"></a>フォーム状態ルール
 `<FormStateRule>` 要素を使用します。 `FormState` ルールは、レコードを表示している現在のフォームの種類を判断する使用します。 状態には次のオプションがあります。  

-   `Create`  

-   `Existing`  

-   `ReadOnly`  

-   `Disabled`  

-   `BulkEdit`  

### <a name="or-rule"></a>Or ルール
 `<OrRule>` 要素を使用します。 `OrRule` を使用すると、複数の有効化ルールの種類に対する既定の AND による比較を無効にすることができます。 確認のために使用可能な複数の有効な結合を定義するには、`OrRule` 要素を使用します。

### <a name="outlook-item-tracking-rule"></a>Outlook アイテム追跡ルール
 `<OutlookItemTrackingRule>` 要素を使用します。 レコードが PowerApps で追跡されているかどうかを判断するには、この要素に対して `TrackedInCrm` 属性を使用します。  

### <a name="outlook-version-rule"></a>Outlook バージョン ルール
 `<OutlookVersionRule>` 要素を使用します。 このルールは、次に示す特定のバージョンの [!INCLUDE[pn_MS_Outlook_Full](../../includes/pn-ms-outlook-full.md)] のリボン要素を有効にする場合に使用します。  

-   `2003`  

-   `2007`  

-   `2010`  

### <a name="page-rule"></a>ページ ルール
 `<PageRule>` 要素を使用します。 この種類のルールでは、表示されているページの URL を確認します。 `Address`が一致した場合は true を返します。  

### <a name="record-privilege-rule"></a>レコード特権ルール
 `<RecordPrivilegeRule>` 要素を使用します。 このルールは、現在のユーザーが特定のレコードに対して特権を持っているかどうかを判断する場合に使用します。 これらの特権には現在のユーザーとレコードを共有している別のユーザーによって取得された特権も含まれるため、エンティティ特権とは異なります。  

### <a name="selection-count-rule"></a>選択カウント ルール
 `<SelectionCountRule>` 要素を使用します。 リストに対して表示されるリボンで、指定した最大数または最小数のレコードがグリッド内で選択された場合にボタンを有効にするには、この種類のルールを使用します。 たとえば、レコードを統合するボタンであれば、リボン コントロールを有効にする前に少なくとも 2 つのレコードが選択されていることを確認する必要があります。  

### <a name="value-rule"></a>値ルール
`<ValueRule>` 要素を使用します。 このルールは、フォームに表示されているレコード内の特定のフィールドの値を確認する場合に使用します。 確認するには`Field`と`Value`を指定する必要があります。

### <a name="see-also"></a>関連項目  
 [コマンド、およびリボンをカスタマイズする](customize-commands-ribbon.md)   
 [リボン コマンドを定義する](define-ribbon-commands.md)   
 [リボンの表示ルールの定義](define-ribbon-display-rules.md)
