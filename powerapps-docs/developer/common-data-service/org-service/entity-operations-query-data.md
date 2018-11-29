---
title: 組織サービスを使用してデータをクエリ (アプリ用 Common Data Service) | Microsoft Docs
description: アプリ用 CDS SDK アセンブリを使用してデータを照会するさまざまな方法を紹介します。
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: brandonsimons
ms.author: jdaly
manager: ryjones
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="query-data-using-the-organization-service"></a>組織サービスを使用したクエリ データ

組織サービス用の SDK アセンブリは、データをクエリするためのいくつかのスタイルを提供します。 それぞれにはさまざまな利点があります。

|スタイル|利点|
|--|--|
|[FetchExpression](#use-fetchxml-with-fetchexpression)|返されるすべてのレコードの値の合計などの集計を返す複雑なクエリを作成するには FetchXML クエリ言語のプロパティを使用します。 FetchXML でグループ化操作も実行できます。 リンクされたエンティティからのデータを含むことができます。|
|[QueryExpression](#use-queryexpression)|複雑なクエリを作成するには、厳密に型指定されたオブジェクト モデルが必要です。 FetchXML の集計とグループ化を除くすべての機能をサポートします。 リンクされたエンティティからのデータを含むことができます。|
|[QueryByAttribute](#use-querybyattribute)|`QueryExpression` より単純なオブジェクトモデルです。 クエリのすべての属性値の条件が一致するかどうかをテストするクエリに対して、`QueryByAttribute` を使用します。 エンティティからのデータのみを返すことができます。|
|[LINQ](/dotnet/csharp/programming-guide/concepts/linq/introduction-to-linq)|<xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext>.<xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext.QueryProvider>を使用し 一般的な LINQ 構文を使用してクエリを作成します。 すべての LINQ クエリは <xref:Microsoft.Xrm.Sdk.Query.QueryExpression> に変換されるため、この機能は  `QueryExpression` で使用できるものに限定されています <br /> このトピックでは、SDK アセンブリ クラスを使用して使用できるクエリのスタイルに焦点を当てます。 詳細: [LINQ (.NET 統合言語クエリ) を使用してクエリを作成する](build-queries-with-linq-net-language-integrated-query.md)|


<xref:Microsoft.Xrm.Sdk.Query.FetchExpression>、<xref:Microsoft.Xrm.Sdk.Query.QueryExpression>、および <xref:Microsoft.Xrm.Sdk.Query.QueryByAttribute> は、<xref:Microsoft.Xrm.Sdk.Query.QueryBase> 抽象クラスから派生しています。 これらのクラスを使用して定義されたクエリの結果を取得するには、2 つの方法があります。

- これらのクラスのいずれかのインスタンスを `query` パラメータとして<xref:Microsoft.Xrm.Sdk.IOrganizationService>.<xref:Microsoft.Xrm.Sdk.IOrganizationService.RetrieveMultiple*> メソッドに渡すことができます。  メソッド。
- <xref:Microsoft.Xrm.Sdk.Messages.RetrieveMultipleRequest> クラスの <xref:Microsoft.Xrm.Sdk.Messages.RetrieveMultipleRequest.Query> プロパティを設定し、<xref:Microsoft.Xrm.Sdk.IOrganizationService>.<xref:Microsoft.Xrm.Sdk.IOrganizationService.Execute*> メソッドを使用できます。  メソッド。

> [!NOTE]
> <xref:Microsoft.Xrm.Sdk.IOrganizationService>.<xref:Microsoft.Xrm.Sdk.IOrganizationService.RetrieveMultiple*> メソッドが優先されます。 <xref:Microsoft.Xrm.Sdk.Messages.RetrieveMultipleRequest> クラスの使用を必要とする特別な機能はありません。

これらのメソッドは両方とも、<xref:Microsoft.Xrm.Sdk.EntityCollection.Entities> コレクション内のクエリの結果と、ページングされた結果を受信するための追加のクエリを管理するプロパティを含む <xref:Microsoft.Xrm.Sdk.EntityCollection> を返します。 

> [!NOTE]
> 最高のパフォーマンスを保証するために、各クエリ要求は最大 5000 のエンティティ レコードを返すことができます。 より大きな結果セットを返すには、追加のページをリクエストする必要があります。

### <a name="null-attribute-values-are-not-returned"></a>Null 属性値は返されません

属性に NULL 値が含まれている場合、または FetchXml 属性または<xref:Microsoft.Xrm.Sdk.Query.ColumnSet> に属性が含まれていない場合、<xref:Microsoft.Xrm.Sdk.Entity>.<xref:Microsoft.Xrm.Sdk.Entity.Attributes> コレクション には属性が含まれません。 属性にアクセスするためのキー、または返す値はありません。 属性の欠落は、それが null であることを示しています。 事前バインド スタイルを使用する場合、生成されたエンティティ クラス プロパティはこれを管理し、null 値を返します。

遅延バインド スタイルを使用する場合、<xref:Microsoft.Xrm.Sdk.Entity.Attributes> または <xref:Microsoft.Xrm.Sdk.Entity.FormattedValues> コレクションのインデクサを使用して値にアクセスしようとすると、`The given key was not present in the dictionary` メッセージの <xref:System.Collections.Generic.KeyNotFoundException> が発生します。

遅延バインド スタイルを使用するときにこれを避けるには、2 つの方法があります。

1. null の可能性のある属性の場合、属性が null かどうかをインデクサでアクセスしようとする前に確認するために<xref:Microsoft.Xrm.Sdk.Entity>.<xref:Microsoft.Xrm.Sdk.Entity.Contains(System.String)> メソッド を使用します。 たとえば、次のようになります。

    `Money revenue = (entity.Contains("revenue")? entity["revenue"] : null);`

1. <xref:Microsoft.Xrm.Sdk.Entity>.<xref:Microsoft.Xrm.Sdk.Entity.GetAttributeValue``1(System.String)> を使用し 値にアクセスします。 たとえば、次のようになります。

    `Money revenue = entity.GetAttributeValue<Money>();`

  > [!NOTE]
  > <xref:Microsoft.Xrm.Sdk.Entity.GetAttributeValue``1(System.String)> で指定された型が、<xref:System.Boolean> または <xref:System.DateTime> などの null にできない値の型である場合、返される値は null ではなく、 `false` または `1/1/0001 12:00:00 AM` などの既定値です。




## <a name="use-fetchxml-with-fetchexpression"></a>FetchExpression を使用した FetchXML の使用

FetchXml は、<xref:Microsoft.Xrm.Sdk.Query.FetchExpression> を使用する SDK アセンブリ クエリと `fetchXml` クエリ文字列を使用する Web API で使用できる独自の XML ベースのクエリ言語です。 詳細: [Web API : 定義済みクエリの取得と実行 > ユーザー定義の FetchXML を使用する](../webapi/retrieve-and-execute-predefined-queries.md#use-custom-fetchxml)

次の例は、`address1_city` の値が `Redmond` と等しい、50 個の一致する取引先企業エンティティを `name` で並べ替えて返す簡単なクエリを示しています。

```csharp
string fetchXml = @"
<fetch top='50' >
  <entity name='account' >
    <attribute name='name' />
    <filter>
      <condition 
        attribute='address1_city' 
        operator='eq' 
        value='Redmond' />
    </filter>
    <order attribute='name' />
  </entity>
</fetch>";

var query = new FetchExpression(fetchXml);

EntityCollection results = svc.RetrieveMultiple(query);

results.Entities.ToList().ForEach(x => {
  Console.WriteLine(x.Attributes["name"]);
});
```

> [!IMPORTANT]
> エンティティ レコードを取得するときは、すべての属性を返すために `all-attributes` 要素を使用するのではなく、`attribute` 要素を使用して特定の属性を設定するだけで、必要な属性値を要求する必要があります。


詳細:
- [FetchXML の使用によるクエリの作成](../use-fetchxml-construct-query.md)
- [FetchXML スキーマ](../fetchxml-schema.md)
- [FetchXML による大量の結果セットのページング](page-large-result-sets-with-fetchxml.md)
- [FetchXML 集計の使用](../use-fetchxml-aggregation.md)
- [FetchXML の会計日クエリ演算子および older than 日付/時刻クエリ演算子](../use-fetchxml-fiscal-date-older-datetime-query-operators.md)
- [左外部結合を FetchXML で使用して "存在しない" 記録をクエリする](../use-fetchxml-left-outer-join-query-records-not-in.md)
- [サンプル: FetchXML での集計の使用](samples/use-aggregation-fetchxml.md)
- [サンプル: ページング Cookie を使用した FetchXML の使用](samples/use-fetchxml-paging-cookie.md)

## <a name="use-queryexpression"></a>QueryExpression の使用

<xref:Microsoft.Xrm.Sdk.Query.QueryExpression> クラスは、クエリの実行時操作のために最適化された、厳密に型指定されたオブジェクトのセットを提供します。

次の例は、`address1_city` の値が `Redmond` と等しい、50 個の一致する取引先企業エンティティを `name` で並べ替えて返す簡単なクエリを示しています。

```csharp
var query = new QueryExpression("account")
{
  ColumnSet = new ColumnSet("name"),
  Criteria = new FilterExpression(LogicalOperator.And),
  TopCount = 50
};
query.Criteria.AddCondition("address1_city", ConditionOperator.Equal, "Redmond");
query.AddOrder("name", OrderType.Ascending);

EntityCollection results = svc.RetrieveMultiple(query);

results.Entities.ToList().ForEach(x =>
{
  Console.WriteLine(x.Attributes["name"]);
});
```

> [!IMPORTANT]
> エンティティ レコードを取得するときは、 <xref:Microsoft.Xrm.Sdk.Query.ColumnSet> クラス コンストラクター使用して特定の属性を設定するだけで、必要な属性値を要求する必要があります。 <xref:Microsoft.Xrm.Sdk.Query.ColumnSet> クラス コンストラクターにはブーリアンの `allColumns` パラメータを受け入れる負荷がありますが、運用コードでは使用しないでください。


詳細:
- [QueryExpression でクエリを作成する](build-queries-with-queryexpression.md)
- [QueryExpression を使用して大きな結果セットをページングする](page-large-result-sets-with-queryexpression.md)
- [QueryExpression クラスの使用](use-queryexpression-class.md)
- [ConditionExpression クラスの使用](use-conditionexpression-class.md)
- [ColumnSet クラスの使用](use-the-columnset-class.md)
- [FilterExpression クラスの使用](use-filterexpression-class.md)
- [サンプル: QueryExpression クラスを使用した複数取得](samples/retrieve-multiple-queryexpression-class.md)
- [サンプル: ページング Cookie を使用した QueryExpression の使用](samples/use-queryexpression-with-a-paging-cookie.md)

## <a name="use-querybyattribute"></a>QueryByAttribute の使用

<xref:Microsoft.Xrm.Sdk.Query.QueryByAttribute> クラスは、エンティティの単純で一般的なクエリに対して最適化された、厳密に型指定されたオブジェクトのセットを提供します。 FetchXML および`QueryExpression` とは違い、`QueryByAttribute` はエンティティからのデータのみを返します。 関連エンティティまたは複雑なクエリ基準からデータを取得することはできません。

次の例は、`address1_city` の値が `Redmond` と等しい、50 個の一致する取引先企業エンティティを `name` で並べ替えて返す簡単なクエリを示しています。

```csharp
var query = new QueryByAttribute("account")
{
  TopCount = 50,
  ColumnSet = new ColumnSet("name")
};
query.AddAttributeValue("address1_city", "Redmond");
query.AddOrder("name", OrderType.Ascending);

EntityCollection results = svc.RetrieveMultiple(query);

results.Entities.ToList().ForEach(x =>
{
  Console.WriteLine(x.Attributes["name"]);
});
```

詳細:
- [QueryByAttribute クラスの使用](use-querybyattribute-class.md)
- [サンプル: QueryByAttribute クラスを使用した複数取得](samples/retrieve-multiple-querybyattribute-class.md)


## <a name="access-formatted-values"></a>書式設定された値にアクセスする

エンティティのクエリに使用するメソッドに関係なく、データは <xref:Microsoft.Xrm.Sdk.EntityCollection>.<xref:Microsoft.Xrm.Sdk.EntityCollection.Entities> として返されます 属性データ値にアクセスするには <xref:Microsoft.Xrm.Sdk.Entity>.<xref:Microsoft.Xrm.Sdk.Entity.Attributes> コレクション を使用します。 しかし、これらの値は、アプリケーションで表示できる文字列値を取得するために操作する必要のある、文字列以外の型である可能性があります。

書式設定の環境設定を使用する文字列値にアクセスするには、<xref:Microsoft.Xrm.Sdk.Entity>.<xref:Microsoft.Xrm.Sdk.Entity.FormattedValues> コレクション の値を使用します。

次のサンプルは、次の取引先企業属性の書式設定された文字列値にアクセスする方法を示しています。

|属性の論理名|型|
|--|--|
|`primarycontactid`|<xref:Microsoft.Xrm.Sdk.EntityReference>|
|`createdon`|<xref:System.DateTime>|
|`revenue`|<xref:Microsoft.Xrm.Sdk.Money>|
|`statecode`|<xref:Microsoft.Xrm.Sdk.OptionSetValue>|

```csharp
var query = new QueryByAttribute("account")
{
TopCount = 50,
ColumnSet = new ColumnSet("name", "primarycontactid", "createdon", "revenue", "statecode")
};
query.AddAttributeValue("address1_city", "Redmond");
query.AddOrder("name", OrderType.Ascending);

EntityCollection results = svc.RetrieveMultiple(query);

results.Entities.ToList().ForEach(x =>
{
Console.WriteLine(@"
name:{0}
primary contact: {1}
created on: {2}
revenue: {3}
status: {4}",
  x.Attributes["name"],
  (x.Contains("primarycontactid")? x.FormattedValues["primarycontactid"]:string.Empty),
  x.FormattedValues["createdon"],
  (x.Contains("revenue") ? x.FormattedValues["revenue"] : string.Empty),
  x.FormattedValues["statecode"]
  );
});
```

> [!NOTE]
> null 値を含む属性は、クエリ `Attributes` または `FormattedValues` コレクションには返されません。 属性に null 値が含まれる場合は、値にアクセスする前に <xref:Microsoft.Xrm.Sdk.Entity.Contains*> メソッドを使用してチェックする必要があります。

書式設定された結果は、次のように表示されます。

```
name:A Datum (sample)
  primary contact: Rene Valdes (sample)
  created on: 2/28/2018 11:04 AM
  revenue: $10,000.000
  status: Active

name:City Power & Light (sample)
  primary contact: Scott Konersmann (sample)
  created on: 2/28/2018 11:04 AM
  revenue: $100,000.000
  status: Active

name:Contoso Pharmaceuticals (sample)
  primary contact: Robert Lyon (sample)
  created on: 2/28/2018 11:04 AM
  revenue: $60,000.000
  status: Active
```


## <a name="convert-queries-between-fetchxml-and-queryexpression"></a>FetchXml と QueryExpression の間でクエリを変換する

<xref:Microsoft.Xrm.Sdk.Query.QueryExpression> クエリを FetchXml、および FetchXml を QueryExpression に変換するには、<xref:Microsoft.Crm.Sdk.Messages.QueryExpressionToFetchXmlRequest> および <xref:Microsoft.Crm.Sdk.Messages.FetchXmlToQueryExpressionRequest> クラスを使用します。

[SavedQuery](../reference/entities/savedquery.md) エンティティはエンティティのシステム ビューを保存し、[UserQuery](../reference/entities/userquery.md) エンティティは保存されたユーザー クエリを保存します。 他のエンティティは、クエリを FetchXml 文字列として保存することもできます。 これらのメソッドを使用すると、FetchXml 文字列を <xref:Microsoft.Xrm.Sdk.Query.QueryExpression> に変換し、オブジェクト モデルを使用して操作し、FetchXml に変換して文字列として保存できるようになります。


詳細: [サンプル: Fetch と QueryExpression の間でクエリを変換する](samples/convert-queries-fetch-queryexpression.md)


