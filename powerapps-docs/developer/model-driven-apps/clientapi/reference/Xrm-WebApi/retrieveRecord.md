---
title: モデル駆動型アプリの retrieveRecord (クライアント API 参照) | MicrosoftDocs
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
# <a name="retrieverecord-client-api-reference"></a>retrieveRecord (クライアント API 参照)



[!INCLUDE[./includes/retrieveRecord-description.md](./includes/retrieveRecord-description.md)] 

## <a name="syntax"></a>構文

`Xrm.WebApi.retrieveRecord(entityLogicalName, id, options).then(successCallback, errorCallback);`

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
<td>ID</td>
<td>String</td>
<td>あり</td>
<td>取得するエンティティ レコードの GUID。</td>
</tr>
<tr>
<td>オプション</td>
<td>String</td>
<td>No</td>
<td><p>データを取得する OData システム クエリ オプション、<b>$select</b> および <b>$expand</b>。</p>
<ul><li>プロパティ名のコンマ区切りリストを含めることにより返されるプロパティを制限するためには <b>$select</b> システム クエリ オプションを使用します。 これは重要なパフォーマンスのベスト プラクティスです。 プロパティが <b></b> を使用して指定されない場合は、すべてのプロパティが返されます。</li>
<li><b>$expand</b> システム クエリ オプションを使用して、関連エンティティからどのデータが返されるかをコントロールします。 単にナビゲーション プロパティ名を含めた場合は、関連レコードのすべてのプロパティが表示されます。 ナビゲーション プロパティ名の後にかっこで示される <b>$select</b> システム クエリ オプションを使用して、関連レコードに対して返されるプロパティを制限できます。 これは、<i>単一値</i>と<i>コレクション値</i>のナビゲーション プロパティの両方で使用します。</li>
</ul>
<p><code>?</code> で始まるクエリ オプションを指定します。 クエリ オプションを <code>&</code> で区切って複数のクエリ オプションを指定することもできます。 たとえば、次のようになります。</p>
<code>?$select=name&$expand=primarycontactid($select=contactid,fullname)</code>
<p>さまざまな取得のシナリオ向けに <code>options</code> パラメーターを定義する方法については、このトピックの以降の例を参照してください。</td>
</tr>
<tr>
<td>successCallback</td>
<td>関数</td>
<td>No</td>
<td><p>レコードを取得した場合に呼び出す関数。 取得したプロパティと値を持つ JSON オブジェクトが関数に渡されます。</p>
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

成功すると、取得した属性とその値を持つ JSON オブジェクトを含む Promise が返されます。

## <a name="examples"></a>例

### <a name="basic-retrieve"></a>基本的な取得 

レコード ID = 5531d753-95af-e711-a94e-000d3a11e605 の取引先企業レコードの名前および売り上げを取得します。

```JavaScript
Xrm.WebApi.retrieveRecord("account", "a8a19cdd-88df-e311-b8e5-6c3be5a8b200", "?$select=name,revenue").then(
    function success(result) {
        console.log(`Retrieved values: Name: ${result.name}, Revenue: ${result.revenue}`);
        // perform operations on record retrieval
    },
    function (error) {
        console.log(error.message);
        // handle error conditions
    }
);
```

上の例では、コンソールに以下が表示されます。データによっては、別の値が表示される場合があります。

`Retrieved values: Name: Sample Account, Revenue: 5000000`

### <a name="retrieve-related-entities-for-an-entity-instance-by-expanding-single-valued-navigation-properties"></a>単一値ナビゲーション プロパティの拡張によるエンティティ インスタンスに対する関連エンティティの取得

 以下の例は、レコード ID = a8a19cdd-88df-e311-b8e5-6c3be5a8b200 の取引先企業レコードの取引先担当者を取得する方法を示します。 関連する取引先担当者レコードの場合は、**contactid** および **fullname** プロパティのみを取得します。

```JavaScript
Xrm.WebApi.retrieveRecord("account", "a8a19cdd-88df-e311-b8e5-6c3be5a8b200", "?$select=name&$expand=primarycontactid($select=contactid,fullname)").then(
    function success(result) {
        console.log(`Retrieved values: Name: ${result.name}, Primary Contact ID: ${result.primarycontactid.contactid}, Primary Contact Name: ${result.primarycontactid.fullname}`);
        // perform operations on record retrieval
    },
    function (error) {
        console.log(error.message);
        // handle error conditions
    }
);
```

上の例では、コンソールに以下が表示されます。データによっては、別の値が表示される場合があります。

`Retrieved values: Name: Adventure Works, Primary Contact ID: 49a0e5b9-88df-e311-b8e5-6c3be5a8b200, Primary Contact Name: Adrian Dumitrascu`

 
### <a name="related-topics"></a>関連トピック

[Xrm.WebApi.retrieveMultipleRecords](retrieveMultipleRecords.md)

[Xrm.WebApi](../xrm-webapi.md)




