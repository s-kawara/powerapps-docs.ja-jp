---
title: モデル駆動型アプリにおける addCustomFilter (クライアント API 参照) | Microsoft Docs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: e359b-c4d9-48ac-a57b-367c2e6168c5
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="addcustomfilter-client-api-reference"></a>addCustomFilter (クライアント API 参照)



検索に表示される結果に、Adds フィルターを使用します。 各フィルターは "AND" 条件として、前に追加したフィルターと結合します。

## <a name="control-types-supported"></a>サポートされているコントロールの種類

検索

## <a name="syntax"></a>構文

`formContext.getControl(arg).addCustomFilter(filter, entityLogicaName)`

## <a name="parameters"></a>パラメーター

- **フィルター**文字列 適用する fetchXml フィルター要素。 たとえば、次のようになります。

    ```xml
    <filter type="and">
      <condition attribute="address1_city" operator="eq" value="Redmond" />
    </filter>
    ```

- **entityLogicalName**: (任意) 文字列。 これを設定すると、フィルターは、そのエンティティの種類にのみ適用されます。 それ以外の場合、返されたすべての種類のエンティティに適用されます。

## <a name="remarks"></a>備考

このメソッドは、[検索コントロール PreSearch イベント](../events/presearch.md) のイベント ハンドラー内の関数でのみ使用できます。

## <a name="example"></a>例

次のコード サンプルは、営業案件フォームの**取引先企業** (parentaccountid) 検索用です。 **Sdk.setParentAccountIdFilter** 関数がフォーム **Onload** イベント ハンドラーに設定されている場合、**Sdk.filterCustomAccounts** 関数が検索用 **PreSearch** イベントに追加されます。 **Onload** イベント ハンドラーの形式で関数を設定するときは、実行コンテキストを渡すオプションを選択してください。 結果として、**カテゴリ** (accountcategorycode) の値が**優先する顧客** (1) である取引先企業のみが戻されます。

```JavaScript
// A namespace defined for SDK sample code
// You should define a unique namespace for your libraries
var Sdk = window.Sdk || {};

// set 'Sdk.setParentAccountIdFilter' in the Opportunity form onload event handler
Sdk.setParentAccountIdFilter = function (executionContext) {

    // get the form context
    formContext = executionContext.getFormContext();
    formContext.getControl("parentaccountid").addPreSearch(Sdk.filterCustomerAccounts);
}

Sdk.filterCustomerAccounts = function () {

    // Only show accounts with the type 'Preferred Customer'
    var customerAccountFilter = "<filter type='and'><condition attribute='accountcategorycode' operator='eq' value='1'/></filter>";
    formContext.getControl("parentaccountid").addCustomFilter(customerAccountFilter, "account");
}
```
[addPreSearch](addPreSearch.md)

[formContext](../../clientapi-form-context.md)