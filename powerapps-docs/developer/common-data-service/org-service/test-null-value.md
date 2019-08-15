---
title: null 値向けのテスト (Common Data Service)| Microsoft Docs
description: このサンプルは、FilterExpression クラスおよび QueryByAttribute クラスを使用して NULL 値をテストする方法を示しています。
ms.custom: ''
ms.date: 05/03/2019
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---

# <a name="test-for-a-null-value"></a>null 値のテスト

次のコード例は、<xref:Microsoft.Xrm.Sdk.Query.FilterExpression> クラスおよび <xref:Microsoft.Xrm.Sdk.Query.QueryByAttribute> クラスを使用して null 値をテストする方法を示しています。  
  
## <a name="example"></a>例  
 このコードは、<xref:Microsoft.Xrm.Sdk.Query.FilterExpression> クラスを使用して等値であるかどうかをテストする場合に使用します。  
  
```csharp  
FilterExpression null_filter = new FilterExpression(LogicalOperator.And);   
null_filter.FilterOperator = LogicalOperator.And;   
null_filter.AddCondition("leadid", ConditionOperator.Null);  
  
```  
  
## <a name="example"></a>例  
 このコードは、<xref:Microsoft.Xrm.Sdk.Query.FilterExpression> クラスを使用して非等値であるかどうかをテストする場合に使用します。  
  
```csharp  
  
FilterExpression filter = new FilterExpression(LogicalOperator.And);   
filter.FilterOperator = LogicalOperator.And;   
filter.AddCondition("leadid", ConditionOperator.NotNull);  
```  
  
## <a name="example"></a>例  
 このコードは、<xref:Microsoft.Xrm.Sdk.Query.QueryByAttribute> クラスを使用して等値であるかどうかをテストする場合に使用します。  
  
```csharp  
  
QueryByAttribute qba = new QueryByAttribute("account");   
qba.ColumnSet = new ColumnSet("name","address1_stateorprovince");   
qba.AddAttributeValue("donotfax", null);  
```  
  
### <a name="see-also"></a>関連項目  
 [QueryExpression でクエリを作成する](build-queries-with-queryexpression.md)   
 [FetchXML による大量の結果セットのページング](page-large-result-sets-with-fetchxml.md)
