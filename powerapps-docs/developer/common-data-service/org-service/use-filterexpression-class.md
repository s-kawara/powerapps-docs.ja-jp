---
title: FilterExpression クラスの使用 (Common Data Service) | Microsoft Docs
description: FilterExpression クラスを使用して、複数の条件を表すクエリを作成する方法について説明します。
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
# <a name="use-the-filterexpression-class"></a>FilterExpression クラスの使用

Common Data Service では <xref:Microsoft.Xrm.Sdk.Query.FilterExpression> クラスを使用して、複数の条件を表すクエリをビルドできます。 たとえば、`([FirstName] = 'Joe' OR [FirstName] = 'John') AND [City] = 'Redmond'` のような SQL ステートメントと同等のクエリ式を作成できます。  
  
 次の表では、<xref:Microsoft.Xrm.Sdk.Query.FilterExpression> クラスのプロパティを示します。  
  
|||  
|-|-|  
|プロパティ|説明|  
|<xref:Microsoft.Xrm.Sdk.Query.FilterExpression.Conditions>|属性、条件演算子、および属性値を含む条件式を取得または設定します。|  
|<xref:Microsoft.Xrm.Sdk.Query.FilterExpression.FilterOperator>|論理 `AND/OR` フィルター演算子を取得または設定します。 これは、<xref:Microsoft.Xrm.Sdk.Query.LogicalOperator> 列挙体を使用して設定します。|  
|<xref:Microsoft.Xrm.Sdk.Query.FilterExpression.Filters>|クエリの結果をフィルターする条件式および論理フィルター式の階層を取得または設定します。|  
|<xref:Microsoft.Xrm.Sdk.Query.FilterExpression.IsQuickFindFilter>|式が簡易検索クエリの一部であるかどうかを示す値を取得または設定します。|  
  
 <xref:Microsoft.Xrm.Sdk.Query.FilterExpression> クラスには、クエリの作成が簡単になる複数のヘルパー メソッドも含まれます。 <xref:Microsoft.Xrm.Sdk.Query.FilterExpression>.<xref:Microsoft.Xrm.Sdk.Query.ConditionExpression> メソッドを使用すると <xref:Microsoft.Xrm.Sdk.Query.ConditionExpression> が <xref:Microsoft.Xrm.Sdk.Query.FilterExpression> の <xref:Microsoft.Xrm.Sdk.Query.FilterExpression.Conditions> プロパティに追加され、条件式の作成に必要なコードが減ります。 <xref:Microsoft.Xrm.Sdk.Query.FilterExpression.AddFilter*>.<xref:Microsoft.Xrm.Sdk.Query.LogicalOperator> メソッドは、新しいフィルターを <xref:Microsoft.Xrm.Sdk.Query.FilterExpression> クラスの <xref:Microsoft.Xrm.Sdk.Query.FilterExpression.Filters> プロパティに追加します。  
  
<a name="example"></a>   

## <a name="filter-expression-example"></a>フィルター式の例  

 次のコード例は、<xref:Microsoft.Xrm.Sdk.Query.FilterExpression> クラスの使用方法を示しています。  
  
```csharp  
QueryExpression query = new QueryExpression("contact");   
query.ColumnSet.AddColumns("firstname", "lastname", "address1_city");   
  
query.Criteria = new FilterExpression();   
query.Criteria.AddCondition("address1_city", ConditionOperator.Equal, "Redmond");   
  
FilterExpression childFilter = query.Criteria.AddFilter(LogicalOperator.Or);   
childFilter.AddCondition("lastname", ConditionOperator.Equal, "Tharpe");   
childFilter.AddCondition("lastname", ConditionOperator.Equal, "Brown");   
  
// Pass query to service proxy   
EntityCollection results = _serviceProxy.RetrieveMultiple(query);   
Console.WriteLine();   
Console.WriteLine("Query using QE with multiple conditions and filters");   
Console.WriteLine("---------------------------------------");   
  
// Print results   
foreach (var a in results.Entities)   
{   
Console.WriteLine("Name: {0} {1}", a.GetAttributeValue<string>("firstname"), a.GetAttributeValue<string>("lastname"));   
Console.WriteLine("City: {0}", a.GetAttributeValue<string>("address1_city"));   
}   
Console.WriteLine("---------------------------------------");  
```  
  
<a name="quickfindfilter"></a> 
  
## <a name="about-the-isquickfindfilter-property"></a>IsQuickFindFilter プロパティについて  

 <xref:Microsoft.Xrm.Sdk.Query.FilterExpression>.<xref:Microsoft.Xrm.Sdk.Query.FilterExpression.IsQuickFindFilter> プロパティを使用することができます。これは Fetch XML の `filter` ノードにある `isquickfindfields` 属性に似ています。 Fetch クエリを保存すると、そのクエリは `SavedQuery` および `UserQuery` エンティティの `IsQuickFind` プロパティに保存されます。 <xref:Microsoft.Xrm.Sdk.Query.FilterExpression.IsQuickFindFilter> プロパティは、クエリ式と Fetch XML クエリとの間に一貫性があるように追加されました。  
  
 <xref:Microsoft.Xrm.Sdk.Query.FilterExpression.IsQuickFindFilter> プロパティには次のルールが適用されます。  
  
-   このフィールドを `true` に設定できるのは、論理演算子の種類が <xref:Microsoft.Xrm.Sdk.Query.LogicalOperator>.`Or` のフィルター式に対してのみです。 論理演算子の種類が <xref:Microsoft.Xrm.Sdk.Query.LogicalOperator>.`And` のフィルター式に対して設定しても、<xref:Microsoft.Xrm.Sdk.Query.FilterExpression.IsQuickFindFilter> プロパティは無視されます。  
  
-   フィルター式階層内の 1 つのフィルター式に対してのみ、<xref:Microsoft.Xrm.Sdk.Query.FilterExpression.IsQuickFindFilter> = **true** を設定できます。 複数のフィルター式が見つかった場合は、例外がスローされます。  
  
-   フィルター式で <xref:Microsoft.Xrm.Sdk.Query.FilterExpression.IsQuickFindFilter> を **true** に設定している場合、子フィルター式のプロパティを追加することはできません。追加できるのは <xref:Microsoft.Xrm.Sdk.Query.ConditionExpression> のプロパティのみです。 子フィルター式を追加した場合は、例外がスローされます。  
  
-   <xref:Microsoft.Xrm.Sdk.Query.FilterExpression.IsQuickFindFilter> を **true** に設定しているフィルター式に関連するすべての条件式は、null 以外の 1 つの値を返す条件式であることが必要です。 つまり、条件式は属性、演算子、および値で構成されていて、その条件式の value プロパティの値が **null** 以外の 1 つの値であることが必要です。 さらに、これらの条件式でサポートされる条件演算子は、null 以外の 1 つの値を返す演算子のみです。 **null** 値または複数の値が検出された場合は、例外がスローされます。  
  
### <a name="see-also"></a>関連項目  

 [QueryExpression でクエリを作成する](build-queries-with-queryexpression.md)   
 [左外部結合を QueryExpression で使用して "存在しない" 記録をクエリする](use-left-outer-join-queryexpression-query-records-not-in.md)   
 [ConditionExpression クラスの使用](use-conditionexpression-class.md)   
 <xref:Microsoft.Xrm.Sdk.Query.FilterExpression>