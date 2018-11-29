---
title: モデル駆動型アプリにおける deleteRecord (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 848c277b-bd44-4388-852a-0f59a3a15538
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="deleterecord-client-api-reference"></a>deleteRecord (Client API 参照)



[!INCLUDE[./includes/deleteRecord-description.md](./includes/deleteRecord-description.md)] 

## <a name="syntax"></a>構文

`Xrm.WebApi.deleteRecord(entityLogicalName, id).then(successCallback, errorCallback);`

## <a name="parameters"></a>パラメーター

<table style="width:100%">
<tr>
<th>Name</th>
<th>種類​​</th>
<th>必須出席者</th>
<th>内容</th>
</tr>
<tr>
<td>entityLogicalName</td>
<td>String</td>
<td>あり</td>
<td>削除するレコードのエンティティの論理名。 たとえば、「account」。 </td>
</tr>
<tr>
<td>ID</td>
<td>String</td>
<td>あり</td>
<td>削除するエンティティ レコードの GUID。</td>
</tr>
<tr>
<td>successCallback</td>
<td>関数</td>
<td>No</td>
<td><p>レコードを削除した場合に呼び出す関数。 次のプロパティを持つオブジェクトが渡され、削除されたレコードが識別されます:</p>
<ul>
<li><b>entityType</b>: 文字列。 レコードのエンティティの種類。</li>
<li><b>id</b>: 文字列。 レコードの GUID。</li>
<li><b>name</b>: 文字列。 レコードの名前。</li>
</ul></td>
</tr>
<tr>
<td>errorCallback</td>
<td>関数</td>
<td>No</td>
<td>処理が失敗したときに呼び出す関数。</td>
</tr>
</table>

## <a name="return-value"></a>戻り値

成功時に、**successCallback** パラメーターの説明で指定済みの属性を含む promise オブジェクトを戻します。

## <a name="examples"></a>例

これらの例は [Web API を使用したエンティティの更新と削除](../../../../common-data-service/webapi/update-delete-entities-using-web-api.md) で実演したのと同じ要求オブジェクトを使用して、エンティティ レコードを更新するためのデータ オブジェクトを定義します。

レコード ID = 5531d753-95af-e711-a94e-000d3a11e605 の取引先企業を削除します。

```JavaScript
Xrm.WebApi.deleteRecord("account", "5531d753-95af-e711-a94e-000d3a11e605").then(
    function success(result) {
        console.log("Account deleted");
        // perform operations on record deletion
    },
    function (error) {
        console.log(error.message);
        // handle error conditions
    }
);
```
 
### <a name="related-topics"></a>関連トピック

[Xrm.WebApi](../xrm-webapi.md)




