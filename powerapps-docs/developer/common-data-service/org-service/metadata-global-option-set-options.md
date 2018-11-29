---
title: グローバル オプション セットのオプション (アプリ用 Common Data Service) を挿入、更新、削除、注文する | Microsoft Docs
description: グローバル オプション セットのオプションの挿入、更新、削除、および並べ替えの方法を示すコード サンプル
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
# <a name="insert-update-delete-and-order-global-option-set-options"></a>グローバル オプション セットのオプションの挿入、更新、削除、および並べ替え

<!-- 

https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/org-service/insert-update-delete-order-global-option-set-options 

-->

次のコード サンプルに、グローバル オプション セットのオプションの挿入、更新、削除、および並べ替えの方法を示します。  
  
<a name="BKMK_InsertNewOption"></a>   
## <a name="insert-a-new-option"></a>新しいオプションの挿入  
 次のサンプルに、<xref:Microsoft.Xrm.Sdk.Messages.InsertOptionValueRequest> を使用してグローバル オプション セットに新しいオプションを追加する方法を示します。  
  
```csharp
// Use InsertOptionValueRequest to insert a new option into a 
// global option set.
InsertOptionValueRequest insertOptionValueRequest =
    new InsertOptionValueRequest
    {
        OptionSetName = _globalOptionSetName,
        Label = new Label("New Picklist Label", _languageCode)
    };

// Execute the request and store the newly inserted option value 
// for cleanup, used in the later part of this sample.
_insertedOptionValue = ((InsertOptionValueResponse)_serviceProxy.Execute(
    insertOptionValueRequest)).NewOptionValue;

//Publish the OptionSet
PublishXmlRequest pxReq2 = new PublishXmlRequest { ParameterXml = String.Format("<importexportxml><optionsets><optionset>{0}</optionset></optionsets></importexportxml>", _globalOptionSetName) };
_serviceProxy.Execute(pxReq2);
```


  
<a name="BKMK_UpdateAnOption"></a>   
## <a name="update-an-option"></a>オプションの更新  
 次のサンプルに、<xref:Microsoft.Xrm.Sdk.Messages.UpdateOptionValueRequest> を使用してグローバル オプション セットのオプションを更新する方法を示します。  
  
```csharp
// In order to change labels on option set values (or delete) option set
// values, you must use UpdateOptionValueRequest 
// (or DeleteOptionValueRequest).
UpdateOptionValueRequest updateOptionValueRequest =
    new UpdateOptionValueRequest
    {
        OptionSetName = _globalOptionSetName,
        // Update the second option value.
        Value = optionList[1].Value.Value,
        Label = new Label("Updated Option 1", _languageCode)
    };

_serviceProxy.Execute(updateOptionValueRequest);

//Publish the OptionSet
PublishXmlRequest pxReq3 = new PublishXmlRequest { ParameterXml = String.Format("<importexportxml><optionsets><optionset>{0}</optionset></optionsets></importexportxml>", _globalOptionSetName) };
_serviceProxy.Execute(pxReq3);
```
  
<a name="BKMK_DeleteAnOption"></a>   
## <a name="delete-an-option"></a>オプションの削除  
 次のサンプルに、<xref:Microsoft.Xrm.Sdk.Messages.DeleteOptionValueRequest> を使用してグローバル オプション セットのオプションを削除する方法を示します。  
  
```csharp
// Use the DeleteOptionValueRequest message 
// to remove the newly inserted label.
DeleteOptionValueRequest deleteOptionValueRequest =
    new DeleteOptionValueRequest
{
    OptionSetName = _globalOptionSetName,
    Value = _insertedOptionValue
};

// Execute the request.
_serviceProxy.Execute(deleteOptionValueRequest);
```  
  
<a name="BKMK_OrderOptions"></a>   
## <a name="order-options"></a>オプションの並べ替え  
 次のサンプルに、<xref:Microsoft.Xrm.Sdk.Messages.OrderOptionRequest> を使用してグローバル オプション セットのオプションの順序を設定する方法を示します。  
  
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
_serviceProxy.Execute(orderOptionRequest);

//Publish the OptionSet
PublishXmlRequest pxReq4 = new PublishXmlRequest { ParameterXml = String.Format("<importexportxml><optionsets><optionset>{0}</optionset></optionsets></importexportxml>", _globalOptionSetName) };
_serviceProxy.Execute(pxReq4);
``` 
