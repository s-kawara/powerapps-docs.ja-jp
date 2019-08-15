---
title: モデル駆動型アプリの Xrm.WebApi.online.execute (クライアント API 参照) | MicrosoftDocs
ms.date: 11/21/2018
ms.service: powerapps
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: d4e92999-3b79-4783-8cac-f656fc5f7fda
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="xrmwebapionlineexecute-client-api-reference"></a>Xrm.WebApi.online.execute (クライアント API 参照)



[!INCLUDE[./includes/execute-description.md](./includes/execute-description.md)]

> [!NOTE]
> このメソッドは、オンライン モードでのみサポートされます ([Xrm.WebApi.online](../online.md))。

## <a name="syntax"></a>構文

`Xrm.WebApi.online.execute(request).then(successCallback, errorCallback);`

## <a name="parameters"></a>パラメーター

<table style="width:100%">
<tr>
<th>Name</th>
<th>型</th>
<th>必須出席者</th>
<th>説明</th>
</tr>
<tr>
<td>要求</td>
<td>オブジェクト</td>
<td>あり</td>
<td><p>アクション、関数、または CRUD 要求を実行する Web API エンドポイントに渡されるオブジェクト。 オブジェクトは、実行するアクション、関数、または CRUD 要求のメタデータを定義することができる、<b>getMetadata</b> メソッドを公開します。 <b>getMetadata</b> メソッドには以下のパラメーターがあります。</p>
<ul>
<li><b>boundParameter</b>: (オプション) 文字列。 実行するアクションまたは関数のバインド型パラメーター名。
<ul><li>CRUD 要求を実行する場合、<code>undefined</code> を指定します。</li>
<li>実行するアクションまたは関数がエンティティにバインドされていない場合、<code>null</code> を指定します。</li>
<li>実行するアクションまたは関数がエンティティにバインドされている場合、<code>entity</code> を指定します。 </li></ul>
<li><b>operationName</b>: (オプション)。 文字列。 CRUD 要求の「作成」、「取得」、「更新」、または「削除」を実行する場合の、アクション、関数、または以下のいずれかの値の名前。</li>
<li><b>operationType</b>: (オプション)。 番号。 実行するオペレーションの種類を示します。以下のいずれかの値を指定します。
<br/><code>0: Action</code>
<br/><code>1: Function</code>
<br/><code>2: CRUD</code></li>
<li><b>parameterTypes</b>: オブジェクト。 パラメータの種類のメタデータ。 オブジェクトには次の属性があります。
<ul>
<li><b>enumProperties</b>: (オプション) オブジェクト。 enum の種類のメタデータ。 オブジェクトには 2 つの文字列属性 <b>名前</b> および <b>値</b> があります</li>
<li><b>structuralProperty</b>: 数。 パラメーターの種類のカテゴリ。 次のいずれかの値を指定します。
<br/><code>0: Unknown</code>
<br/><code>1: PrimitiveType</code>
<br/><code>2: ComplexType</code>
<br/><code>3: EnumerationType</code>
<br/><code>4: Collection</code>
<br/><code>5: EntityType</code></li>
<li><b>typeName</b>: 文字列。 パラメーターの種類の完全修飾名です。
</ul>
</li>
</ul>
</td>
</tr>
<tr>
<td>successCallback</td>
<td>関数</td>
<td>No</td>
<td><p>オペレーションが正常に実行されたときにコールされる関数。 応答オブジェクトは以下の属性を持つ関数に渡されます。</p>
<ul>
<li><b>ボディ</b>: (オプション)。 オブジェクト。 応答ボディ。</li>
<li><b>ヘッダー</b>: オブジェクト。 応答ヘッダー。</li>
<li><b>ok</b>: Boolean。 要求が成功したかどうかを示します。</li>
<li><b>ステータス</b>: 数。 応答ステータス コードの数値です。 例: <b>200</b></li>
<li><b>statusText</b>: 文字列。 応答ステータス コードの説明。 例: <b>OK </b></li>
<li><b>種類:</b>: 文字列。 応答の種類。 値は、空の文字列 (既定)、"arraybuffer"、"blob"、"ドキュメント"、"json"、および "テキスト" です。</b></li>
<li><b>URL</b>: 文字列。 Web API エンドポイントに送信された、アクション、関数、または CRUD 要求の要求 URL。</b></li>
</ul>
</td>
</tr>
<tr>
<td>errorCallback</td>
<td>関数</td>
<td>No</td>
<td>処理が失敗したときに呼び出す関数。</td>
</tr>
</table>

## <a name="return-value"></a>戻り値

成功時に、**successCallback** 関数の説明で指定済みの属性を持つ promise オブジェクトを戻します。

## <a name="examples"></a>例

### <a name="execute-an-action"></a>アクションの実行

次の例は、<xref:Microsoft.Dynamics.CRM.WinOpportunity> アクションを実行する方法を説明します。 要求オブジェクトは、[バインドされていないアクション](../../../../../common-data-service/webapi/use-web-api-actions.md#unbound-actions) のアクション定義に基づき作成されます。
```JavaScript
var Sdk = window.Sdk || {};
/**
 * Request to win an opportunity
 * @param {Object} opportunityClose - The opportunity close activity associated with this state change.
 * @param {number} status - Status of the opportunity.
 */
Sdk.WinOpportunityRequest = function (opportunityClose, status) {
    this.OpportunityClose = opportunityClose;
    this.Status = status;

    this.getMetadata = function () {
        return {
            boundParameter: null,
            parameterTypes: {
                "OpportunityClose": {
                    "typeName": "mscrm.opportunityclose",
                    "structuralProperty": 5 // Entity Type
                },
                "Status": {
                    "typeName": "Edm.Int32",
                    "structuralProperty": 1 // Primitive Type
                }
            },
            operationType: 0, // This is an action. Use '1' for functions and '2' for CRUD
            operationName: "WinOpportunity",
        };
    };
};


var opportunityClose = {
    "opportunityid@odata.bind": "/opportunities(c60e0283-5bf2-e311-945f-6c3be5a8dd64)",
    "description": "Product and maintainance for 2018",
    "subject": "Contract for 2018"
}

// Construct a request object from the metadata
var winOpportunityRequest = new Sdk.WinOpportunityRequest(opportunityClose, 3);

// Use the request object to execute the function
Xrm.WebApi.online.execute(winOpportunityRequest).then(
    function (result) {
        if (result.ok) {
            console.log("Status: %s %s", result.status, result.statusText);
            // perform other operations as required;
        }
    },
    function (error) {
        console.log(error.message);
        // handle error conditions
    }
);
```


### <a name="execute-a-function"></a>関数の実行

次の例は、<xref:Microsoft.Dynamics.CRM.WhoAmI> 関数を実行する方法を説明します。

```JavaScript
var Sdk = window.Sdk || {};
/**
 * Request to execute WhoAmI function
 */
Sdk.WhoAmIRequest = function () { };
Sdk.WhoAmIRequest.prototype.getMetadata = function () {
    return {
        boundParameter: null,
        parameterTypes: {},
        operationType: 1, // This is a function. Use '0' for actions and '2' for CRUD
        operationName: "WhoAmI",
    };
};

// Construct a request object from the metadata
var whoAmIRequest = new Sdk.WhoAmIRequest();

// Use the request object to execute the function
Xrm.WebApi.online.execute(whoAmIRequest).then(
    function (result) {
        if (result.ok) {
            console.log("Status: %s %s", result.status, result.statusText);
            result.json().then(
                function (response) {
                    console.log("User Id: %s", response.UserId);
                    // perform other operations as required;
                });
        }
    },
    function (error) {
        console.log(error.message);
        // handle error conditions
    }
);
```

 
### <a name="related-topics"></a>関連トピック


[Xrm.WebApi](../../xrm-webapi.md)




