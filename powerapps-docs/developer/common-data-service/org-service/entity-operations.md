---
title: 組織サービスを使用したエンティティ操作 (アプリ用Common Data Service) | Microsoft Docs
description: アプリ用 CDS 組織サービスを使用してデータ操作に使用されるエンティティ クラスについて説明します
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
# <a name="entity-operations-using-the-organization-service"></a>組織サービスを使用したエンティティ操作

組織サービスを使用してアプリ用 Common Data Service データを操作する場合は、遅延バインド スタイルで <xref:Microsoft.Xrm.Sdk.Entity> クラスを使用するか、事前バインド スタイルを使用して生成されたエンティティ クラスを使用します。 生成されたエンティティ クラスは <xref:Microsoft.Xrm.Sdk.Entity> クラスから継承されるため、どちらのスタイルでも <xref:Microsoft.Xrm.Sdk.Entity> クラスを理解することが重要です。

このトピックでは、<xref:Microsoft.Xrm.Sdk.Entity> クラスの最も頻繁に使用されるプロパティとメソッドについて説明します。

## <a name="entitylogicalname"></a>Entity.LogicalName

遅延バインド スタイルを使用して新しい <xref:Microsoft.Xrm.Sdk.Entity> インスタンスをインスタンス化するときは、有効な文字列値を指定してエンティティのタイプを指定する必要があります。 `LogicalName` は、エンティティ メタデータで定義されています。

事前バインド スタイルを使用する場合、この値は生成されたクラスのコンストラクターによって設定されます。 例: `var account = new Entity("account");`

コードで、エンティティのタイプを記述する文字列値を後で取得したい場合は、<xref:Microsoft.Xrm.Sdk.Entity.LogicalName> プロパティを使用できます。 これは、エンティティ論理名をパラメータとして必要とする API の多くを使用する際に便利です。

## <a name="entityid"></a>Entity.Id

遅延バインド スタイルを使用するか、事前バインド スタイルを使用するかどうかに関係なく、エンティティ インスタンスをインスタンス化するときに、一意の ID セットはありません。 エンティティを作成する場合は、エンティティを設定する必要はありませんが、エンティティを作成 (保存) するときにはそのエンティティを設定できます。

エンティティを取得する場合は、エンティティを要求したかどうかにかかわらず、主キーの属性値が含まれます。 主キー属性名は、エンティティのタイプごとに異なります。 一般に、主キー属性の名前はエンティティ `logicalname` + `id` です。 したがって、取引先企業エンティティの場合は `accountid` であり、取引先担当者は `contactid` です。

主キー属性を使用して主キー値を取得または設定できますが、<xref:Microsoft.Xrm.Sdk.Entity.Id>  プロパティを使用して、主キー属性の名前を覚える必要なく値にアクセスすることができます。

## <a name="early-bound-access-to-attributes"></a>属性への事前バインド アクセス

生成されたクラスで事前バインド スタイルを使用している場合、クラスの各属性の型付きプロパティがあります。 属性のプロパティは、<xref:Microsoft.Xrm.Sdk.Metadata.AttributeMetadata>.<xref:Microsoft.Xrm.Sdk.Metadata.AttributeMetadata.SchemaName> を使用し、 エンティティ インスタンス上で直接アクセスできます。
たとえば、次のようになります。 


```csharp
//Using the early-bound Account entity class
var account = new Account();
// set attribute values
// string primary name
account.Name = "Contoso";
// Boolean (Two option)
account.CreditOnHold = false;
// DateTime
account.LastOnHoldTime = new DateTime(2017, 1, 1);
// Double
account.Address1_Latitude = 47.642311;
account.Address1_Longitude = -122.136841;
// Int
account.NumberOfEmployees = 500;
// Money
account.Revenue = new Money(new decimal(5000000.00));
// Picklist (Option set)
account.AccountCategoryCode = new OptionSetValue(1); //Preferred customer
```

## <a name="late-bound-access-to-attributes"></a>属性への遅延バインド アクセス

エンティティに含まれるデータは、<xref:Microsoft.Xrm.Sdk.Entity>.<xref:Microsoft.Xrm.Sdk.Entity.Attributes> プロパティに設定します。 このプロパティは、新しい属性を追加したり、属性が存在するかどうかをチェックしたり、属性を削除したりする一連のメソッドを提供する <xref:Microsoft.Xrm.Sdk.AttributeCollection> です。

### <a name="discover-attribute-names-and-data-types"></a>属性名とデータの種類を発見する

遅延バインド スタイルでは、属性とデータ型の  <xref:Microsoft.Xrm.Sdk.Metadata.AttributeMetadata>.<xref:Microsoft.Xrm.Sdk.Metadata.AttributeMetadata.LogicalName> を 知っておく必要があります。 `LogicalName` は、`SchemaName` の小文字のバージョンです。 `LogicalName` と属性のタイプは、以下の方法で検出できます。

- カスタマイズ ツールで属性の定義を表示する
- システム エンティティの場合は、[エンティティの参照](../reference/about-entity-reference.md) を確認する
- [環境のメタデータの参照](../browse-your-metadata.md)のメタデータ ブラブザーなどのツールを使用して、エンティティのメタデータをブラウザする

属性タイプは、次のいずれかになります。

|型|説明|
|--|--|
|<xref:Microsoft.Xrm.Sdk.EntityReference>|**検索**属性。 別のレコードへのリンク。|
|<xref:Microsoft.Xrm.Sdk.BooleanManagedProperty>|[WebResource Entity](../reference/entities/webresource.md) などのソリューション コンポーネントになることができるエンティティにのみ使用されます。 詳細: [マネージド プロパティの使用](../use-managed-properties.md)|
|<xref:Microsoft.Xrm.Sdk.Money>|**通貨**属性。|
|<xref:Microsoft.Xrm.Sdk.OptionSetValue>|**オプション セット**属性。 **状態**および**状態**属性もこの種類を使用します。 |
|<xref:System.Boolean>|**2 つのオプション**属性。|
|<xref:System.Byte>[]|**イメージ**属性。 各エンティティは 1 つのイメージを持つことができ、属性の名前は `entityimage` です。 イメージをダウンロードする URL は、`entityimage_url` という名前のコンパニオン属性で取得することができます。 詳細: [イメージ属性](../image-attributes.md) |
|<xref:System.DateTime>|**日時**属性は、通常、UTC 値を使用します。 詳細: [日時属性の動作と形式](../behavior-format-date-time-attribute.md)|
|<xref:System.Decimal>|**10 進数**属性。|
|<xref:System.Double>|**浮動小数点数**属性。|
|<xref:System.Guid>|通常、エンティティの一意の識別子として使用されます。 |
|<xref:System.Int32>|**整数**属性。|
|<xref:System.String>|**複数行テキスト**および **1 行テキスト**属性がこの種類を使用します。|



遅延バインド スタイルを使用してエンティティ属性を操作する方法は 3 つあります。
- エンティティでインデクサを使用する
- `Attributes` コレクションでインデクサを使用する
- 提供されたエンティティ メソッドを使用する

### <a name="use-the-indexer-on-the-entity"></a>エンティティでインデクサを使用する

遅延バインド スタイルを使用する場合のほとんどでは、インデクサを使用して、属性の `LogicalName` を使用する属性の値を取得または設定することによって、コレクションを操作できます。 たとえば、取引先企業の名前属性を設定するには、次のようにします。

```csharp
//Use Entity class with entity logical name
var account = new Entity("account");
// set attribute values
// string primary name
account["name"] = "Contoso";
// Boolean (Two option)
account["creditonhold"] = false;
// DateTime
account["lastonholdtime"] = new DateTime(2017, 1, 1);
// Double
account["address1_latitude"] = 47.642311;
account["address1_longitude"] = -122.136841;
// Int
account["numberofemployees"] = 500;
// Money
account["revenue"] = new Money(new decimal(5000000.00));
// Picklist (Option set)
account["accountcategorycode"] = new OptionSetValue(1); //Preferred customer
```

### <a name="use-the-indexer-on-the-attributes-collection"></a>属性コレクションでインデクサを使用する

エンティティと同じように、属性コレクションのインデクサを使用して値にアクセスすることもできます。

```csharp
string accountName = account.Attributes["name"];
```

### <a name="use-the-entity-methods"></a>エンティティ メソッドを使用する

<xref:Microsoft.Xrm.Sdk.Entity> メソッドを使用して属性値を取得または設定することもできます。

|方法|説明|
|--|--|
|<xref:Microsoft.Xrm.Sdk.Entity.GetAttributeValue``1(System.String)>|型指定された属性値を戻します|
|<xref:Microsoft.Xrm.Sdk.Entity.SetAttributeValue(System.String,System.Object)>|型指定された属性値を設定します|

たとえば、次のようになります。

```csharp
account.SetAttributeValue("name", "Account Name");
var accountName = account.GetAttributeValue<string>("name");
```



## <a name="entityformattedvalues"></a>Entity.FormattedValues

UI に表示され、文字列ではないエンティティ属性値には、UI に値を表示するために使用できる文字列形式の値があります。 たとえば、次のようになります。

- 金額には、適切な通貨と桁数の書式設定の文字列値が含まれます。
- 日付の値は、システムの構成方法に応じて設定されます
- OptionSet の値には、整数値を表すローカライズされたラベルが表示されます

> [!NOTE]
> 書式設定された値は、取得されたエンティティにのみ適用されます。 値を設定すると、エンティティを保存し、エンティティを再度取得するまで、新しい形式の値は計算されません。 フォーマットされた値はサーバー上で生成されます。

インデクサまたはエンティティ <xref:Microsoft.Xrm.Sdk.Entity.GetFormattedAttributeValue(System.String)> メソッドを使用する、<xref:Microsoft.Xrm.Sdk.Entity.FormattedValues> コレクションを使用して、書式設定された値にアクセスできます。

たとえば、これらの両方で同じ形式の値を取得します。

```csharp
var formattedRevenueString1 = account.FormattedValues["revenue"];
var formattedRevenueString2 = account.GetFormattedAttributeValue("revenue");
```

詳細: [書式設定された値にアクセスする](entity-operations-query-data.md#access-formatted-values)

## <a name="entityrelatedentities"></a>Entity.RelatedEntities 

エンティティを作成するときに、同じ操作で作成する関連エンティティ レコードのセットを定義することもできます。 詳細: [1 回の操作で関連するエンティティを作成する](entity-operations-create.md#create-related-entities-in-one-operation)

エンティティを取得するときに、関連するエンティティを結果に含めるためにクエリで <xref:Microsoft.Xrm.Sdk.Messages.RetrieveRequest> を設定することによって、<xref:Microsoft.Xrm.Sdk.Messages.RetrieveRequest.RelatedEntitiesQuery> を使用することができます。 詳細: [関連レコードの取得](entity-operations-retrieve.md#retrieve-with-related-records)

関連するエンティティを結果に含めると、それらの関連エンティティの値を更新し、エンティティを更新するときにそれらのエンティティを含めることもできます。 詳細: [1 回の操作で関連するエンティティを更新する](entity-operations-update-delete.md#update-related-entities-in-one-operation)

## <a name="convert-to-an-entityreference"></a>EntityReference への変換

多くのメッセージ プロパティは <xref:Microsoft.Xrm.Sdk.EntityReference> のみを必要とします。 <xref:Microsoft.Xrm.Sdk.Entity>.<xref:Microsoft.Xrm.Sdk.Entity.ToEntityReference> メソッドを使用し、エンティティをエンティティ参照に変換します。

## <a name="convert-to-an-entity-class"></a>エンティティ クラスに変換します

事前バインド スタイルを使用している場合、生成された、使用しているエンティティ クラスの種類に <xref:Microsoft.Xrm.Sdk.Entity> インスタンスを変換する必要があります。 これは通常、キャストで行うことができますが、<xref:Microsoft.Xrm.Sdk.Entity>.<xref:Microsoft.Xrm.Sdk.Entity.ToEntity``1> メソッドを使用することもできます。  メソッド。

```csharp
Account account1 = (Account)retrievedEntity;
Account account2 = retrievedEntity.ToEntity<Account>();
```

> [!NOTE]
> このメソッドを使用して、生成されたエンティティ インスタンスを別の生成クラス、または <xref:Microsoft.Xrm.Sdk.Entity> に変換することはできません。 <xref:Microsoft.Xrm.Sdk.Entity> インスタンスを、継承した生成クラスの 1 つに変換するためにのみ使用できます。 <xref:Microsoft.Xrm.Sdk.Entity> インスタンスが実際に生成されたクラスのインスタンスでない場合、このメッセージはエラーをスローします。

## <a name="next-steps"></a>次の手順

これらのトピックでは、アプリ用 CDS エンティティの使用について詳しく説明します。

[クイック スタート: 組織サービス サンプル (C#)](quick-start-org-service-console-app.md)
[クエリ データ](entity-operations-query-data.md)<br />
[エンティティの作成](entity-operations-create.md)<br />
[エンティティの取得](entity-operations-retrieve.md)<br />
[エンティティの更新と削除](entity-operations-update-delete.md)<br />
[エンティティの関連付けと関連付け解除](entity-operations-associate-disassociate.md)<br />
[事前バインド プログラミングのクラスを生成する](generate-early-bound-classes.md)<br />