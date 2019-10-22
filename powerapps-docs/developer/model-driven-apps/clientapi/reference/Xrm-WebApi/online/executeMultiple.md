---
title: モデル駆動型アプリの Xrm.WebApi.online.executeMultiple (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: powerapps
ms.topic: reference
ms.assetid: d4e92999-3b79-4783-8cac-f656fc5f7fda
author: KumarVivek
ms.author: kvivek
manager: annbe
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="xrmwebapionlineexecutemultiple-client-api-reference"></a>Xrm.WebApi.online.executeMultiple (クライアント API 参照)

[!INCLUDE[./includes/executeMultiple-description.md](./includes/executeMultiple-description.md)]

> [!NOTE]
> このメソッドは、オンライン モードでのみサポートされます ([Xrm.WebApi.online](../online.md))。 

トランザクション内で複数の要求を実行する場合、変更セットをパラメーターとしてこのメソッドに渡す必要があります。 [変更セット](../../../../../common-data-service/webapi/execute-batch-operations-using-web-api.md#change-sets) はトランザクションで実行されるオペレーションのコレクションを示します。 また、個々の要求および変更セットを一緒にパラメーターとしてこのメソッドに渡すことができます。

> [!NOTE]
> 読み取りオペレーション (取得、複数取得、および Web API 関数) を変更セットの一部として含めることはできません。これは OData v4 仕様です。

## <a name="syntax"></a>構文

**複数の要求を実行する:**

```JavaScript
var requests = [req1, req2, req3];
Xrm.WebApi.online.executeMultiple(requests).then(successCallback, errorCallback);
```

**トランザクション内で複数の要求を実行する:**

この場合、`req1`、`req2`、および `req3` がトランザクション内で実行されます。

```JavaScript
var changeSet = [req1, req2, req3];
var requests = [changeSet];
Xrm.WebApi.online.executeMultiple(requests).then(successCallback, errorCallback);
```


**トランザクション内で個々の要求および複数の要求の混在を実行:**

この場合、`req1`、`req2`、および `req3` はトランザクションで実行されますが、`req4` および `req5` は個々に実行されます。

```JavaScript
var changeSet = [req1, req2, req3];
var requests = [req4, req5, changeset];
Xrm.WebApi.online.executeMultiple(requests).then(successCallback, errorCallback);
```

## <a name="parameters"></a>パラメーター

<table style="width:100%">
<tr>
<th>Name</th>
<th>種類​​</th>
<th>必須出席者</th>
<th>内容</th>
</tr>
<tr>
<td>要求</td>
<td>オブジェクトの配列</td>
<td>あり</td>
<td><p>以下のいずれかの種類の配列:</p>
<ul>
<li>各オブジェクトが、Web API エンドポイントに対して実行するアクション、関数、または CRUD 要求であるオブジェクト。 各オブジェクトは、実行するアクション、関数、または CRUD 要求のメタデータを定義することができる、<b>getMetadata</b> メソッドを公開します。 これは <code>execute</code> メソッドを渡すのと同じオブジェクトです。 オブジェクトの詳細については、<a href="execute.md">実行</a> を参照してください。</li>
<li>変更セット内の各オブジェクトが上記のように定義された変更セット (オブジェクトの配列)。 この場合、変更セットで指定されたすべての要求オブジェクトがトランザクションで実行されます。</li>
</ul>
<p>詳細については、**構文**セクションの前半の要求例を参照してください。</p>
</td>
</tr>
<tr>
<td>successCallback</td>
<td>関数</td>
<td>No</td>
<td><p>オペレーションが正常に実行されたときにコールされる関数。 応答オブジェクトの配列は、各応答オブジェクトが以下の属性を持つ関数に渡されます。</p>
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

成功時に、**successCallback** 関数の説明で指定済みの属性を持つオブジェクトの配列を含む promise を戻します。

### <a name="related-topics"></a>関連トピック

[Xrm.WebApi](../../xrm-webapi.md)

