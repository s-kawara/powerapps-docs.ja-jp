---
title: エンティティの関連付けの作成および取得 (Common Data Service) | Microsoft Docs
description: コード サンプルを表示し、エンティティ関係を作成および取得します。
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
# <a name="create-and-retrieve-entity-relationships"></a>エンティティ関係の作成および取得

<!-- https://docs.microsoft.com/dynamics365/customer-engagement/developer/org-service/create-retrieve-entity-relationships -->

このトピックでは、エンティティ関係の作成および取得方法について説明します。  
  
<a name="BKMK_Create1NEntityRelationship"></a>   
## <a name="create-a-1n-entity-relationship"></a>1:N のエンティティ関連付けの作成  
 次のサンプルでは、[EligibleCreateOneToManyRelationship](#eligiblecreateonetomanyrelationship) メソッドを使用して、`Account` および `Campaign` エンティティが 1:N のエンティティ関連付けに参加できることを確認し、<xref:Microsoft.Xrm.Sdk.Messages.CreateOneToManyRequest> を使用してエンティティ関連付けを作成します。  
  
```csharp
bool eligibleCreateOneToManyRelationship =
    EligibleCreateOneToManyRelationship("account", "campaign");

if (eligibleCreateOneToManyRelationship)
{
    CreateOneToManyRequest createOneToManyRelationshipRequest =
        new CreateOneToManyRequest
    {
        OneToManyRelationship =
        new OneToManyRelationshipMetadata
        {
            ReferencedEntity = "account",
            ReferencingEntity = "campaign",
            SchemaName = "new_account_campaign",
            AssociatedMenuConfiguration = new AssociatedMenuConfiguration
            {
                Behavior = AssociatedMenuBehavior.UseLabel,
                Group = AssociatedMenuGroup.Details,
                Label = new Label("Account", 1033),
                Order = 10000
            },
            CascadeConfiguration = new CascadeConfiguration
            {
                Assign = CascadeType.NoCascade,
                Delete = CascadeType.RemoveLink,
                Merge = CascadeType.NoCascade,
                Reparent = CascadeType.NoCascade,
                Share = CascadeType.NoCascade,
                Unshare = CascadeType.NoCascade
            }
        },
        Lookup = new LookupAttributeMetadata
        {
            SchemaName = "new_parent_accountid",
            DisplayName = new Label("Account Lookup", 1033),
            RequiredLevel = new AttributeRequiredLevelManagedProperty(AttributeRequiredLevel.None),
            Description = new Label("Sample Lookup", 1033)
        }
    };


    CreateOneToManyResponse createOneToManyRelationshipResponse =
        (CreateOneToManyResponse)_serviceProxy.Execute(
        createOneToManyRelationshipRequest);

    _oneToManyRelationshipId =
        createOneToManyRelationshipResponse.RelationshipId;
    _oneToManyRelationshipName = 
        createOneToManyRelationshipRequest.OneToManyRelationship.SchemaName;

    Console.WriteLine(
        "The one-to-many relationship has been created between {0} and {1}.",
        "account", "campaign");
}
```
  
<a name="BKMK_EligibleCreateOneToManyRelationship"></a>   

### <a name="eligiblecreateonetomanyrelationship"></a>EligibleCreateOneToManyRelationship  

 次のサンプルでは、<xref:Microsoft.Xrm.Sdk.Messages.CanBeReferencedRequest> および <xref:Microsoft.Xrm.Sdk.Messages.CanBeReferencingRequest>  を使用する `EligibleCreateOneToManyRelationship` メソッドを作成して、2 つのエンティティが 1:N のエンティティ関連付けに参加できるかどうかを確認します。  
  
```csharp
/// <summary>
/// Determines whether two entities are eligible to participate in a relationship
/// </summary>
/// <param name="referencedEntity">Primary Entity</param>
/// <param name="referencingEntity">Referencing Entity</param>
/// <returns></returns>
public bool EligibleCreateOneToManyRelationship(string referencedEntity, 
    string referencingEntity)
{
    //Checks whether the specified entity can be the primary entity in one-to-many
    //relationship.
    CanBeReferencedRequest canBeReferencedRequest = new CanBeReferencedRequest
    {
        EntityName = referencedEntity
    };

    CanBeReferencedResponse canBeReferencedResponse =
        (CanBeReferencedResponse)_serviceProxy.Execute(canBeReferencedRequest);

    if (!canBeReferencedResponse.CanBeReferenced)
    {
        Console.WriteLine(
            "Entity {0} can't be the primary entity in this one-to-many relationship", 
            referencedEntity);
    }

    //Checks whether the specified entity can be the referencing entity in one-to-many
    //relationship.
    CanBeReferencingRequest canBereferencingRequest = new CanBeReferencingRequest
    {
        EntityName = referencingEntity
    };

    CanBeReferencingResponse canBeReferencingResponse =
        (CanBeReferencingResponse)_serviceProxy.Execute(canBereferencingRequest);

    if (!canBeReferencingResponse.CanBeReferencing)
    {
        Console.WriteLine(
            "Entity {0} can't be the referencing entity in this one-to-many relationship", 
            referencingEntity);
    }


    if (canBeReferencedResponse.CanBeReferenced == true
        && canBeReferencingResponse.CanBeReferencing == true)
    {
        return true;
    }
    else
    {
        return false;
    }
}
```
  
<a name="BKMK_CreateNNEntityRelationship"></a>   

## <a name="create-an-nn-entity-relationship"></a>N:N のエンティティ関連付けの作成  

 次のサンプルでは、[EligibleCreateManyToManyRelationship](#BKMK_EligibleCreateManyToManyRelationship) メソッドを使用して、`Account` および `Campaign` エンティティが N:N のエンティティ関連付けに参加できることを確認し、<xref:Microsoft.Xrm.Sdk.Messages.CreateManyToManyRequest> を使用してエンティティ関連付けを作成します。  
  
```csharp
bool accountEligibleParticipate =
    EligibleCreateManyToManyRelationship("account");
bool campaignEligibleParticipate =
    EligibleCreateManyToManyRelationship("campaign");

if (accountEligibleParticipate && campaignEligibleParticipate)
{

    CreateManyToManyRequest createManyToManyRelationshipRequest =
        new CreateManyToManyRequest
    {
        IntersectEntitySchemaName = "new_accounts_campaigns",
        ManyToManyRelationship = new ManyToManyRelationshipMetadata
        {
            SchemaName = "new_accounts_campaigns",
            Entity1LogicalName = "account",
            Entity1AssociatedMenuConfiguration =
            new AssociatedMenuConfiguration
            {
                Behavior = AssociatedMenuBehavior.UseLabel,
                Group = AssociatedMenuGroup.Details,
                Label = new Label("Account", 1033),
                Order = 10000
            },
            Entity2LogicalName = "campaign",
            Entity2AssociatedMenuConfiguration =
            new AssociatedMenuConfiguration
            {
                Behavior = AssociatedMenuBehavior.UseLabel,
                Group = AssociatedMenuGroup.Details,
                Label = new Label("Campaign", 1033),
                Order = 10000
            }
        }
    };

    CreateManyToManyResponse createManytoManyRelationshipResponse =
        (CreateManyToManyResponse)_serviceProxy.Execute(
        createManyToManyRelationshipRequest);


    _manyToManyRelationshipId =
        createManytoManyRelationshipResponse.ManyToManyRelationshipId;
    _manyToManyRelationshipName =
        createManyToManyRelationshipRequest.ManyToManyRelationship.SchemaName;

    Console.WriteLine(
        "The many-to-many relationship has been created between {0} and {1}.",
        "account", "campaign");
}
```
  
<a name="BKMK_EligibleCreateManyToManyRelationship"></a>   

### <a name="eligiblecreatemanytomanyrelationship"></a>EligibleCreateManyToManyRelationship  

 次のサンプルでは、<xref:Microsoft.Xrm.Sdk.Messages.CanManyToManyRequest> を使用する `EligibleCreateManyToManyRelationship` メソッドを作成して、任意のエンティティが N:N のエンティティ関連付けに参加できるかどうかを確認します。  
  
```csharp
/// <summary>
/// Determines whether the entity can participate in a many-to-many relationship.
/// </summary>
/// <param name="entity">Entity</param>
/// <returns></returns>
public bool EligibleCreateManyToManyRelationship(string entity)
{
    CanManyToManyRequest canManyToManyRequest = new CanManyToManyRequest
    {
        EntityName = entity
    };

    CanManyToManyResponse canManyToManyResponse =
        (CanManyToManyResponse)_serviceProxy.Execute(canManyToManyRequest);

    if (!canManyToManyResponse.CanManyToMany)
    {
        Console.WriteLine(
            "Entity {0} can't participate in a many-to-many relationship.", 
            entity);
    }

    return canManyToManyResponse.CanManyToMany;
}
```
  
<a name="BKMK_RetrieveEntityRelationships"></a>   
## <a name="retrieve-entity-relationships"></a>エンティティの関連付けの取得  
 次のサンプルでは、<xref:Microsoft.Xrm.Sdk.Messages.RetrieveRelationshipRequest> を使用して前に作成した 2 つのエンティティ関連付けを取得します。 最初の例では `MetadataId` を使用し、2 番目の例では `Name` を使用します。  
  
```csharp
//You can use either the Name or the MetadataId of the relationship.

//Retrieve the One-to-many relationship using the MetadataId.
RetrieveRelationshipRequest retrieveOneToManyRequest =
    new RetrieveRelationshipRequest { MetadataId = _oneToManyRelationshipId };
RetrieveRelationshipResponse retrieveOneToManyResponse =
    (RetrieveRelationshipResponse)_serviceProxy.Execute(retrieveOneToManyRequest);

Console.WriteLine("Retrieved {0} One-to-many relationship by id", retrieveOneToManyResponse.RelationshipMetadata.SchemaName);

//Retrieve the Many-to-many relationship using the Name.
RetrieveRelationshipRequest retrieveManyToManyRequest =
    new RetrieveRelationshipRequest { Name = _manyToManyRelationshipName};
RetrieveRelationshipResponse retrieveManyToManyResponse =
    (RetrieveRelationshipResponse)_serviceProxy.Execute(retrieveManyToManyRequest);

Console.WriteLine("Retrieved {0} Many-to-Many relationship by Name", retrieveManyToManyResponse.RelationshipMetadata.MetadataId);
```
  
### <a name="see-also"></a>関連項目  
 
 [エンティティの関連付けのメタデータ メッセージ](../entity-relationship-metadata-messages.md)   
