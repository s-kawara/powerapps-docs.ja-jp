---
title: 組織サービスを使用したエンティティの更新および削除 (Common Data Service) | Microsoft Docs
description: 組織サービスを使用したエンティティの更新と削除の各操作を実行する方法を説明します。
ms.custom: ''
ms.date: 04/21/2019
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
# <a name="update-and-delete-entities-using-the-organization-service"></a>組織サービスを使用したエンティティの更新と削除

このトピックでは、遅延バインドと事前バインドの両方のプログラミング形式を使用する例を紹介します。 詳細: [組織サービスを使用した事前バインドと遅延バインド プログラミングのクラス](early-bound-programming.md)

それぞれの例では、<xref:Microsoft.Xrm.Sdk.IOrganizationService>インターフェイスのメソッドを実装するクラスのインスタンスを表す `svc` 変数を使用しています。 このインターフェイスのサポートの詳細については、 [IOrganizationService インターフェイス](iorganizationservice-interface.md)を参照してください。

> [!IMPORTANT]
>  エンティティを更新するときは、変更する属性のみを含めます。 前に取得したエンティティの属性を更新するだけで、値が変更されていない場合であっても各属性が更新されます。 これにより、値が実際に変化したことを予期するビジネス ロジックをトリガーすることができる、システム イベントを発生させます。 またこれにより、属性が実際に変更されなかったとき、監査データではプロパティが更新されたように見えます。 
>
> 新しいエンティティ インスタンスを作成して、ID 属性および変更する属性値をセットし、そのエンティティ インスタンスを使用してレコードを更新する必要があります。

> [!NOTE]
> 属性のメタデータは `RequiredLevel` プロパティを含みます。 これが `SystemRequired` に設定された場合、これらの属性を NULL 値に設定することはできません。 これを試みると、メッセージ `Attribute: <attribute name> cannot be set to NULL` とともにエラー コード `-2147220989` を受け取ります。
> 
> 詳細: [属性の入力要求レベル](../entity-attribute-metadata.md#attribute-requirement-level)

## <a name="basic-update"></a>基本的な更新

以下の両方の例で<xref:Microsoft.Xrm.Sdk.IOrganizationService>。<xref:Microsoft.Xrm.Sdk.IOrganizationService.Update*>を使用します メソッドで、以前に取得したエンティティの属性値を設定をします。

<xref:Microsoft.Xrm.Sdk.Entity>.<xref:Microsoft.Xrm.Sdk.Entity.Id> 取得したエンティティの意識別子を、更新操作を実行するために使用されるエンティティ インスタンスに移動するためのプロパティ。

> [!NOTE]
> 主キーに値を設定せずにレコードを更新すると次のエラーになります: `Entity Id must be specified for Update`。
> 
> 主キー値がない場合は、代替キーを使用してレコードを更新することもできます。 詳細: [代替キーで更新する](#update-with-alternate-key)

### <a name="late-bound-example"></a>遅延バインド例

次の例は、<xref:Microsoft.Xrm.Sdk.IOrganizationService>.<xref:Microsoft.Xrm.Sdk.IOrganizationService.Update*>を使う取引先企業レコードを作成するために<xref:Microsoft.Xrm.Sdk.Entity>クラスを使用する方法を示しています  メソッド。 

```csharp
var retrievedAccount = new Entity("account", new Guid("a976763a-ba1c-e811-a954-000d3af451d6"));

//Use Entity class with entity logical name
var account = new Entity("account");
account.Id = retrievedAccount.Id;
// set attribute values
// Boolean (Two option)
account["creditonhold"] = true;
// DateTime
account["lastonholdtime"] = DateTime.Now;
// Double
account["address1_latitude"] = 47.642311;
account["address1_longitude"] = -122.136841;
// Int
account["numberofemployees"] = 400;
// Money
account["revenue"] = new Money(new Decimal(2000000.00));
// Picklist (Option set)
account["accountcategorycode"] = new OptionSetValue(2); //Standard customer

//Update the account
svc.Update(account);
```

### <a name="early-bound-example"></a>事前バインド例

次の例は、<xref:Microsoft.Xrm.Sdk.IOrganizationService>.<xref:Microsoft.Xrm.Sdk.IOrganizationService.Update*>を使う取引先企業レコードを更新するために、生成された `Account` クラスを使用する方法を示しています  メソッド。

```csharp
var retrievedAccount = new Account()
{ Id = new Guid("a976763a-ba1c-e811-a954-000d3af451d6") };

var account = new Account();
account.Id = retrievedAccount.Id;
// set attribute values
// Boolean (Two option)
account.CreditOnHold = true;
// DateTime
account.LastOnHoldTime = DateTime.Now;
// Double
account.Address1_Latitude = 47.642311;
account.Address1_Longitude = -122.136841;
// Int
account.NumberOfEmployees = 400;
// Money
account.Revenue = new Money(new Decimal(2000000.00));
// Picklist (Option set)
account.AccountCategoryCode = new OptionSetValue(2); //Standard customer

//Update the account
svc.Update(account);
```

## <a name="use-the-updaterequest-class"></a>UpdateRequest クラスを使用

<xref:Microsoft.Xrm.Sdk.IOrganizationService>.<xref:Microsoft.Xrm.Sdk.IOrganizationService.Update*>メソッドを使用する代わりに エンティティ インスタンスを<xref:Microsoft.Xrm.Sdk.Messages.UpdateRequest.Target>プロパティに設定し、次に<xref:Microsoft.Xrm.Sdk.IOrganizationService> .<xref:Microsoft.Xrm.Sdk.IOrganizationService.Execute*>を使用して、<xref:Microsoft.Xrm.Sdk.Messages.UpdateRequest>クラスで遅延バインド<xref:Microsoft.Xrm.Sdk.Entity> クラスまたは生成された事前バインド エンティティ クラスのいずれかを使用できます  メソッド。

> [!NOTE]
> <xref:Microsoft.Xrm.Sdk.Messages.UpdateResponse>にはプロパティがありません。 <xref:Microsoft.Xrm.Sdk.IOrganizationService.Execute*>メソッドによって返される場合、それを参照する必要はありません。
 
```csharp
var request = new UpdateRequest()
{ Target = account };
svc.Execute(request);
```
### <a name="when-to-use-the-updaterequest-class"></a>UpdateRequest クラスを使用する場合

オプション パラメーターを渡す場合は、<xref:Microsoft.Xrm.Sdk.Messages.UpdateRequest>クラスを使用する必要があります。 特殊なパラメーターを必要とする場合が 2 つあります。
 - 重複する検出ルールを適用する場合。 詳細: [重複レコードの確認](entity-operations-create.md#check-for-duplicate-records)
 - [WebResource](../reference/entities/webresource.md) などのソリューション コンポーネントを表すエンティティ レコードを作成し、それを特定のソリューションに関連付ける場合。 この場合、`SolutionUniqueName` パラメーターを使用して[Solution.UniqueName](../reference/entities/solution.md#BKMK_UniqueName) の値を含めます。 詳細: [メッセージを組織サービスと共に使用する](use-messages.md)

オプティミスティック同時実行の動作を指定する場合は、<xref:Microsoft.Xrm.Sdk.Messages.UpdateRequest>クラスも使用する必要があります。 詳細: [オプティミスティック同時実行の動作](#optimistic-concurrency-behavior)

## <a name="update-related-entities-in-one-operation"></a>1 回の操作で関連するエンティティを更新する

[1 回の操作で関連するエンティティを作成する](entity-operations-create.md#create-related-entities-in-one-operation) と同じような方法で、関連エンティティを更新することもできます。

これを行うには、ID 値にアクセスできるよう関連レコードを持つエンティティを取得する必要があります。 詳細: [関連レコードの取得](entity-operations-retrieve.md#retrieve-with-related-records)

> [!IMPORTANT]
> レコードに対する更新は、特定の順序で行われます。 まず、主エンティティが処理されてから、関連エンティティが処理されます。 参照属性または関連エンティティ属性に対して主エンティティによって変更が行われてから、関連エンティティが同じ属性を更新した場合は、関連エンティティの値が保持されます。 通常、検索属性値と<xref:Microsoft.Xrm.Sdk.Entity>.<xref:Microsoft.Xrm.Sdk.Entity.RelatedEntities>の同等の値 同じ関連付けに対して、同時に使用しないでください。

### <a name="late-bound-example"></a>遅延バインド例


```csharp
var account = new Entity("account");
account.Id = retrievedAccount.Id;

//Define relationships
var primaryContactRelationship = new Relationship("account_primary_contact");
var AccountTasksRelationship = new Relationship("Account_Tasks");

//Update the account name
account["name"] = "New Account name";

//Update the email address for the primary contact of the account
var contact = new Entity("contact");
contact.Id = retrievedAccount.RelatedEntities[primaryContactRelationship]
.Entities.FirstOrDefault().Id;
contact["emailaddress1"] = "someone_a@example.com";

List<Entity> primaryContacts = new List<Entity>();
primaryContacts.Add(contact);  
account.RelatedEntities.Add(primaryContactRelationship, new EntityCollection(primaryContacts));

// Find related Tasks that need to be updated
List<Entity> tasksToUpdate = retrievedAccount
.RelatedEntities[AccountTasksRelationship].Entities
.Where(t => t["subject"].Equals("Example Task")).ToList();

// A list to put the updated tasks
List<Entity> updatedTasks = new List<Entity>();

//Fill the list of updated tasks based on the tasks that need to but updated
tasksToUpdate.ForEach(t => {
var updatedTask = new Entity("task");
updatedTask.Id = t.Id;
updatedTask["subject"] = "Updated Subject";

updatedTasks.Add(updatedTask);
});

//Set the updated tasks to the collection
account.RelatedEntities.Add(AccountTasksRelationship, new EntityCollection(updatedTasks));

//Update the account and related contact and tasks
svc.Update(account);
```


### <a name="early-bound-example"></a>事前バインド例

```csharp
var account = new Account();
account.Id = retrievedAccount.Id;

//Update the account
account.Name = "New Account name";

//Update the email address for the primary contact of the account
account.account_primary_contact = new Contact
{ Id = retrievedAccount.PrimaryContactId.Id, EMailAddress1 = "someone_a@example.com" };

// Find related Tasks that need to be updated
List<Task> tasksToUpdate = retrievedAccount.Account_Tasks
    .Where(t => t.Subject.Equals("Example Task")).ToList();

// A list to put the updated tasks
List<Task> updatedTasks = new List<Task>();

//Fill the list of updated tasks based on the tasks that need to but updated
tasksToUpdate.ForEach(t =>
{
    updatedTasks
    .Add(new Task() {
        ActivityId = t.ActivityId,
        Subject = "Updated Subject"
    });

});

//Set the updated tasks to the collection
account.Account_Tasks = updatedTasks;

//Update the account and related contact and tasks
svc.Update(account);
```

## <a name="check-for-duplicate-records"></a>重複レコードの確認

エンティティを更新するときは、レコードが別のレコードと重複していることを表すように値を変更します。 詳細: [組織サービスを使用した重複データ検出](detect-duplicate-data.md)

## <a name="update-with-alternate-key"></a>代替キーで更新する

エンティティに代替キーが定義されている場合は、主キーの代わりにそれを使用してレコードを更新できます。 事前バインド型クラスを使用して代替キーを指定できません。 代替キーを指定するには [Entity(文字列, KeyAttributeCollection)](/dotnet/api/microsoft.xrm.sdk.entity.-ctor#Microsoft_Xrm_Sdk_Entity__ctor_System_String_Microsoft_Xrm_Sdk_KeyAttributeCollection_) コンストラクターを使用する必要があります。

事前バインド型クラスを使用する場合は、<xref:Microsoft.Xrm.Sdk.Entity.ToEntity``1> メソッドを使用して <xref:Microsoft.Xrm.Sdk.Entity> を事前バインド型クラスに変換できます。

次の例は `accountnumber` 属性に対して定義された代替キーを使用して、`Account` エンティティを更新する方法を示しています。

> [!IMPORTANT]
> 既定では、どのエンティティに対しても代替キーは定義されていません。 このメソッドは、エンティティーに対して代替キーを定義するように環境が構成されている場合にのみ使用できます。

```csharp
var accountNumberKey = new KeyAttributeCollection();
accountNumberKey.Add(new KeyValuePair<string, object>("accountnumber", "123456"));

Account exampleAccount = new Entity("account", accountNumberKey).ToEntity<Account>();
exampleAccount.Name = "New Account Name";
svc.Update(exampleAccount);
```

詳細: 
- [代替キーに関する作業](../define-alternate-keys-entity.md)
- [代替キーを使用してレコードを作成](../use-alternate-key-create-record.md)

## <a name="use-upsert"></a>upsert の使用

通常、データ統合シナリオでは、他のソースから Common Data Service にデータを作成または更新する必要があります。 Common Data Service には、既に一意識別子と同じレコードが存在する可能性があります。これは代替キーでもかまいません。 エンティティ レコードが存在し、それを更新する場合。 エンティティ レコードが存在しない場合は、追加するデータがソース データと同期するように作成します。 これは、upsert を使いたい場合です。

次の例は<xref:Microsoft.Xrm.Sdk.Messages.UpsertRequest>を 2 回使用します。 1 回目は、アカウント エンティティ レコードが作成するとき、次は `accountnumber` 値を持ち、その属性を使用する代替キーがあるために更新されるときです。

どちらの呼び出しでも、<xref:Microsoft.Xrm.Sdk.Messages.UpsertResponse>.<xref:Microsoft.Xrm.Sdk.Messages.UpsertResponse.RecordCreated> プロパティは、操作がレコードを作成したかどうかを示します。

```csharp
// This environment has an alternate key set for the accountnumber attribute.

//Instantiate account entity with accountnumber value
var account = new Entity("account", "accountnumber", "0003");
account["name"] = "New Account";

//Use Upsert the first time
UpsertRequest request1 = new UpsertRequest() {
Target = account
};

//The new entity is created
var response1 = (UpsertResponse)svc.Execute(request1);
Console.WriteLine("Record Created: {0}",response1.RecordCreated); //true

//Update the name of the existing account entity
account["name"] = "Updated Account";

//Use Upsert for the second time
UpsertRequest request2 = new UpsertRequest()
{
Target = account
};

//The existing entity is updated.
var response2 = (UpsertResponse)svc.Execute(request1);
Console.WriteLine("Record Created: {0}", response2.RecordCreated); //false
```
詳細: [Upsert を使用してレコードを挿入または更新](../use-upsert-insert-update-record.md)

## <a name="delete"></a>削除

<xref:Microsoft.Xrm.Sdk.IOrganizationService>.<xref:Microsoft.Xrm.Sdk.IOrganizationService.Delete*> メソッドはエンティティの論理名と一意識別子を必要とします。 遅延バインド<xref:Microsoft.Xrm.Sdk.Entity>クラスを使用しているのか、生成された事前バインド エンティティ クラスを使用しているのかにかかわらず、<xref:Microsoft.Xrm.Sdk.Entity>.<xref:Microsoft.Xrm.Sdk.Entity.LogicalName>を渡すことによって、削除操作に次の構文を使用できます。 および <xref:Microsoft.Xrm.Sdk.Entity>.<xref:Microsoft.Xrm.Sdk.Entity.Id> プロパティ。

```csharp
svc.Delete(retrievedEntity.LogicalName, retrievedEntity.Id);
```
または、次の値を使用できます。
```csharp
svc.Delete("account", new Guid("e5fa5509-2582-e811-a95e-000d3af40ae7"));
```
> [!IMPORTANT]
> 削除操作では、環境の関連付けに定義されたロジックに応じてデータの整合性を維持するために子レコードを削除するカスケード操作を開始することができます。 詳細: [エンティティ関係の動作](../../../maker/common-data-service/entity-relationship-behavior.md)

## <a name="use-the-deleterequest-class"></a>DeleteRequest クラスの使用

<xref:Microsoft.Xrm.Sdk.IOrganizationService>.<xref:Microsoft.Xrm.Sdk.IOrganizationService.Delete*>メソッドの代わりに<xref:Microsoft.Xrm.Sdk.Messages.DeleteRequest>を使うことができます ただし、オプティミスティック同時実行の動作を指定する場合にのみ必要です。

```csharp
var retrievedEntity = new Entity("account")
{
    Id = new Guid("c81ffd82-cd82-e811-a95c-000d3af49bf8"),
    RowVersion = "986335"

};

var request = new DeleteRequest()
{
    Target = retrievedEntity.ToEntityReference(),
    ConcurrencyBehavior = ConcurrencyBehavior.IfRowVersionMatches
};

svc.Execute(request);
```

## <a name="optimistic-concurrency-behavior"></a>オプティミスティック同時実行の動作

<xref:Microsoft.Xrm.Sdk.Messages.UpdateRequest>または <xref:Microsoft.Xrm.Sdk.Messages.DeleteRequest>クラスの`ConcurrencyBehavior` プロパティを設定すると、操作のためのオプティミスティック同時実行の動作を指定できます。

レコードを更新または削除するロジックは、古いデータに基づいている可能性があります。 最新のデータが取得されてから変更されたために異なる場合は、オプティミスティック同時実行によって更新または削除操作を取り消してから、再度取得して現在のデータを使用して続行するかどうかを判断できます。

エンティティが変更されたかどうかを判断するには、すべての値を比較する必要はなく、<xref:Microsoft.Xrm.Sdk.Entity.RowVersion>プロパティを使用して変更されているかどうかを確認できます。

次の例は、次の場合にのみ成功します。
- データベース内エンティティの `RowVersion` が `986323` と等しい
- 取引先企業エンティティは、オプティミスティック同時実行が可能です (<xref href="Microsoft.Xrm.Sdk.Metadata.EntityMetadata.IsOptimisticConcurrencyEnabled?text=EntityMetadata.IsOptimisticConcurrencyEnabled" />は `true`)
- `RowVersion` プロパティは、要求で渡されたエンティティに設定されます。

`RowVersion` が一致しないと、メッセージ `The version of the existing record doesn't match the RowVersion property provided.` のエラーが発生します。

```csharp
var retrievedAccount = new Account()
{   
    Id = new Guid("a976763a-ba1c-e811-a954-000d3af451d6"), 
    RowVersion = "986323" 
};

var account = new Account();
account.Id = retrievedAccount.Id;
account.RowVersion = retrievedAccount.RowVersion;

// set attribute values
account.CreditOnHold = true;

//Update the account
var request = new UpdateRequest()
{ 
    Target = account,
    ConcurrencyBehavior = ConcurrencyBehavior.IfRowVersionMatches 
};

try
{
    svc.Execute(request);
}
catch (FaultException<OrganizationServiceFault> ex)
{
    switch (ex.Detail.ErrorCode)
    {
        case -2147088254: // ConcurrencyVersionMismatch 
        case -2147088253: // OptimisticConcurrencyNotEnabled 
            throw new InvalidOperationException(ex.Detail.Message);
        case -2147088243: // ConcurrencyVersionNotProvided
            throw new ArgumentNullException(ex.Detail.Message);
        default:
            throw ex;
    }
}
```

詳細: 
- [オプティミスティック同時実行](../optimistic-concurrency.md)
- <xref href="Microsoft.Xrm.Sdk.ConcurrencyBehavior?text=ConcurrencyBehavior Enum"  />

## <a name="legacy-update-messages"></a>従来の更新メッセージ

<!-- https://docs.microsoft.com/dynamics365/customer-engagement/developer/org-service/perform-specialized-operations-using-update -->

更新操作を実行する複数の削除され特化されたメッセージです。 以前のバージョンではこれらのメッセージを使用する必要がありましたが、現在は同じ操作で<xref:Microsoft.Xrm.Sdk.IOrganizationService>.<xref:Microsoft.Xrm.Sdk.IOrganizationService.Update*>を使用して実行されます。 または<xref:Microsoft.Xrm.Sdk.Messages.UpdateRequest>クラスおよび<xref:Microsoft.Xrm.Sdk.IOrganizationService>.<xref:Microsoft.Xrm.Sdk.IOrganizationService.Execute*>

[!INCLUDE [cc-legacy-update-messages](../includes/cc-legacy-update-messages.md)]

詳細: [特化された更新操作の動作](../special-update-operation-behavior.md)

### <a name="see-also"></a>関連項目

[組織サービスを使用したエンティティの作成](entity-operations-create.md)<br />
[組織サービスを使用してエンティティを取得する](entity-operations-retrieve.md)<br />
[組織サービスを使用したエンティティの関連付けまたは関連付けを解除する](entity-operations-associate-disassociate.md)<br />