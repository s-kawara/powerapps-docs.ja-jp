---
title: モデル駆動型アプリの createRecord (クライアント API 参照) | MicrosoftDocs
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
# <a name="createrecord-client-api-reference"></a>createRecord (Client API 参照)



[!INCLUDE[./includes/createRecord-description.md](./includes/createRecord-description.md)] 

## <a name="syntax"></a>構文

`Xrm.WebApi.createRecord(entityLogicalName, data).then(successCallback, errorCallback);`

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
<td>作成するエンティティの論理名。 たとえば、「account」。</td>
</tr>
<tr>
<td>data</td>
<td>オブジェクト</td>
<td>あり</td>
<td><p>新しいエンティティ レコードの属性および値を定義する JSON オブジェクト。</p>
<p>さまざまな作成のシナリオ向けに <code>data</code> オブジェクトを定義する方法については、このトピックの以降の例を参照してください。</td>
</tr>
<tr>
<td>successCallback</td>
<td>関数</td>
<td>No</td>
<td><p>レコードを作成した場合に呼び出す関数。 次のプロパティを持つオブジェクトが渡され、新しいレコードが識別されます:</p>
<ul>
<li><b>entityType</b>: 文字列。 新しいレコードのエンティティ論理名。</li>
<li><b>id</b>: 文字列。 新しいレコードの GUID。</li>
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

これらの例は [Web API を使用してエンティティを作成する](../../../../common-data-service/webapi/create-entity-web-api.md) で実演したのと同じ要求オブジェクトを使用して、エンティティ レコードを作成するためのデータ オブジェクトを定義します。

### <a name="basic-create"></a>基本的な作成 

サンプルの取引先企業レコードを作成します。

```JavaScript
// define the data to create new account
var data =
    {
        "name": "Sample Account",
        "creditonhold": false,
        "address1_latitude": 47.639583,
        "description": "This is the description of the sample account",
        "revenue": 5000000,
        "accountcategorycode": 1
    }

// create account record
Xrm.WebApi.createRecord("account", data).then(
    function success(result) {
        console.log("Account created with ID: " + result.id);
        // perform operations on record creation
    },
    function (error) {
        console.log(error.message);
        // handle error conditions
    }
);
```

### <a name="create-related-entity-records-along-with-the-primary-record"></a>プライマリ レコードと共に関連エンティティ レコードを作成する

 ナビゲーション プロパティの値として定義することで、相互に関連するエンティティを作成することができます。 これを*ディープ挿入*と言います。 この例では、取引先責任者レコードとそれに関連する営業案件レコードと共にサンプル取引先企業レコードを作成します。

```JavaScript
// define data to create primary and related entity records
var data =
    {
        "name": "Sample Account",
        "primarycontactid":
        {
            "firstname": "John",
            "lastname": "Smith"
        },
        "opportunity_customer_accounts":
        [
            {
                "name": "Opportunity associated to Sample Account",
                "Opportunity_Tasks":
                [
                    { "subject": "Task associated to opportunity" }
                ]
            }
        ]
    }

// create account record
Xrm.WebApi.createRecord("account", data).then(
    function success(result) {
        console.log("Account created with ID: " + result.id);
        // perform operations on record creation
    },
    function (error) {
        console.log(error.message);
        // handle error conditions
    }
);
```

### <a name="associate-entities-on-creating-new-records"></a>新しいレコードの作成に関連するエンティティ

新しいエンティティ レコードを既存のエンティティ レコードに関連付けるには、`@odata.bind` 注釈を使用して、単一値ナビゲーション プロパティの値を設定します。 ただし、オフライン モードのモバイル クライアントの場合、`@odata.bind` 注釈を使用することはできません。代わりに、目的のレコードを示す**検索**オブジェクト (**logicalname** および **id**) を渡す必要があります。 これは両方のシナリオ用のコード例です。 


**オンライン シナリオ用 (サーバーに接続済み)**

次の例は取引先企業レコードを作成して、既存の取引先担当者レコードに関連付け、後者を新しい取引先企業レコードの取引先責任者としてセットします。

```JavaScript
var data =
    {
        "name": "Sample Account",
        "primarycontactid@odata.bind": "/contacts(465b158c-541c-e511-80d3-3863bb347ba8)"
    }

// create account record
Xrm.WebApi.createRecord("account", data).then(
    function success(result) {
        console.log("Account created with ID: " + result.id);
        // perform operations on record creation
    },
    function (error) {
        console.log(error.message);
        // handle error conditions
    }
);
```

**モバイル オフライン シナリオ用**

これは、オフライン モードで作業中にモバイル クライアントから取引先企業レコードを作成して、それを既存の取引先担当者レコードに関連付け、この取引先担当者レコードを新しい取引先企業レコードの取引先責任者として設定する、更新されたサンプル コードです。

```JavaScript
var data =
    {
        "name": "Sample Account",
        "primarycontactid":
        {
            "logicalname": "contact",
            "id": "465b158c-541c-e511-80d3-3863bb347ba8"
        } 
    }

// create account record
Xrm.WebApi.offline.createRecord("account", data).then(
    function success(result) {
        console.log("Account created with ID: " + result.id);
        // perform operations on record creation
    },
    function (error) {
        console.log(error.message);
        // handle error conditions
    }
);
``` 
 
### <a name="related-topics"></a>関連トピック

[Web API を使用してエンティティを作成する](../../../../common-data-service/webapi/create-entity-web-api.md) 

[Xrm.WebApi](../xrm-webapi.md)