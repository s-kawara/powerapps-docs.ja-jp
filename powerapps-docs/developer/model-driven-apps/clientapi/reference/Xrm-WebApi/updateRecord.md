---
title: モデル駆動型アプリにおけるupdateRecord (Client API リファレンス) | Microsoft Docs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: f5d4c8a9-4188-472a-83bf-b986dd135754
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="updaterecord-client-api-reference"></a>updateRecord (Client API 参照)



[!INCLUDE[./includes/updateRecord-description.md](./includes/updateRecord-description.md)] 

## <a name="syntax"></a>構文

`Xrm.WebApi.updateRecord(entityLogicalName, id, data).then(successCallback, errorCallback);`

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
<td>更新するレコードのエンティティの論理名。 たとえば、「account」。</td>
</tr>
<tr>
<td>ID</td>
<td>String</td>
<td>あり</td>
<td>更新するエンティティ レコードの GUID。</td>
</tr>
<tr>
<td>data</td>
<td>オブジェクト</td>
<td>あり</td>
<td><p>`key` がエンティティのプロパティである、 <code>key: value</code> ペアを含む JSON オブジェクト <code>value</code> が更新すべきプロパティの値です。</p>
<p>さまざまな更新のシナリオ向けに <code>data</code> オブジェクトを定義する方法については、このトピックの以降の例を参照してください。</td>
</tr>
<tr>
<td>successCallback</td>
<td>関数</td>
<td>No</td>
<td><p>レコードを更新した場合に呼び出す関数。 次のプロパティを持つオブジェクトが渡され、更新されたレコードが識別されます:</p>
<ul>
<li><b>entityType</b>: 文字列。 更新されたレコードのエンティティの種類。</li>
<li><b>id</b>: 文字列。 更新されたレコードの GUID。</li>
</ul></td>
</tr>
<tr>
<td>errorCallback</td>
<td>関数</td>
<td>No</td>
<td>処理が失敗したときに呼び出す関数。 次のプロパティを持つオブジェクトが渡されます。
<ul>
<li><b>errorCode</b>: 数値。 エラー コード。</li>
<li><b>message</b>: 文字列。 問題を示すエラー メッセージが表示されます。</li>
</ul></td>
</tr>
</table>

## <a name="return-value"></a>戻り値

成功時に、**successCallback** パラメーターの説明で指定済みの属性を含む promise オブジェクトを戻します。

## <a name="examples"></a>例

これらの例は [Web API を使用したエンティティの更新と削除](../../../../common-data-service/webapi/update-delete-entities-using-web-api.md) で実演したのと同じ要求オブジェクトを使用して、エンティティ レコードを更新するためのデータ オブジェクトを定義します。

### <a name="basic-update"></a>基本的な更新 

レコード ID = 5531d753-95af-e711-a94e-000d3a11e605 の既存の取引先企業を更新します。

```JavaScript
// define the data to update a record
var data =
    {
        "name": "Updated Sample Account ",
        "creditonhold": true,
        "address1_latitude": 47.639583,
        "description": "This is the updated description of the sample account",
        "revenue": 6000000,
        "accountcategorycode": 2
    }
// update the record
Xrm.WebApi.updateRecord("account", "5531d753-95af-e711-a94e-000d3a11e605", data).then(
    function success(result) {
        console.log("Account updated");
        // perform operations on record update
    },
    function (error) {
        console.log(error.message);
        // handle error conditions
    }
);
```

### <a name="update-associations-to-the-related-entities"></a>関連エンティティの関連付けの更新

関連エンティティ レコード (検索) への関連付けを更新するには、`@odata.bind` 注釈を使用して、単一値ナビゲーション プロパティの値を別のレコードに設定します。 ただし、オフライン モードのモバイル クライアントの場合、`@odata.bind` 注釈を使用することはできません。代わりに、目的のレコードを示す**検索**オブジェクト (**logicalname** および **id**) を渡す必要があります。 これは両方のシナリオ用のコード例です。

**オンライン シナリオ用 (サーバーに接続済み)**

次の例では、アカウント レコードを更新して、別の取引先担当者レコードを取引先企業アカウントの取引先責任者として関連付けます。

```JavaScript
// define the data to update a record
var data =
    {
        "primarycontactid@odata.bind": "/contacts(61a0e5b9-88df-e311-b8e5-6c3be5a8b200)"
    }
// update the record
Xrm.WebApi.updateRecord("account", "5531d753-95af-e711-a94e-000d3a11e605", data).then(
    function success(result) {
        console.log("Account updated");
        // perform operations on record update
    },
    function (error) {
        console.log(error.message);
        // handle error conditions
    }
);
```

**モバイル オフライン シナリオ用**

これは、オフライン モードで作業中にモバイル クライアントから取引先企業レコードを更新して、別の取引先担当者レコードを取引先企業の取引先責任者として関連付ける、更新されたサンプル コードです。

```JavaScript
// define the data to update a record
var data =
    {
        "primarycontactid":
        {
            "logicalname": "contact",
            "id": "61a0e5b9-88df-e311-b8e5-6c3be5a8b200"
        }
    }
// update the record
Xrm.WebApi.offline.updateRecord("account", "5531d753-95af-e711-a94e-000d3a11e605", data).then(
    function success(result) {
        console.log("Account updated");
        // perform operations on record update
    },
    function (error) {
        console.log(error.message);
        // handle error conditions
    }
);
```
 
### <a name="related-topics"></a>関連トピック

[Xrm.WebApi](../xrm-webapi.md)