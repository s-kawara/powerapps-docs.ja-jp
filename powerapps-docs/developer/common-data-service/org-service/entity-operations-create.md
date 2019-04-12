---
title: 組織サービスを用いたエンティティの作成 (Common Data Service) | Microsoft Docs
description: <Description>
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
# <a name="create-entities-using-the-organization-service"></a>組織サービスを使用したエンティティの作成

このトピックでは、遅延バインドと事前バインドの両方のプログラミング形式を使用する例を紹介します。 詳細: 
- [組織サービスを使用した事前バインドと遅延バインドのプログラミング](early-bound-programming.md)
- [組織サービスの事前バインド クラスを生成する](generate-early-bound-classes.md)

## <a name="basic-create"></a>基本的な作成

以下の例は、遅延バインドおよび事前バインド スタイルを使用してエンティティー レコードを作成する方法を示しています。

<!-- TODO make this an include? -->
それぞれの例では、<xref:Microsoft.Xrm.Sdk.IOrganizationService>インターフェイスのメソッドを実装するクラスのインスタンスを表す `svc` 変数を使用しています。 このインターフェイスのサポートの詳細については、 [IOrganizationService インターフェイス](iorganizationservice-interface.md)を参照してください。

> [!NOTE]
> 各エンティティには、エンティティの作成時に指定できる一意識別子属性があります。 ほとんどの場合、システムによって生成された値は最良なパフォーマンスに最適化されているため、システムがこの属性を設定できるようにする必要があります。


### <a name="late-bound-example"></a>遅延バインドの例

次の例は、<xref:Microsoft.Xrm.Sdk.IOrganizationService>.<xref:Microsoft.Xrm.Sdk.IOrganizationService.Create*> メソッドを使う取引先企業レコードを作成するために <xref:Microsoft.Xrm.Sdk.Entity> クラスを使う方法を示しています。  メソッド。 

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

### <a name="early-bound-example"></a>事前バインドの例

次の例は、<xref:Microsoft.Xrm.Sdk.IOrganizationService>.<xref:Microsoft.Xrm.Sdk.IOrganizationService.Create*> メソッドを使う取引先企業レコードを作成するため、生成された `Account` クラスを使う方法を示しています。  メソッド。

`Account` クラスは、<xref:Microsoft.Xrm.Sdk.Entity> クラスから派生されます

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

## <a name="use-the-createrequest-class"></a>CreateRequest クラスが使用されます

<xref:Microsoft.Xrm.Sdk.IOrganizationService>.<xref:Microsoft.Xrm.Sdk.IOrganizationService.Create*> メソッドを使用する代わりに エンティティ インスタンスを <xref:Microsoft.Xrm.Sdk.Messages.CreateRequest.Target> プロパティに設定し、<xref:Microsoft.Xrm.Sdk.Messages.CreateRequest> クラスで遅延バインド <xref:Microsoft.Xrm.Sdk.Entity> クラスまたは事前バンド エンティティ クラスのいずれかを使用できます。その際に、<xref:Microsoft.Xrm.Sdk.IOrganizationService> .<xref:Microsoft.Xrm.Sdk.IOrganizationService.Execute*>メソッドを使用して、 <xref:Microsoft.Xrm.Sdk.Messages.CreateResponse> を取得します。 作成されたレコードの ID は <xref:Microsoft.Xrm.Sdk.Messages.CreateResponse.id> プロパティ値になります。

```csharp
var request = new CreateRequest() { Target = account };
var response  = (CreateResponse)svc.Execute(request);
Guid accountid = response.id;
```

### <a name="when-to-use-the-createrequest-class"></a>CreateRequest クラスを使用する場合

オプション パラメーターを渡す場合は、<xref:Microsoft.Xrm.Sdk.Messages.CreateRequest> クラスを使用する必要があります。 特殊なパラメーターを必要とする場合が 2 つあります。
 - 重複する検出ルールを適用する場合。 詳細: [重複レコードの確認](#check-for-duplicate-records)
 - [WebResource](../reference/entities/webresource.md) などのソリューション コンポーネントを表すレコードを作成し、それを特定のソリューションに関連付ける場合。 この場合、`SolutionUniqueName` パラメーターを使用して[Solution.UniqueName](../reference/entities/solution.md#BKMK_UniqueName) の値を含めます。 詳細: [メッセージを組織サービスと共に使用する](use-messages.md)

## <a name="create-related-entities-in-one-operation"></a>1 回の操作で関連するエンティティを作成する

新しいエンティティ レコードを作成する場合、同じ操作で関連するエンティティ レコードを作成することもできます。

次の遅延バインドおよび事前バインドの例では、[取引先企業 primarycontactid](../reference/entities/account.md#BKMK_PrimaryContactId) が `ReferencingAttribute` である場合、[account_primary_contact の作成](../reference/entities/contact.md#BKMK_account_primary_contact)の 1 対多の関係を使用して、その取引先企業に関連する[取引先企業](../reference/entities/account.md)および[取引先担当者](../reference/entities/contact.md)を作成します。

この例では、[取引先企業 Account_Tasks](../reference/entities/account.md#BKMK_Account_Tasks) の 1 対多の関係を使用して、3 つの関連する[タスク](../reference/entities/task.md) エンティティレ コードも作成します。この[タスク regardingobjectid](../reference/entities/task.md#BKMK_RegardingObjectId) 検索は `ReferencingAttribute` です。

### <a name="late-bound-example"></a>遅延バインドの例

遅延バインド スタイルでは、<xref:Microsoft.Xrm.Sdk.EntityCollection> に明示的に関連エンティティ (ies) を追加し、その後 関係の `SchemaName` を使用して関係を指定し <xref:Microsoft.Xrm.Sdk.Relationship> クラスを使用する必要があります。これは <xref:Microsoft.Xrm.Sdk.Entity>.<xref:Microsoft.Xrm.Sdk.Entity.RelatedEntities> プロパティに追加する前に行う必要があります。 プロパティに設定します。

```csharp
// Use Entity class with entity logical name
var account = new Entity("account");

// Set attribute values
    // string primary name
    account["name"] = "Sample Account";

// Create Primary contact
var primaryContact = new Entity("contact");
primaryContact["firstname"] = "John";
primaryContact["lastname"] = "Smith";

// Add the contact to an EntityCollection
EntityCollection primaryContactCollection = new EntityCollection();
primaryContactCollection.Entities.Add(primaryContact);

// Set the value to the relationship
account.RelatedEntities[new Relationship("account_primary_contact")] = primaryContactCollection;

// Add related tasks to create
var taskList = new List<Entity>() {
            new Entity("task") { ["subject"] = "Task 1" },
            new Entity("task") { ["subject"] = "Task 2" },
            new Entity("task") { ["subject"] = "Task 3" }
        };

// Add the tasks to an EntityCollection
EntityCollection tasks = new EntityCollection(taskList);

// Set the value to the relationship
account.RelatedEntities[new Relationship("Account_Tasks")] = tasks;

// Create the account
Guid accountid = svc.Create(account);
```

### <a name="early-bound-example"></a>事前バインドの例

事前バインド クラスでは、クラスに関係の定義が含まれているため、コード量を少なくすることができます。

```csharp
var account = new Account();
// set attribute values
    // string primary name
    account.Name = "Sample Account";

    // Set the account primary contact
    account.account_primary_contact = new Contact()
    { FirstName = "John", LastName = "Smith" };

// Set a list of Tasks to create
account.Account_Tasks = new List<Task>() {
        new Task() { Subject = "Task 1" },
        new Task() { Subject = "Task 2" },
        new Task() { Subject = "Task 3" }
    };

// Create the account
Guid accountid = svc.Create(account);
```

## <a name="associate-entities-on-create"></a>作成時にエンティティを関連付ける

新しいレコードを更新するときと同じ方法で、既存のレコードを作成するときに、新しいレコードを関連付けることができます。 検索属性の値を設定するには、<xref:Microsoft.Xrm.Sdk.EntityReference> を使用する必要があります。

この検索属性の割り当ては、事前バインド スタイルと遅延バインド スタイルの両方で同じです。

```csharp
//Use Entity class with entity logical name
var account = new Entity("account");

// set attribute values
    //string primary name
    account["name"] = "Sample Account";

Guid primarycontactid = new Guid("e6fa5509-2582-e811-a95e-000d3af40ae7");

account["primarycontactid"] = new EntityReference("contact", primarycontactid);

//Create the account
Guid accountid = svc.Create(account);
```

### <a name="use-alternate-keys"></a>代替キーの使用

エンティティの ID がわからず、次の条件が当てはまる場合。
- エンティティの代替キーが設定されている
- キー値を知っている

`keyName` および `keyValue` パラメータを使用して、代替の <xref:Microsoft.Xrm.Sdk.EntityReference> コンストラクターを使用できます。
```csharp
account["primarycontactid"] = new EntityReference("contact", "sample_username", "john.smith123");
```
> [!NOTE]
> 代替キーは、通常、データ統合シナリオでのみ使用されます

詳細: 
- [レコードを参照する代替キーの定義](../../../maker/common-data-service/define-alternate-keys-reference-records.md)
- [代替キーを使用してレコードを作成](../use-alternate-key-create-record.md)
- [代替キーに関する作業](../define-alternate-keys-entity.md)


## <a name="check-for-duplicate-records"></a>重複レコードの確認

詳細: [組織サービスを使用した重複データ検出](detect-duplicate-data.md)

## <a name="set-default-values-from-the-primary-entity"></a>主エンティティから既定の値を設定する

アプリケーションで新しいレコードを作成すると、通常、別のレコードのコンテキストで作成されます。 たとえば、取引先企業のコンテキストで新しい取引先担当者レコードを作成することができます。 これが発生すると、取引先企業エンティティから特定の属性値が取引先担当者フォームにコピーされます。 新しいレコードにはいくつかの既定値が設定されているため、作成するレコードを編集する人にこれらの値を入力する必要がないため、新しい関連レコードの作成が迅速化されます。 保存する前に値を変更することができます。

この方法で新しいレコードを作成するときにコピーされる値は、Common Data Service 環境に適用される構成によって制御されるため、環境によって異なる可能性があります。 

詳細: 
- [エンティティ フィールドのマップ](../../../maker/common-data-service/map-entity-fields.md)
- [エンティティ マッピングおよび属性マッピングのカスタマイズ](../customize-entity-attribute-mappings.md)

開発者は、<xref:Microsoft.Crm.Sdk.Messages.InitializeFromRequest> クラスを使用して、既定値が設定済みのエンティティを生成できます。

次のコードは、既存のアカウントに関連付けられている新しい取引先担当者を作成します。 取引先担当者エンティティは指定されたアカウントに関連付けられ、`Telephone1` などの特定の属性値と、取引先企業と取引先担当者エンティティ間で共有されるさまざまなアドレス値が既定で設定されます。

```csharp
//The account that the contact will be associated with:
var parentAccount = new EntityReference("account", new Guid("a976763a-ba1c-e811-a954-000d3af451d6"));

// Initialize a new contact entity with default values from the account.
var request = new InitializeFromRequest()
{
    EntityMoniker = parentAccount,
    TargetEntityName = "contact"

};

var response = (InitializeFromResponse)svc.Execute(request);
//Get the Entity from the response
Entity contact = response.Entity;

// Set values that are not from the account
contact["firstname"] = "Joe";
contact["lastname"] = "Smith";

// Create the contact
Guid contactid = svc.Create(contact);
```

## <a name="use-upsert"></a>upsert の使用

エンティティを作成する別の方法は、<xref:Microsoft.Xrm.Sdk.Messages.UpsertRequest> クラスを使用することです。 upsert は、要求と共に渡されたエンティティに含まれる一意の識別子を持つ既存のレコードが存在しない場合、新しいエンティティを作成します。

詳細: [upsert の使用](entity-operations-update-delete.md#use-upsert)


### <a name="see-also"></a>関連項目

[組織サービスを使用してエンティティを取得する](entity-operations-retrieve.md)<br />
[組織サービスを使用したエンティティの更新と削除](entity-operations-update-delete.md)<br />
[組織サービスを使用したエンティティの関連付けまたは関連付けを解除する](entity-operations-associate-disassociate.md)<br />

