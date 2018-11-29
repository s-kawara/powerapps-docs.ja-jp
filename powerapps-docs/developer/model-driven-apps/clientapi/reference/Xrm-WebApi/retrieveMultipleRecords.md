---
title: モデル駆動型アプリのフォーム データ retrieveMultipleRecords (クライアント API 参照) | Microsoft Docs
ms.date: 10/31/2018
ms.service: crm-online
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
# <a name="retrievemultiplerecords-client-api-reference"></a>retrieveMultipleRecords (クライアント API 参照)



[!INCLUDE[./includes/retrieveMultipleRecords-description.md](./includes/retrieveMultipleRecords-description.md)] 

## <a name="syntax"></a>構文

`Xrm.WebApi.retrieveMultipleRecords(entityLogicalName, options, maxPageSize).then(successCallback, errorCallback);`

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
<td>取得するレコードのエンティティの論理名。 たとえば、「account」。</td>
</tr>
<tr>
<td>オプション</td>
<td>String</td>
<td>No</td>
<td><p>データを取得する OData システム クエリ オプションまたは FetchXML クエリ。 </p> 
<ul>
<li>システム クエリ オプション <b>$select</b>、<b>$top</b>、<b>$filter</b>、<b>$expand</b>、および <b>$orderby</b> はサポートされます。</li>
<li>FetchXML クエリを指定するには、クエリを指定する <code>fetchXml</code> 属性を使用します。</li>
</ul>
<p>メモ:  <b>$select</b> システム クエリ オプションを使用し、プロパティ名のコンマ区切りリストを含めて、エンティティ レコードに対して返されるプロパティを制限する必要があります。 これは重要なパフォーマンスのベスト プラクティスです。 プロパティが <b></b> を使用して指定されない場合は、すべてのプロパティが返されます。</li>
<p><code>?</code> で始まるクエリ オプションを指定します。 クエリ オプションを <code>&</code> で区切って、複数のシステム クエリ オプションを指定することもできます。
<p>複数取得のさまざまなシナリオ向けに <code>options</code> パラメーターを定義する方法については、このトピックの以降の例を参照してください。</td>
</tr>
<tr>
<td>maxPageSize</td>
<td>数値</td>
<td>No</td>
<td><p>ページごとに返されるエンティティ レコードの数を表す正の数を指定します。 このパラメーターを指定しない場合、既定の 5000 が渡されます。</p>
<p>取得されるレコード数が、指定された <code>maxPageSize</code> 値より多い場合は、返された Promise オブジェクト内の <code>nextLink</code> 属性に、エンティティの次のセットを取得するためのリンクが含まれます。 </td>
</tr>
<tr>
<td>successCallback</td>
<td>関数</td>
<td>No</td>
<td><p>エンティティ レコードを取得した場合に呼び出す関数。 次の属性のオブジェクトは関数に渡されます。</p>
<ul>
<li><b>entities</b>: JSON オブジェクトの配列。各オブジェクトは、属性と値のペア <code>key: value</code> を含む、取得したエンティティ レコードを表します。 既定では、エンティティ レコードの ID が取得されます。</li>
<li><b>nextLink</b>: 文字列。 取得されるレコードの件数が、要求内の <code>maxPageSize</code> パラメーターで指定された値より多い場合、この属性はレコードの次のセットを返す URL を返します。</li>
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

成功すると、要求内でページング (`maxPageSize`) が指定され、返されるレコード数がページング値を超える場合にレコードの次のセットを指す URL とともに、取得したエンティティ レコードおよび **nextLink** 属性 (オプション) を含む JSON オブジェクト (**エンティティ**) の配列を含む promise を返します。

## <a name="examples"></a>例

「[Web API を使用してデータをクエリする](../../../../common-data-service/webapi/query-data-web-api.md)」に記載されたシナリオ/例のほとんどは、**retrieveMutipleRecords** メソッドを使用して実現できます。 いくつかの例を以下に示します。

### <a name="basic-retrieve-multiple"></a>基本的な複数取得

この例は、取引先企業エンティティ セットをクエリし、`$select` および `$top` システム クエリ オプションを使用して、最初の 3 つの取引先企業の名前プロパティを返します。

```JavaScript
Xrm.WebApi.retrieveMultipleRecords("account", "?$select=name&$top=3").then(
    function success(result) {
        for (var i = 0; i < result.entities.length; i++) {
            console.log(result.entities[i]);
        }                    
        // perform additional operations on retrieved records
    },
    function (error) {
        console.log(error.message);
        // handle error conditions
    }
);
```

### <a name="specify-the-number-of-entities-to-return-in-a-page"></a>ページに戻すエンティティ数の指定

次の例では、`maxPageSize` パラメーターを使用して、ページに表示されるレコード数 (3) を指定しています。

```JavaScript
Xrm.WebApi.retrieveMultipleRecords("account", "?$select=name", 3).then(
    function success(result) {
        for (var i = 0; i < result.entities.length; i++) {
            console.log(result.entities[i]);
        }
        console.log("Next page link: " + result.nextLink);
        // perform additional operations on retrieved records
    },
    function (error) {
        console.log(error.message);
        // handle error conditions
    }
);
```

この例では、3 つのレコードと、次のページへのリンクが表示されます。 以下に示すのは、ブラウザー開発ツールの**コンソール**からの出力例です。

```
{@odata.etag: "W/"1035541"", name: "A. Datum", accountid: "475b158c-541c-e511-80d3-3863bb347ba8"}
@odata.etag: "W/"1035541""accountid: "475b158c-541c-e511-80d3-3863bb347ba8"name: "A. Datum"__proto__: Object
VM5595:4 
{@odata.etag: "W/"947306"", name: "Adventure Works", accountid: "a8a19cdd-88df-e311-b8e5-6c3be5a8b200"}
VM5595:4 
{@odata.etag: "W/"1033754"", name: "Alpine Ski House", accountid: "aaa19cdd-88df-e311-b8e5-6c3be5a8b200"}
VM5595:6 
Next page link: [Organization URI]/api/data/v9.0/accounts?$select=name&$skiptoken=%3Ccookie%20pagenumber=%222%22%20pagingcookie=%22%253ccookie%2520page%253d%25221%2522%253e%253caccountid%2520last%253d%2522%257bAAA19CDD-88DF-E311-B8E5-6C3BE5A8B200%257d%2522%2520first%253d%2522%257b475B158C-541C-E511-80D3-3863BB347BA8%257d%2522%2520%252f%253e%253c%252fcookie%253e%22%20istracking=%22False%22%20/%3E
```

`nextLink` プロパティの URL のクエリ部分を、レコードの次のセットを要求するための次の **retrieveMultipleRecords** 呼び出しで `options` パラメーター の値として使用します。 値に対する追加のシステム クエリ オプションを変更または追加しないでください。 以降の追加ページの要求のすべてで、元の複数取得要求で使用したものと同じ `maxPageSize` 値を使用する必要があります。 また、返された結果または nextLink プロパティの値をキャッシュして、以前に取得したページが返されるようにします。 

たとえば、レコードの次のページを取得するには、`nextLink` URL のクエリ部分で `options` パラメーターに渡します。

```JavaScript
Xrm.WebApi.retrieveMultipleRecords("account", "?$select=name&$skiptoken=%3Ccookie%20pagenumber=%222%22%20pagingcookie=%22%253ccookie%2520page%253d%25221%2522%253e%253caccountid%2520last%253d%2522%257bAAA19CDD-88DF-E311-B8E5-6C3BE5A8B200%257d%2522%2520first%253d%2522%257b475B158C-541C-E511-80D3-3863BB347BA8%257d%2522%2520%252f%253e%253c%252fcookie%253e%22%20istracking=%22False%22%20/%3E", 3).then(
    function success(result) {
        for (var i = 0; i < result.entities.length; i++) {
            console.log(result.entities[i]);
        }
        console.log("Next page link: " + result.nextLink);
        // perform additional operations on retrieved records
    },
    function (error) {
        console.log(error.message);
        // handle error conditions
    }
);
```

これで、結果セットの次のページが返されます。

```
{@odata.etag: "W/"1035542"", name: "Blue Yonder Airlines", accountid: "aca19cdd-88df-e311-b8e5-6c3be5a8b200"}
VM5597:4 
{@odata.etag: "W/"1031348"", name: "City Power & Light", accountid: "aea19cdd-88df-e311-b8e5-6c3be5a8b200"}
VM5597:4 
{@odata.etag: "W/"1035543"", name: "Coho Winery", accountid: "b0a19cdd-88df-e311-b8e5-6c3be5a8b200"}
VM5597:6 
Next page link: [Organization URI]/api/data/v9.0/accounts?$select=name&$skiptoken=%3Ccookie%20pagenumber=%223%22%20pagingcookie=%22%253ccookie%2520page%253d%25222%2522%253e%253caccountid%2520last%253d%2522%257bB0A19CDD-88DF-E311-B8E5-6C3BE5A8B200%257d%2522%2520first%253d%2522%257bACA19CDD-88DF-E311-B8E5-6C3BE5A8B200%257d%2522%2520%252f%253e%253c%252fcookie%253e%22%20istracking=%22False%22%20/%3E
``` 
  
> [!IMPORTANT]
>  `nextLink` プロパティの値は URI エンコードされます。 送信前に値を URI エンコードすると、URL 内の XML Cookie 情報によりエラーが発生します。

### <a name="retrieve-related-entities-by-expanding-navigation-properties"></a>ナビゲーション プロパティの拡張による関連エンティティの取得

ナビゲーション プロパティの **$expand** システム クエリ オプションを使用して、関連エンティティから返されるデータをコントロールします。 以下の例は、すべての取引先企業レコードの取引先担当者を取得する方法を示します。 関連する取引先担当者レコードの場合は、`contactid` および `fullname` のみを取得します。

```JavaScript
Xrm.WebApi.retrieveMultipleRecords("account", "?$select=name&$top=3&$expand=primarycontactid($select=contactid,fullname)", 3).then(
    function success(result) {
        for (var i = 0; i < result.entities.length; i++) {
            console.log(result.entities[i]);
        }        
        // perform additional operations on retrieved records
    },
    function (error) {
        console.log(error.message);
        // handle error conditions
    }
);
```


Web API を使用した複数レコード取得のその他の例については、「[Web API を使用してデータをクエリする](../../../../common-data-service/webapi/query-data-web-api.md)」を参照してください。

 
### <a name="related-topics"></a>関連トピック

[Web API を使用したクエリ データ](../../../../common-data-service/webapi/query-data-web-api.md)

[Xrm.WebApi.retrieveRecord](retrieveRecord.md)

[Xrm.WebApi](../xrm-webapi.md)




