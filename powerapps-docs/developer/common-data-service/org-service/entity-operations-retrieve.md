---
title: 組織サービスを用いたエンティティの取得 (Common Data Service) | Microsoft Docs
description: プログラムでレコードを取得するときに使用できるオプションについて説明します。
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
# <a name="retrieve-an-entity-using-the-organization-service"></a>組織サービスを使用してエンティティを取得する

通常、クエリの結果に基づいてレコードを取得し、クエリ結果にはエンティティ レコードの一意の識別子を含める必要があります。

> [!NOTE]
> 次の例では、`accountid` 変数は、取引先企業エンティティ レコードの <xref:System.Guid> 識別子を表します。

エンティティ レコードを取得するときに返されるデータを定義するオプションがあります。 <xref:Microsoft.Xrm.Sdk.Query.ColumnSet> クラスを使用して、必要な属性値を定義します。


> [!IMPORTANT]
> エンティティ レコードを取得するときは、 <xref:Microsoft.Xrm.Sdk.Query.ColumnSet> クラス コンストラクター使用して特定の属性を設定するだけで、必要な属性値を要求する必要があります。 <xref:Microsoft.Xrm.Sdk.Query.ColumnSet> クラス コンストラクターにはブーリアンの `allColumns` パラメータを受け入れる負荷がありますが、運用コードでは使用しないでください。 詳細: [クエリ API を使用してエンティティのすべての列を取得することはできません](/dynamics365/customer-engagement/guidance/data/retrieve-specific-columns-entity-via-query-apis)

関連するエンティティ レコードを返す必要がある場合は、検索要求と共にクエリを含めて、返す関連レコードを定義することができます。


## <a name="basic-retrieve"></a>基本的な取得

<xref:Microsoft.Xrm.Sdk.IOrganizationService>.<xref:Microsoft.Xrm.Sdk.IOrganizationService.Retrieve*> メソッドを使用するか、 <xref:Microsoft.Xrm.Sdk.Messages.RetrieveRequest> クラスの <xref:Microsoft.Xrm.Sdk.Messages.RetrieveRequest.Target> プロパティを参照レコードに設定し、<xref:Microsoft.Xrm.Sdk.IOrganizationService>.<xref:Microsoft.Xrm.Sdk.IOrganizationService.Execute*> メソッドを使用して、個々のレコードを取得できます。  メソッド。

この例では、<xref:Microsoft.Xrm.Sdk.IOrganizationService>.<xref:Microsoft.Xrm.Sdk.IOrganizationService.Retrieve*> メソッドを使用しています。  メソッド。

```csharp
Entity entity = svc.Retrieve("account", accountid, new ColumnSet("name"));
Console.WriteLine("account name: {0}", entity["name"]);
```

この例では、<xref:Microsoft.Xrm.Sdk.Messages.RetrieveRequest> クラスと <xref:Microsoft.Xrm.Sdk.Messages.RetrieveRequest> クラスを <xref:Microsoft.Xrm.Sdk.IOrganizationService>.<xref:Microsoft.Xrm.Sdk.IOrganizationService.Execute*> メソッドで使用する方法を示しています。  メソッド。

```csharp
RetrieveRequest request = new RetrieveRequest()
{
  ColumnSet = new ColumnSet("name"),
  Target = new EntityReference("account", accountid)
};
var response = (RetrieveResponse)svc.Execute(request);
Entity entity = response.Entity;
Console.WriteLine("account name: {0}", entity["name"]);
```

> [!NOTE]
> ほとんどの場合、<xref:Microsoft.Xrm.Sdk.IOrganizationService>.<xref:Microsoft.Xrm.Sdk.IOrganizationService.Retrieve*> メソッドを使用します。  メソッド。
>
> 以下で説明するように、特別な状況の場合は、<xref:Microsoft.Xrm.Sdk.Messages.RetrieveRequest> を <xref:Microsoft.Xrm.Sdk.IOrganizationService>.<xref:Microsoft.Xrm.Sdk.IOrganizationService.Execute*> メソッド で使用します。 
> 詳細: 
> - [関連レコードの取得](#retrieve-with-related-records)
> - [代替キーの取得](#retrieve-with-an-alternate-key)


## <a name="retrieve-with-related-records"></a>関連レコードで取得

個々のレコードを取得するときは、<xref:Microsoft.Xrm.Sdk.Messages.RetrieveRequest> の <xref:Microsoft.Xrm.Sdk.Messages.RetrieveRequest.RelatedEntitiesQuery> プロパティを設定して、関連するレコードを含めるためのクエリを組み込むこともできます。

<xref:Microsoft.Xrm.Sdk.Query.QueryBase> から派生した任意のクラスを使用してクエリを定義し、特定のエンティティ関係に関連付けることができます。 <xref:Microsoft.Xrm.Sdk.RelationshipQueryCollection> を使用して、<xref:Microsoft.Xrm.Sdk.Messages.RetrieveRequest.RelatedEntitiesQuery> プロパティにクエリと関連付けのペアのコレクションを追加します。

次の例には、取得されている `account` エンティティ レコードに関連する `task` レコードと `contact` レコードが含まれています。

```csharp

var relationshipQueryCollection = new RelationshipQueryCollection();

var relatedTasks = new QueryExpression("task");
relatedTasks.ColumnSet = new ColumnSet("subject", "description");
var taskRelationship = new Relationship("Account_Tasks");
relationshipQueryCollection.Add(taskRelationship, relatedTasks);


var relatedContacts = new QueryExpression("contact");
relatedContacts.ColumnSet = new ColumnSet("fullname", "emailaddress1");
var contactRelationship = new Relationship("account_primary_contact");
relationshipQueryCollection.Add(contactRelationship, relatedContacts);

var request = new RetrieveRequest()
{
  ColumnSet = new ColumnSet(true),
  RelatedEntitiesQuery = relationshipQueryCollection,
  Target = new EntityReference("account", accountid)
};

RetrieveResponse response = (RetrieveResponse)svc.Execute(request);

Entity retrievedAccount = response.Entity;

Console.WriteLine("Account Name: {0}",retrievedAccount["name"]);

var tasks = retrievedAccount.RelatedEntities[new Relationship("Account_Tasks")];

Console.WriteLine("Tasks:");
tasks.Entities.ToList().ForEach(x => {
  Console.WriteLine(" Task Subject: {0}",x["subject"]);
});

Entity primaryContact = retrievedAccount
  .RelatedEntities[new Relationship("account_primary_contact")]
  .Entities.FirstOrDefault();

Console.WriteLine("Primary Contact Fullname: {0}",primaryContact["fullname"]);
```
サンプルの結果は次のようになります。

```
Account Name: City Power & Light (sample)
Tasks:
 Task Subject: Task 1
 Task Subject: Task 2
Primary Contact Fullname: Scott Konersmann (sample)
```

詳細: [組織サービスを使用したクエリ データ](entity-operations-query-data.md)


## <a name="retrieve-with-an-alternate-key"></a>代替キーで取得

代替キーを使用するようにエンティティを設定した場合は、この代替キーを使用して <xref:Microsoft.Xrm.Sdk.EntityReference> を定義し、この値を <xref:Microsoft.Xrm.Sdk.Messages.RetrieveRequest>.<xref:Microsoft.Xrm.Sdk.Messages.RetrieveRequest.Target> プロパティに設定します。

たとえば、アカウントの `account` `accountnumber` 属性を代替キーに定義すると、その属性の値を使用してアカウントを取得できます。


```csharp
RetrieveRequest request = new RetrieveRequest()
{
ColumnSet = new ColumnSet("name"),
Target = new EntityReference("account", "accountnumber", "0001")
};
var response = (RetrieveResponse)svc.Execute(request);
Entity entity = response.Entity;

Console.WriteLine(entity["name"]);
```

代替キーが複数の属性の複合体である場合は、<xref:Microsoft.Xrm.Sdk.KeyAttributeCollection> を定義します。 次の例は、`accountnumber` 属性と `sic` 属性の両方を含む代替キーを持つ取引先企業エンティティの例です。

```csharp
var keyCollection = new KeyAttributeCollection();
keyCollection.Add("accountnumber", "0001");
keyCollection.Add("sic", "7372");

RetrieveRequest request = new RetrieveRequest()
{
ColumnSet = new ColumnSet("name"),
Target = new EntityReference("account", keyCollection)
};
var response = (RetrieveResponse)svc.Execute(request);
Entity entity = response.Entity;

Console.WriteLine(entity["name"]);
```
> [!NOTE]
> 代替キーは、通常、データ統合シナリオでのみ使用されます


## <a name="access-formatted-values"></a>書式設定された値にアクセスする

検索操作で書式設定された値にアクセスする方法は、クエリの結果でアクセスするときに使用する方法と同じです。 詳細: [書式設定された値にアクセスする](entity-operations-query-data.md#access-formatted-values)

<!-- TODO Move the information about accessing formatted values here, where the topic is shorter rather than the query topic which is longer -->

### <a name="see-also"></a>関連項目

[組織サービスを使用したエンティティの作成](entity-operations-create.md)<br />
[組織サービスを使用したエンティティの更新と削除](entity-operations-update-delete.md)<br />
[組織サービスを使用したエンティティの関連付けまたは関連付けを解除する](entity-operations-associate-disassociate.md)<br />
