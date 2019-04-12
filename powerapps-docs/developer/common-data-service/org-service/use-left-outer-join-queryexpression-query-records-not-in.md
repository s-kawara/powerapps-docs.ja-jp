---
title: QueryExpression の左外部結合を &quot;not in&quot; レコードのクエリに使用する (Common Data Service) | Microsoft Docs
description: 左外部結合を QueryExpression クラスで使用して、結合の表をフィルタリングするクエリを実行して、セットに &quot;存在しない&quot; 記録を探すクエリを作成する方法について説明します
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
# <a name="use-a-left-outer-join-in-queryexpression-to-query-for-records-not-in"></a>左外部結合を QueryExpression で使用して "存在しない" 記録をクエリする

<xref:Microsoft.Crm.Sdk.Messages.SearchByKeywordsKbArticleRequest.QueryExpression> クラスの使用して、左外部結合を使用し、結合の表をフィルタリングするクエリを実行します。たとえば、過去 2 か月間のキャンペーン活動がない、取引先担当者をすべて検索できます。 このクエリタイプの別のよくある使用法では、次のような場合には存在しないといった、あるセットには存在しないレコードを検索するクエリです。  
  
- タスクのないすべての潜在顧客を検索する  
  
- 取引先担当者のないすべての取引先企業を検索する  
  
- 1つか、2つのタスクがあるすべての潜在顧客を検索する  
  
  左外部結合では、2 番め入力で最初の入力の結合を満たす各列を返します。 また、2 番目入力で一致する列がない最初の入力列を返します。 2 番めの一致しない列が null 値として返されます。  
  
  条件演算子として `entityname` 属性を使用して、`QueryExpression` で左外部結合を実行できます。 `entityname` 属性は、条件、フィルターおよび入れ子フィルターで有効です。  
  
## <a name="find-all-leads-that-have-no-tasks-using-an-alias"></a>エイリアス名を使用して、タスクのないすべての潜在顧客を検索する  

次の例は、このクエリの作成方法を示しています。  
  
```csharp
QueryExpression qx = new QueryExpression("lead");  
qx.ColumnSet.AddColumn("subject");  
  
LinkEntity link = qx.AddLink("task", "leadid", "regardingobjectid", JoinOperator.LeftOuter);  
link.Columns.AddColumn("subject");  
link.EntityAlias = "tsk";  
  
qx.Criteria = new FilterExpression();  
qx.Criteria.AddCondition("tsk", "activityid", ConditionOperator.Null);
```  
  
これは次のSQLと等価です。  
  
```sql
SELECT lead.FullName  
FROM Leads as lead  
LEFT OUTER JOIN Tasks as ab  
ON (lead.leadId  =  ab.RegardingObjectId)  
WHERE ab.RegardingObjectId is null
```  
  
### <a name="see-also"></a>関連項目  
 [QueryExpression でクエリを作成する](build-queries-with-queryexpression.md)   
 [NULL 値のテスト](/dynamics365/customer-engagement/developer/test-null-value)   
 [QueryExpression クラスの使用](use-queryexpression-class.md)   
 [QueryByAttribute クラスの使用](use-querybyattribute-class.md)