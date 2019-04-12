---
title: 組織サービスを用いたエンティティの関連付けおよび関連付け解除 (Common Data Service) | Microsoft Docs
description: 組織サービスを使用してエンティティの関連付けまたは関連付けを解除する方法
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
# <a name="associate-and-disassociate-entities-using-the-organization-service"></a>組織サービスを使用したエンティティの関連付けまたは関連付けを解除する

エンティティ レコードは、関連エンティティの検索属性を使用して相互に関連付けられます。 2 つのエンティティ レコードを 1 対多の関係で関連付ける最も簡単な方法は、<xref:Microsoft.Xrm.Sdk.EntityReference> を使用して関連エンティティの検索属性の値を設定することです。

2 つのエンティティ レコードの 1 対多の関係に関連付けを解除する最も簡単な方法は、検索属性の値を null に設定することです。

多対多の関連付けを使用する関連付けは、多対多関連付けをサポートする*交差エンティティ*の検索属性によっても異なります。 これらの関係は、その交差するエンティティ内のエンティティ レコードの存在によって定義されます。 交差エンティティを直接操作することはできますが、API を使用する方がはるかに簡単です。

## <a name="use-the-associate-method-or-associaterequest"></a>Associate メソッドまたは AssociateRequest の使用

<xref:Microsoft.Xrm.Sdk.IOrganizationService>.<xref:Microsoft.Xrm.Sdk.IOrganizationService.Associate*> メソッド、または または <xref:Microsoft.Xrm.Sdk.Messages.AssociateRequest> を <xref:Microsoft.Xrm.Sdk.IOrganizationService>.<xref:Microsoft.Xrm.Sdk.IOrganizationService.Execute*> メソッド で使用する際の主な価値は、次のことができることです。

- 1 回の操作で複数のレコードを関連付ける
- エンティティを交差させることなく、多対多の関係を使用してレコードを簡単に関連付けることができます。

エンティティ レコードをこれらの API に関連付けるには、次の 3 つのことが必要です。

- 関連付けるエンティティへのエンティティ参照
- 関連付けの名前
- エンティティを関連付ける 1 つ以上の参照

関係が 1 対多であるか多対多であるかは関係ありません。 パラメータまたはプロパティは同等です。

メタデータ ブラウザを使用してカスタマイズ UI またはメタデータを表示することによって、関係の名前を見つけることができます。 詳細: 

- [1:N (一対多) または N:1 (多対一) の関連付けを作成および編集する](../../../maker/common-data-service/create-edit-1n-relationships.md)
- [N:N (多対多) の関連付けを作成および編集する](../../../maker/common-data-service/create-edit-nn-relationships.md)
- [環境のメタデータの参照](../browse-your-metadata.md)

次の例では、特定の連絡先エンティティ (`jimGlynn`) を Redmond にあるすべての取引先担当者のプライマリ連絡先として設定します。


```csharp

// Retrieve the accounts
var query = new QueryByAttribute("account")
{
ColumnSet = new ColumnSet("name")
};
query.AddAttributeValue("address1_city", "Redmond");

EntityCollection accounts = svc.RetrieveMultiple(query);

//Convert the EntityCollection to a EntityReferenceCollection
var accountReferences = new EntityReferenceCollection();

accounts.Entities.ToList().ForEach(x => {
accountReferences.Add(x.ToEntityReference());
});

// The contact to associate to the accounts
var jimGlynn = new EntityReference("contact", 
new Guid("cf76763a-ba1c-e811-a954-000d3af451d6"));

// The relationship to use
var relationship = new Relationship("account_primary_contact");

// Use the Associate method
svc.Associate(jimGlynn.LogicalName, jimGlynn.Id, relationship, accountReferences);
```
それによって特別な利点はありませんが、<xref:Microsoft.Xrm.Sdk.Messages.AssociateRequest> を使用する場合は、最後の行を次のように置き換えることができます。


```csharp
// Use AssociateRequest
AssociateRequest request = new AssociateRequest()
{
RelatedEntities = accountReferences,
Relationship = relationship,
Target = jimGlynn
};

svc.Execute(request);
```

この操作は、[取引先企業](../reference/entities/account.md)に対する 3 つの個別の更新操作と同じです。[PrimaryContactId](../reference/entities/account.md#BKMK_PrimaryContactId) 検索属性ですが、[account_primary_contact](../reference/entities/contact.md#BKMK_account_primary_contact) 関連付けを使用します。これは、エンティティの多対一エンティティ関連付けと、連絡先エンティティの一対多エンティティ関連付けです。

リレーションシップ メタデータのプロパティを調べると、`ReferencingEntity` 値が `account` であり、 `ReferencingAttribute` 値が `primarycontactid` であることがわかります。


## <a name="use-the-disassociate-method-or-disassociaterequest"></a>Disassociate メソッドまたは DisassociateRequest の使用

<xref:Microsoft.Xrm.Sdk.IOrganizationService>.<xref:Microsoft.Xrm.Sdk.IOrganizationService.Disassociate*> メソッドまたは <xref:Microsoft.Xrm.Sdk.Messages.DisassociateRequest> と <xref:Microsoft.Xrm.Sdk.IOrganizationService>.<xref:Microsoft.Xrm.Sdk.IOrganizationService.Execute*> メソッドは 、エンティティ レコードを関連付ける方法の逆になります。

次のコードは、上記のサンプルで作成された関連付けを元に戻します。


```csharp
// Retrieve the accounts
var query = new QueryByAttribute("account")
{
ColumnSet = new ColumnSet("name")
};
query.AddAttributeValue("address1_city", "Redmond");

EntityCollection accounts = svc.RetrieveMultiple(query);

//Convert the EntityCollection to a EntityReferenceCollection
var accountReferences = new EntityReferenceCollection();

accounts.Entities.ToList().ForEach(x => {
accountReferences.Add(x.ToEntityReference());
});

// The contact to associate to the accounts
var jimGlynn = new EntityReference("contact", 
new Guid("cf76763a-ba1c-e811-a954-000d3af451d6"));

// The relationship to use
var relationship = new Relationship("account_primary_contact");

// Use the Disassociate method
svc.Disassociate(jimGlynn.LogicalName, jimGlynn.Id, relationship, accountReferences);
```
それによって特別な利点はありませんが、<xref:Microsoft.Xrm.Sdk.Messages.DisassociateRequest> を使用する場合は、最後の行を次のように置き換えることができます。

```csharp
// Use DisassociateRequest
DisassociateRequest request = new DisassociateRequest()
{
RelatedEntities = accountReferences,
Relationship = relationship,
Target = jimGlynn
};

svc.Execute(request);
```

### <a name="see-also"></a>関連項目

[組織サービスを使用したエンティティの作成](entity-operations-create.md)<br />
[組織サービスを使用してエンティティを取得する](entity-operations-retrieve.md)<br />
[組織サービスを使用したエンティティの更新と削除](entity-operations-update-delete.md)<br />
