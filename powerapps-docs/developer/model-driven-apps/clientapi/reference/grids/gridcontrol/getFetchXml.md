---
title: モデル駆動型アプリの getFetchXml (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 4d025f92-db16-440c-9f82-e40d71e09862
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getfetchxml-client-api-reference"></a>getFetchXml (クライアント API 参照)



[!INCLUDE[./includes/getFetchXml-description.md](./includes/getFetchXml-description.md)]

## <a name="grid-types-supported"></a>サポートされるグリッドの種類

読み取り専用および編集可能なグリッド

## <a name="syntax"></a>構文

`var result = gridContext.getfetchXml();`

## <a name="return-value"></a>戻り値

**種類**: 文字列

**説明**: FetchXML クエリ。

## <a name="remarks"></a>備考

`gridContext` を取得するには、「[グリッド コンテキストの取得](../../grids.md#bkmk_gridcontext)」を参照してください 

## <a name="example"></a>例

次の例は、取引先担当者サブグリッドの取得された Fetch XML をコンソールに表示します。

```JavaScript
function myFunction(executionContext) {
    var formContext = executionContext.getFormContext(); // get the form context
    var gridContext = formContext.getControl("Contacts"); // get the grid context
    var retrieveFetchXML = function () {
        var result = gridContext.getFetchXml();
        console.log(result)
    };
    gridContext.addOnLoad(retrieveFetchXML);    
}
```


