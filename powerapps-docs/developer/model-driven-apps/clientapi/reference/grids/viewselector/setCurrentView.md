---
title: モデル駆動型アプリにおける setCurrentView (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: f5ee65bf-2964-49c9-9dd2-d81416353bf3
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="setcurrentview-client-api-reference"></a>setCurrentView (クライアント API 参照)



[!INCLUDE[./includes/setCurrentView-description.md](./includes/setCurrentView-description.md)]

## <a name="grid-types-supported"></a>サポートされるグリッドの種類

読み取り専用グリッド

## <a name="syntax"></a>構文

`viewSelector.setCurrentView(object);`

## <a name="parameter"></a>パラメーター

|Name|種類​​|必須出席者|内容|
|--|--|--|--|
|object|検索オブジェクト|あり|検索オブジェクトには、次の 3 つの属性があります。<br/>- **entityType**: 番号。 ユーザーが選択可能なビューを表す、SavedQuery (1039) または UserQuery (4230) のオブジェクトの種類コード。<br/>- **id**: 文字列。 ユーザーが選択できるビューの ID。<br/>- **name**: 文字列。 ユーザーが選択できるビューの名前。|

## <a name="remarks"></a>備考

ビュー セレクターが表示されるようにサブグリッド コントロールが構成されていない場合、`viewSelector` オブジェクトでこのメソッドを呼び出すと、エラーがスローされます。

`viewSelector` オブジェクトを取得するには、「[ViewSelector](../viewselector.md)」を参照してください。

## <a name="example"></a>例

```JavaScript
function setView(executionContext) {
    var ContactsIFollow = {
        entityType: 1039, // SavedQuery
        id: "3A282DA1-5D90-E011-95AE-00155D9CFA02",
        name: "Contacts I Follow"
    }
    // Get the gridContext
    var formContext = executionContext.getFormContext();
    var gridContext = formContext.getControl("Contacts");

    // Set the view using ContactsIFollow
    gridContext.getViewSelector().setCurrentView(ContactsIFollow);
}
```

### <a name="related-topics"></a>関連トピック

[ViewSelector](../viewselector.md)




