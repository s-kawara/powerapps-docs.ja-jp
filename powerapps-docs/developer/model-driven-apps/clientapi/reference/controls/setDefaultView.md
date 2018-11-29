---
title: モデル駆動型アプリにおける setDefaultView (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 8c918cd4-d0ce-45e5-91a3-1addf11258c7
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="setdefaultview-client-api-reference"></a>setDefaultView (クライアント API 参照)



検索コントロール ダイアログ ボックスの既定のビューを設定します。

## <a name="control-types-supported"></a>サポートされているコントロールの種類

検索

## <a name="syntax"></a>構文

`formContext.getControl(arg).setDefaultView(viewId);`

## <a name="parameter"></a>パラメーター

|Name|種類​​|必須出席者|内容|
|--|--|--|--|
|viewId|String|あり|既定のビューとして設定されるビューの ID。|

## <a name="example"></a>例

この **setDefaultViewSample** 機能 は、**取引先企業**エンティティ フォームの取引先責任者検索の既定のビューを**自分のアクティブな取引先担当者**に設定します。

```JavaScript
function setDefaultViewSample(executionContext) {
    var formContext = executionContext.getFormContext();
    formContext.getControl("primarycontactid").setDefaultView("{00000000-0000-0000-00AA-000010001003}");
}
```

### <a name="related-topics"></a>関連トピック

[getDefaultView](getDefaultView.md) 


