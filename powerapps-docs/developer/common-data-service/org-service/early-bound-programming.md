---
title: 組織サービスを使用した遅延バインドおよび早期バインドプログラム (Common Data Service) | Microsoft Docs
description: 組織サービスで .NET SDK アセンブリを使うときは、利用可能な異なるプログラミング スタイルが表示されます。
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
# <a name="late-bound-and-early-bound-programming-using-the-organization-service"></a>組織サービスを使用して遅延バインドと事前バインドのプログラミング クラス

組織サービスのアセンブリで作業するときは、次の 2 つのスタイルを使用できます: *遅延バインド*および*事前バインド*。

事前バインドと遅延バインドの重要な違いとして、型変換があります。 事前バインドではすべての型をコンパイル時にチェックできるので暗黙的なキャストが一切起こらないのに対し、遅延バインドではオブジェクトの作成時や型に対するアクションの実行時にのみ型のチェックが行われます。 <xref:Microsoft.Xrm.Sdk.Entity> クラスでは、型を明示的に指定して暗黙的なキャストを防ぐ必要があります。

遅延バインドを使用して、コードがコンパイルしたときは使用できなかったカスタム エンティティまたは属性で作業することができます

## <a name="late-bound"></a>遅延バインド

遅延バインド プログラミングでは、<xref:Microsoft.Xrm.Sdk.Entity> クラスを使用し、エンティティおよび `LogicalName` プロパティの値で属性を参照する必要があります。 
- <xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata>.<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata.LogicalName> 
- <xref:Microsoft.Xrm.Sdk.Metadata.AttributeMetadata>.<xref:Microsoft.Xrm.Sdk.Metadata.AttributeMetadata.LogicalName>

関連付けには `LogicalName` プロパティがないので、<xref:Microsoft.Xrm.Sdk.Metadata.RelationshipMetadataBase>.<xref:Microsoft.Xrm.Sdk.Metadata.RelationshipMetadataBase.SchemaName> を確認します。 プロパティが使用されます。

遅延バインド プログラミングの主な利点は、クラスを生成する必要がなく、またプロジェクト中に生成されたファイルを含む必要もありません。 生成されたファイルはかなり大きいです。 

主な欠点:

- エンティティ、属性および関連付けの時間検証をコンパイルしません。
- メタデータの属性および関連付けの名前を知る必要があります。 

> [!TIP]
> この情報を簡単に見つけることができるツールが、Metadata Browser です。 組織にダウンロードおよびインストールできるアプリです。 詳細: [環境に適切なメタデータ ブラウザ](../browse-your-metadata.md) を参照してください。

### <a name="example"></a>例

次の例では、遅延バインド スタイルを使うアカウントを作成します。

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
                
//Create the account
Guid accountid = svc.Create(account);
```

## <a name="early-bound"></a>事前バインド

事前バインド プログラミングでは、生成ツール (CrmSvcUtil.exe) を使い特定組織のメタデータに基づいて、一連のクラスを最初に生成することを要求します。 詳細: [組織サービスを使用して事前バインド プログラミングのクラスを生成](generate-early-bound-classes.md)

生成ツールのコードを使い事前バインド エンティティ クラスを生成した場合、個別の `SchemaName` プロパティ値でクラスと属性プロパティがコードを記述している間、エクスペリエンスは向上します。

- <xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata>.<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata.SchemaName> 
- <xref:Microsoft.Xrm.Sdk.Metadata.AttributeMetadata>.<xref:Microsoft.Xrm.Sdk.Metadata.AttributeMetadata.SchemaName>
- <xref:Microsoft.Xrm.Sdk.Metadata.RelationshipMetadataBase>.<xref:Microsoft.Xrm.Sdk.Metadata.RelationshipMetadataBase.SchemaName>

クラスをインスタンス化し、IntelliSenseに Visual Studio でプロパティと関係の名前を提供させるのみです。

事前バインド プログラミングのため生成されたクラスは、環境に対して定義されているカスタム アクションの定義を含むことができます。 これを使用して、要求と返答の一対のクラスを提供し、カスタム アクションと使用できます。 詳細: [Custom Actions](../custom-actions.md)

アウトプットを変更するため、生成ツールのコードを拡張するオプションもあります。 1 つの拡張で、各オプション セットのオプション値の列挙を作成できます。 各オプション整数値を検索する必要がないので、エクスペリエンスの向上が提供されます。 詳細: [生成ツールのコードの拡張機能を作成](extend-code-generation-tool.md)

ただし、クラスが特定のインスタンスからメタデータを使い生成されたので、各インスタンスは時間の経過とともに変化する異なるエンティティと属性をもつかもしれません。 厳密に型指定されたクラスを生成するときは、存在しないエンティティの作業にコードを記述する必要があるかもしれません。

> [!IMPORTANT]
> 使用する <xref:Microsoft.Xrm.Sdk.IOrganizationService> メソッドを提供するために <xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceProxy> を使用している場合は、<xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceProxy>.<xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceProxy.EnableProxyTypes> を呼び出す必要があります。 事前バインド スタイルを有効にする方法。


### <a name="example"></a>例

次の例では、事前バインド スタイルを使うアカウントを作成します。

```csharp
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

//Create the account
Guid accountid = svc.Create(account);
```

## <a name="choose-which-style"></a>どちらのスタイルか選択

どちらのスタイルを使うか、自由に決めることができます。 次の表では、それぞれの利点と欠点が表示されます。

|事前バインド|遅延バインド|
|--|--|
|コンパイル時にエンティティ、属性および関連付けの名前を確認できます。|エンティティ、属性および関連付けの名前のコンパイル時の検証はありません。|
|エンティティ クラスを生成する必要があります。|エンティティ クラスを生成する必要がありません。|
|IntelliSense サポートの向上|IntelliSense サポートの低下|
|読み取り可能コードの低下| さらに、読み取り可能コードの低下|
|パフォーマンスのわずかな低下|パフォーマンスのわずかな向上|


## <a name="mix-early-and-late-bound"></a>事前および遅延バインドの組み合わせ

すべての生成されたクラスは遅延バインド プログラミングで使用された <xref:Microsoft.Xrm.Sdk.Entity> クラスから継承したので、エンティティ、属性およびクラス内の定義されない関連付けで作業できます。

### <a name="examples"></a>例

次の例では、 <xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext>を使用して早期バインドメソッドと遅延バインドメソッドを併用する一例を示します。  
  
```csharp  
// Create an organization service context object  
AWCServiceContext context = new AWCServiceContext(_serviceProxy);  
  
// Instantiate an account object using the Entity class.  
Entity testaccount = new Entity("account");  
  
// Set several attributes. For account, only the name is required.   
testaccount["name"] = "Fourth Coffee";  
testaccount["emailaddress1"] = "marshd@contoso.com";  
  
// Save the entity using the organization service context object.  
context.AddToAccountSet(testaccount);  
context.SaveChanges();  
  
```  

カスタムの属性が生成されたクラスに含まれなかった場合でも、まだ使えます。


```csharp
var account = new Account();
// set attribute values
    // string primary name
    account.Name = "Contoso";
    // A custom boolean attribute not included in the generated classes.
    account["sample_customboolean"] = false;


//Create the account
Guid accountid = svc.Create(account);
```

#### <a name="assign-an-early-bound-instance-to-a-late-bound-instance"></a>事前バインド インスタンスを遅延バインド インスタンスに割り当てる  
 次の例は、事前バインド インスタンスを遅延バインド インスタンスに割り当てる方法を示します。  
  
```csharp
Entity incident = ((Entity)context.InputParameters[ParameterName.Target]).ToEntity<Incident>();  
Task relatedEntity = new Task() { Id = this.TaskId };  
  
incident.RelatedEntities[new Relationship("Incident_Tasks")] =   
new EntityCollection(new Entity[] { relatedEntity.ToEntity<Entity>() });  
```

### <a name="see-also"></a>関連項目

[組織サービスを使用したエンティティ操作](entity-operations.md)<br />
[組織サービスを使用したエンティティの作成](entity-operations-create.md)<br />
[組織サービスを使用してエンティティを取得する](entity-operations-retrieve.md)<br />
[組織サービスを使用したクエリ データ](entity-operations-query-data.md)<br />
[組織サービスを使用したエンティティの更新と削除](entity-operations-update-delete.md)<br />
[組織サービスを使用したエンティティの関連付けまたは関連付けを解除する](entity-operations-associate-disassociate.md)<br />
[IOrganizationService インターフェイス](iorganizationservice-interface.md)<br />
[OrganizationServiceContext の使用](organizationservicecontext.md)<br />