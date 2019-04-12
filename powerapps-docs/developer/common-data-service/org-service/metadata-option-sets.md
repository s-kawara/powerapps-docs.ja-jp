---
title: オプション セットのカスタマイズ (Common Data Service) | Microsoft Docs
description: コード内でグロバールおよびローカル オプション セットを操作する方法について説明します。
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
# <a name="customize-option-sets"></a>オプション セットのカスタマイズ

通常、*グローバル* オプション セットでフィールドを設定するのは、さまざまなフィールドを同じオプション セットで共有して、それらを 1 つの場所でメンテナンスできるようにするためです。 特定の属性に対してのみ定義される*ローカル* オプション セットとは異なり、グローバル オプション セットは再利用できます。 要求パラメーターの中で列挙体のときと同じように使われる例もあります。  
  
<xref:Microsoft.Xrm.Sdk.Messages.CreateOptionSetRequest> でグローバル オプション セットを設定するときは、値の設定をシステムに任せることをお勧めします。 具体的には新規の `OptionMetadata` インスタンスを作成するとき、引数として **null** 値を渡します。 オプションを変更すると、そのオプション セットが作成されたソリューションに設定されている発行者のコンテキストに固有の接頭辞がオプション値に含められます。 この接頭辞は、マネージド ソリューションや、マネージド ソリューションのインストール先の組織で定義されている任意のオプション セットの中で、オプション セットの重複が生じる可能性を減らす効果があります。 詳細については、[オプション セット オプションのマージ](../understand-managed-solutions-merged.md#merge-option-set-options) を参照してください。  
 
## <a name="messages-request-classes"></a>メッセージ要求クラス  

次のメッセージ要求クラスを使って、グローバル オプション セットを操作します。

- <xref:Microsoft.Xrm.Sdk.Messages.CreateOptionSetRequest>
- <xref:Microsoft.Xrm.Sdk.Messages.DeleteOptionSetRequest>
- <xref:Microsoft.Xrm.Sdk.Messages.RetrieveAllOptionSetsRequest>
- <xref:Microsoft.Xrm.Sdk.Messages.RetrieveOptionSetRequest>  
- <xref:Microsoft.Xrm.Sdk.Messages.UpdateOptionSetRequest> 

次のメッセージ要求クラスを使って、グローバル オプション セットとローカル オプション セットを操作します。

- <xref:Microsoft.Xrm.Sdk.Messages.DeleteOptionValueRequest>
- <xref:Microsoft.Xrm.Sdk.Messages.InsertOptionValueRequest>
- <xref:Microsoft.Xrm.Sdk.Messages.InsertStatusValueRequest>
- <xref:Microsoft.Xrm.Sdk.Messages.OrderOptionRequest>
- <xref:Microsoft.Xrm.Sdk.Messages.UpdateOptionValueRequest>
- <xref:Microsoft.Xrm.Sdk.Messages.UpdateStateValueRequest>  

<a name="BKMK_RetrieveAGlobalOptionSet"></a>

## <a name="retrieve-a-global-option-set"></a>グローバル オプション セットの取得  

 次のサンプルは、<xref:Microsoft.Xrm.Sdk.Messages.RetrieveOptionSetRequest> メッセージを使用して名前でグローバル オプション セットを取得する方法を示します。  
  

```csharp
// Use the RetrieveOptionSetRequest message to retrieve  
// a global option set by it's name.
RetrieveOptionSetRequest retrieveOptionSetRequest =
    new RetrieveOptionSetRequest
    {
        Name = _globalOptionSetName
    };

// Execute the request.
RetrieveOptionSetResponse retrieveOptionSetResponse =
    (RetrieveOptionSetResponse)svc.Execute(
    retrieveOptionSetRequest);

Console.WriteLine("Retrieved {0}.",
    retrieveOptionSetRequest.Name);

// Access the retrieved OptionSetMetadata.
OptionSetMetadata retrievedOptionSetMetadata =
    (OptionSetMetadata)retrieveOptionSetResponse.OptionSetMetadata;

// Get the current options list for the retrieved attribute.
OptionMetadata[] optionList =
    retrievedOptionSetMetadata.Options.ToArray();
```

  
<a name="BKMK_CreateGlobalOptionSet"></a>  
 
## <a name="create-a-global-option-set"></a>グローバル オプション セットの作成
  
<xref:Microsoft.Xrm.Sdk.Messages.CreateOptionSetRequest> メッセージを使用して、新しいグローバル オプション セットを作成します。 <xref:Microsoft.Xrm.Sdk.Metadata.OptionSetMetadataBase.IsGlobal> プロパティを `true` に設定して、オプションがグローバルであることを示します。 次のコード例では、"Example Option Set" というグローバル オプション セットを作成します。  
  
```csharp
// Define the request object and pass to the service.
CreateOptionSetRequest createOptionSetRequest = new CreateOptionSetRequest
{
    // Create a global option set (OptionSetMetadata).
    OptionSet = new OptionSetMetadata
    {
        Name = _globalOptionSetName,
        DisplayName = new Label("Example Option Set", _languageCode),
        IsGlobal = true,
        OptionSetType = OptionSetType.Picklist,
        Options = 
    {
        new OptionMetadata(new Label("Open", _languageCode), null),
        new OptionMetadata(new Label("Suspended", _languageCode), null),
        new OptionMetadata(new Label("Cancelled", _languageCode), null),
        new OptionMetadata(new Label("Closed", _languageCode), null)
    }
    }
};

// Execute the request.
CreateOptionSetResponse optionsResp =
    (CreateOptionSetResponse)svc.Execute(createOptionSetRequest);
```

  
<a name="BKMK_CreatePicklistWithGlobalOptionSet"></a>  
 
## <a name="create-a-picklist-that-uses-a-global-option-set"></a>グローバル オプション セットを使用する候補リストの作成  

 次のサンプルは、グローバル オプション セットを使用する候補リスト属性を <xref:Microsoft.Xrm.Sdk.Messages.CreateAttributeRequest> で作成する方法を示します。  
  

```csharp
// Create a Picklist linked to the option set.
// Specify which entity will own the picklist, and create it.
CreateAttributeRequest createRequest = new CreateAttributeRequest
{
    EntityName = Contact.EntityLogicalName,
    Attribute = new PicklistAttributeMetadata
    {
        SchemaName = "sample_examplepicklist",
        LogicalName = "sample_examplepicklist",
        DisplayName = new Label("Example Picklist", _languageCode),
        RequiredLevel = new AttributeRequiredLevelManagedProperty(AttributeRequiredLevel.None),

        // In order to relate the picklist to the global option set, be sure
        // to specify the two attributes below appropriately.
        // Failing to do so will lead to errors.
        OptionSet = new OptionSetMetadata
        {
            IsGlobal = true,
            Name = _globalOptionSetName
        }
    }
};

svc.Execute(createRequest);
```

  
<a name="BKMK_UpdateGlobalOptionSet"></a>

## <a name="update-a-global-option-set"></a>グローバル オプション セットの更新 

次のサンプルは、<xref:Microsoft.Xrm.Sdk.Messages.UpdateOptionSetRequest> メッセージを使用してグローバル オプション セットのラベルを更新する方法を示します。  
  

```csharp
// Use UpdateOptionSetRequest to update the basic information of an option
// set. Updating option set values requires different messages (see below).
UpdateOptionSetRequest updateOptionSetRequest = new UpdateOptionSetRequest
{
    OptionSet = new OptionSetMetadata
    {
        DisplayName = new Label("Updated Option Set", _languageCode),
        Name = _globalOptionSetName,
        IsGlobal = true
    }
};

svc.Execute(updateOptionSetRequest);

//Publish the OptionSet
PublishXmlRequest pxReq1 = new PublishXmlRequest { ParameterXml = String.Format("<importexportxml><optionsets><optionset>{0}</optionset></optionsets></importexportxml>", _globalOptionSetName) };
svc.Execute(pxReq1);
```

  
<a name="BKMK_OrderingOptions"></a> 
  
## <a name="ordering-options"></a>オプションの順序設定  

次のサンプルは、<xref:Microsoft.Xrm.Sdk.Messages.OrderOptionRequest> でグローバル オプション セットの順序を設定する方法を示します。  
  

```csharp
// Change the order of the original option's list.
// Use the OrderBy (OrderByDescending) linq function to sort options in  
// ascending (descending) order according to label text.
// For ascending order use this:
var updateOptionList =
    optionList.OrderBy(x => x.Label.LocalizedLabels[0].Label).ToList();

// For descending order use this:
// var updateOptionList =
//      optionList.OrderByDescending(
//      x => x.Label.LocalizedLabels[0].Label).ToList();

// Create the request.
OrderOptionRequest orderOptionRequest = new OrderOptionRequest
{
    // Set the properties for the request.
    OptionSetName = _globalOptionSetName,
    // Set the changed order using Select linq function 
    // to get only values in an array from the changed option list.
    Values = updateOptionList.Select(x => x.Value.Value).ToArray()
};

// Execute the request
svc.Execute(orderOptionRequest);

//Publish the OptionSet
PublishXmlRequest pxReq4 = new PublishXmlRequest { 
ParameterXml = String.Format("<importexportxml><optionsets><optionset>{0}</optionset></optionsets></importexportxml>", _globalOptionSetName) 
};
svc.Execute(pxReq4);
```

  
<a name="BKMK_RetrieveAllGlobalOptionSets"></a>  
 
## <a name="retrieve-all-global-option-sets"></a>すべてのグローバル オプション セットの取得  

次のサンプルは、<xref:Microsoft.Xrm.Sdk.Messages.RetrieveAllOptionSetsRequest> を使用してすべてのグローバル オプション セットを取得する方法を示します。  
  

```csharp
// Use RetrieveAllOptionSetsRequest to retrieve all global option sets.
// Create the request.
RetrieveAllOptionSetsRequest retrieveAllOptionSetsRequest =
    new RetrieveAllOptionSetsRequest();

// Execute the request
RetrieveAllOptionSetsResponse retrieveAllOptionSetsResponse =
    (RetrieveAllOptionSetsResponse)svc.Execute(
    retrieveAllOptionSetsRequest);

// Now you can use RetrieveAllOptionSetsResponse.OptionSetMetadata property to 
// work with all retrieved option sets.
if (retrieveAllOptionSetsResponse.OptionSetMetadata.Count() > 0)
{
    Console.WriteLine("All the global option sets retrieved as below:");
    int count = 1;
    foreach (OptionSetMetadataBase optionSetMetadata in
        retrieveAllOptionSetsResponse.OptionSetMetadata)
    {
        Console.WriteLine("{0} {1}", count++,
            (optionSetMetadata.DisplayName.LocalizedLabels.Count >0)? optionSetMetadata.DisplayName.LocalizedLabels[0].Label : String.Empty);
    }
}
```

  
<a name="BKMK_DeleteAGlobalOptionSet"></a>

## <a name="delete-a-global-option-set"></a>グローバル オプション セットの削除

 次のサンプルは、グローバル オプション セットが別のソリューション コンポーネントから削除されるかどうかを `RetrieveDependentComponents` メッセージ (<xref href="Microsoft.Dynamics.CRM.RetrieveDependentComponents?text=RetrieveDependentComponents Function" /> または <xref:Microsoft.Crm.Sdk.Messages.RetrieveDependentComponentsRequest>) で確認する方法と、それを `DeleteOptionSet` メッセージ (組織サービスでは、<xref:Microsoft.Xrm.Sdk.Messages.DeleteOptionSetRequest> を使用) で削除する方法を示します。  
  

```csharp
// Create the request to see which components have a dependency on the
// global option set.
RetrieveDependentComponentsRequest dependencyRequest =
    new RetrieveDependentComponentsRequest
    {
        ObjectId = _optionSetId,
        ComponentType = (int)componenttype.OptionSet
    };

RetrieveDependentComponentsResponse dependencyResponse =
    (RetrieveDependentComponentsResponse)svc.Execute(
    dependencyRequest);

// Here you would check the dependencyResponse.EntityCollection property
// and act as appropriate. However, we know there is exactly one 
// dependency so this example deals with it directly and deletes 
// the previously created attribute.
DeleteAttributeRequest deleteAttributeRequest =
    new DeleteAttributeRequest
{
    EntityLogicalName = Contact.EntityLogicalName,
    LogicalName = "sample_examplepicklist"
};

svc.Execute(deleteAttributeRequest);

Console.WriteLine("Referring attribute deleted.");
  
// Finally, delete the global option set. Attempting this before deleting
// the picklist above will result in an exception being thrown.
DeleteOptionSetRequest deleteRequest = new DeleteOptionSetRequest
{
    Name = _globalOptionSetName
};

svc.Execute(deleteRequest);
```

  
### <a name="see-also"></a>関連項目

[Web API を使用してオプション セットを作成および更新](../webapi/create-update-optionsets.md)