---
title: QueryByAttribute クラスの使用 (Common Data Service) | Microsoft Docs
description: QueryByAttribute クラスを使用して、一意の値に対して一意の属性をテストするクエリを作成できます。
ms.custom: ''
ms.date: 05/03/2019
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

# <a name="use-the-querybyattribute-class"></a>QueryByAttribute クラスの使用

<xref:Microsoft.Xrm.Sdk.Query.QueryByAttribute> クラスを使用して、一群の値に対して一群の属性をテストするクエリを作成できます。 このクラスは <xref:Microsoft.Xrm.Sdk.IOrganizationService.RetrieveMultiple*> メソッドまたは <xref:Microsoft.Xrm.Sdk.IOrganizationService>です。<xref:Microsoft.Xrm.Sdk.Messages.RetrieveMultipleRequest>  メソッドと共に使用します。
  
 <xref:Microsoft.Xrm.Sdk.Query.QueryByAttribute> クラスを使用してクエリ式を作成するために設定できるプロパティを次の表に示します。  
  
|プロパティ|説明|  
|--------------|-----------------|  
|<xref:Microsoft.Xrm.Sdk.Query.QueryByAttribute.EntityName>|取得するエンティティの種類を指定します。 クエリ式では、1 種類のエンティティのコレクションのみ取得できます。 <xref:Microsoft.Xrm.Sdk.Query.QueryExpression> コンストラクターを使用して、この値を渡すこともできます。|  
|<xref:Microsoft.Xrm.Sdk.Query.QueryByAttribute.ColumnSet>|取得する一連の属性 (列) を指定します。|  
|<xref:Microsoft.Xrm.Sdk.Query.QueryByAttribute.Attributes>|クエリ内で選択された一群の属性を指定します。|  
|<xref:Microsoft.Xrm.Sdk.Query.QueryByAttribute.Values>|クエリの実行時に検索する属性値を指定します。|  
|<xref:Microsoft.Xrm.Sdk.Query.QueryByAttribute.Orders>|クエリでレコードを返す順序を指定します。|  
|<xref:Microsoft.Xrm.Sdk.Query.QueryByAttribute.PageInfo>|クエリで返されるページ数、およびページごとのレコード数を指定します。|  
  
 次のコード例は、`QueryByAttribute` クラスの使用方法を示しています。  
  
```csharp  
//  Create query using querybyattribute      
QueryByAttribute querybyexpression = new QueryByAttribute("account");      
querybyexpression.ColumnSet = new ColumnSet("name", "address1_city", "emailaddress1");  
  
//  Attribute to query      
querybyexpression.Attributes.AddRange("address1_city");  
  
//  Value of queried attribute to return      
querybyexpression.Values.AddRange("Detroit");      
  
//  Query passed to the service proxy      
EntityCollection retrieved = _serviceProxy.RetrieveMultiple(querybyexpression);     
  
//  Iterate through returned collection      
foreach (var c in retrieved.Entities)      
{  
      System.Console.WriteLine("Name: " + c.Attributes["name"]);  
      System.Console.WriteLine("Address: " + c.Attributes["address1_city"]);        
      System.Console.WriteLine("E-mail: " + c.Attributes["emailaddress1"]);      
}  
  
```  
  
### <a name="see-also"></a>関連項目  
 [QueryExpression でクエリを作成する](build-queries-with-queryexpression.md)   
 <xref:Microsoft.Xrm.Sdk.Query.QueryByAttribute>