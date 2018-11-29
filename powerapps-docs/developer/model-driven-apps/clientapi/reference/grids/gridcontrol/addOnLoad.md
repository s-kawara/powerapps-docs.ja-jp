---
title: モデル駆動型アプリにおける addOnLoad (クライアント API 参照) | Microsoft Docs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 24f34ac9-2a15-478e-980c-588a79d84e8d
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="addonload-client-api-reference"></a>addOnLoad (クライアント API 参照)



[!INCLUDE[./includes/addOnLoad-description.md](./includes/addOnLoad-description.md)]

## <a name="grid-types-supported"></a>サポートされるグリッドの種類

読み取り専用グリッド

## <a name="syntax"></a>構文

`gridContext.addOnLoad(myFunction);`

## <a name="parameter"></a>パラメーター

|Name|種類​​|必須出席者|内容|
|--|--|--|--|
|myFunction|関数リファレンス|あり|サブグリッドの読み込み時に実行する関数。  その関数は、イベント ハンドラー パイプラインの一番下に追加されます。 実行コンテキストは、この関数に最初のパラメーターとして自動的に渡されます。 詳細については、「[実行コンテキスト](../../../clientapi-execution-context.md)」を参照してください。

## <a name="remarks"></a>備考

`gridContext` を取得するには、「[グリッド コンテキストの取得](../../grids.md#bkmk_gridcontext)」を参照してください。

## <a name="example"></a>例

myContactsGridOnloadFunction 関数を取引先担当者 サブグリッド **OnLoad** イベントに追加します。

```JavaScript
function myFunction(executionContext) {
    var formContext = executionContext.getFormContext(); // get the form context
    var gridContext = formContext.getControl("Contacts");// get the grid context
    var myContactsGridOnloadFunction = function () { console.log("Contacts Subgrid OnLoad event occurred") };
    gridContext.addOnLoad(myContactsGridOnloadFunction);
}
```

### <a name="related-topics"></a>関連トピック

[removeOnLoad](removeOnLoad.md)



