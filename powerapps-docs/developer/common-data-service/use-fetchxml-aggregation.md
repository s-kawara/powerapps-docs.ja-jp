---
title: FetchXML 集計の使用 (Common Data Service)| Microsoft Docs
description: FetchXML のグループ化と集計の機能について説明します。この機能を使用すると、合計、平均、最小値、最大値、および件数を計算できます。
ms.custom: ''
ms.date: 06/18/2019
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

# <a name="use-fetchxml-aggregation"></a>FetchXML 集計の使用

Common Data Service で、`FetchXML` にはグループ化および集計の機能が含まれています。この機能を使用すると、合計、平均、最小値、最大値、および件数を計算できます。  
  
 次の集計機能がサポートされています。  
  
- sum  
- avg  
- 分  
- max  
- count(*)  
- count(*属性名*)
  
<a name="Aggregation"></a>

## <a name="about-aggregation"></a>集計について
 
aggregate 属性を作成するには、`aggregate` キーワードを `true` に設定し、有効な*エンティティ名*、*属性名*、および*エイリアス* (変数名) を指定します。 また、実行する集計の種類を指定する必要があります。  
  
次の例は、`FetchXML` の簡単な aggregate 属性を示しています。  
  
```xml  
<fetch distinct='false' mapping='logical' aggregate='true'>   
   <entity name='entity name'>   
      <attribute name='attribute name' aggregate='count' alias='alias name'/>   
   </entity>   
</fetch>
```  
  
aggregate 属性を使用したクエリの結果は、標準のクエリの結果とは異なります。 エイリアスの値は、集計結果のタグ識別子として使用されます。  
  
次の例は、集計クエリの結果の形式を示しています。  
  
```xml
<resultset morerecords="0"'>   
   <result>  
      <alias>aggregate value</alias>  
   </result>  
</resultset>
```  
  
次の例は、alias 変数が `account_count` に設定された場合のクエリの結果を示しています。  
  
```xml
<resultset morerecords="0"'>   
   <result>  
      <account_count>20</account_count>  
   </result>  
</resultset>
```  

<a name="Limitations"></a>

## <a name="limitations"></a>制限

返される集計値が 50,000 レコードに限定されたクエリ。 この最大値で、システムの動作および信頼性を保持することができます。 クエリ内のフィルター条件に 50,000 を超えるレコードが含まれる場合は次のエラーが表示されます。

エラー コード: `-2147164125`<br />
16 進値のエラー コードです。`8004E023`<br />
プラットフォーム エラー メッセージ: `AggregateQueryRecordLimit exceeded. Cannot perform this operation.`<br />
クライアント エラー メッセージ: 最大レコード制限を超えています。 レコード数を減らしてください。<br />

このエラーを回避するには、適切なフィルターをクエリに追加して、50,000 超のレコードを評価する必要がないことを確認します。 その後、クエリを何度か実行して結果をまとめます。

> [!TIP]
> フィルターなしにレコードの総数を取得するには、Web API <xref href="Microsoft.Dynamics.CRM.RetrieveTotalRecordCount?text=RetrieveTotalRecordCount Function" /> または組織サービス <xref:Microsoft.Crm.Sdk.Messages.RetrieveTotalRecordCountRequest> メッセージ クラスを用いて `RetrieveTotalRecordCount` メッセージを使用します。
  
<a name="AVG"></a>

## <a name="avg"></a>Avg

 次の例は、`avg` `aggregate` 属性の使用方法を示しています。  
  
 ```csharp
// Fetch the average of estimatedvalue for all opportunities.  This is the equivalent of 
// SELECT AVG(estimatedvalue) AS estimatedvalue_avg ... in SQL.
string estimatedvalue_avg = @" 
<fetch distinct='false' mapping='logical' aggregate='true'> 
    <entity name='opportunity'> 
       <attribute name='estimatedvalue' alias='estimatedvalue_avg' aggregate='avg' /> 
    </entity> 
</fetch>";

EntityCollection estimatedvalue_avg_result = _serviceProxy.RetrieveMultiple(new FetchExpression(estimatedvalue_avg));

foreach (var c in estimatedvalue_avg_result.Entities)
{
    decimal aggregate1 = ((Money)((AliasedValue)c["estimatedvalue_avg"]).Value).Value;
    System.Console.WriteLine("Average estimated value: " + aggregate1);

}
```
  
### <a name="limitation-with-null-values-while-computing-average"></a>平均を計算する場合の NULL 値による制限

**Null** 値は、Common Data Service がデータ平均を計算する時は考慮されません。 ただし、ゼロ (0) は使用されます。  
  
次の例のデータの場合、取引先企業 1 (2 つのエントリ) の平均は 250 です。これに対し、取引先企業 2 (2 つのエントリ) の平均は 125 です。  
  
|トピック|見込み顧客|見込み値|  
|-----|------------------|---------------|  
|営業案件 1|取引先企業 1|null|  
|営業案件 2|取引先企業 1|250|  
|営業案件 3|取引先企業 2|0|  
|営業案件 4|取引先企業 2|250|  
  
<a name="count"></a>

## <a name="count"></a>件数

次の例は、`count` `aggregate` 属性の使用方法を示しています。  
  
 ```csharp
// *****************************************************************************************************************
//                FetchXML      opportunity_count   Aggregate 2
// *****************************************************************************************************************
// Fetch the count of all opportunities.  This is the equivalent of
// SELECT COUNT(*) AS opportunity_count ... in SQL.
string opportunity_count = @" 
<fetch distinct='false' mapping='logical' aggregate='true'> 
    <entity name='opportunity'> 
       <attribute name='name' alias='opportunity_count' aggregate='count'/> 
    </entity> 
</fetch>";

EntityCollection opportunity_count_result = _serviceProxy.RetrieveMultiple(new FetchExpression(opportunity_count));

foreach (var c in opportunity_count_result.Entities)
{
    Int32 aggregate2 = (Int32)((AliasedValue)c["opportunity_count"]).Value;
    System.Console.WriteLine("Count of all opportunities: " + aggregate2); 

}
```
  
<a name="count_column"></a>

### <a name="countcolumn"></a>CountColumn

次の例は、`countcolumn` `aggregate` 属性を使用して列をカウントする方法を示しています。  
  
 ```csharp
// *****************************************************************************************************************
//                FetchXML      opportunity_colcount   Aggregate 3
// *****************************************************************************************************************
// Fetch the count of all opportunities.  This is the equivalent of 
// SELECT COUNT(name) AS opportunity_count ... in SQL.
string opportunity_colcount = @" 
<fetch distinct='false' mapping='logical' aggregate='true'> 
    <entity name='opportunity'> 
       <attribute name='name' alias='opportunity_colcount' aggregate='countcolumn'/> 
    </entity> 
</fetch>";

EntityCollection opportunity_colcount_result = _serviceProxy.RetrieveMultiple(new FetchExpression(opportunity_colcount));

foreach (var c in opportunity_colcount_result.Entities)
{
    Int32 aggregate3 = (Int32)((AliasedValue)c["opportunity_colcount"]).Value;
    System.Console.WriteLine("Column count of all opportunities: " + aggregate3);

}
```
  
<a name="count_distinct"></a>
 
### <a name="count-distinct-columns"></a>個別の列のカウント

次の例は、`countcolumn` `aggregate` 属性を`distinct` 属性を用いてそれぞれの列をカウントする方法を示しています。  
  
 ```csharp
// *****************************************************************************************************************
//                FetchXML      opportunity_distcount   Aggregate 4
// *****************************************************************************************************************
// Fetch the count of distinct names for opportunities.  This is the equivalent of 
// SELECT COUNT(DISTINCT name) AS opportunity_count ... in SQL.
string opportunity_distcount = @" 
<fetch distinct='false' mapping='logical' aggregate='true'> 
    <entity name='opportunity'> 
       <attribute name='name' alias='opportunity_distcount' aggregate='countcolumn' distinct='true'/> 
    </entity> 
</fetch>";

EntityCollection opportunity_distcount_result = _serviceProxy.RetrieveMultiple(new FetchExpression(opportunity_distcount));

foreach (var c in opportunity_distcount_result.Entities)
{
    Int32 aggregate4 = (Int32)((AliasedValue)c["opportunity_distcount"]).Value;
    System.Console.WriteLine("Distinct name count of all opportunities: " + aggregate4);

}
```
  
<a name="max"></a>

## <a name="max"></a>Max

**Null** 値は、Common Data Service がデータの最大値を計算する場合は考慮されません。 ただし、ゼロ (0) は使用されます。  
  
次の例は、`max` `aggregate` 属性の使用方法を示しています。  
  
 ```csharp
// *****************************************************************************************************************
//                FetchXML      estimatedvalue_max   Aggregate 5
// *****************************************************************************************************************
// Fetch the maximum estimatedvalue of all opportunities.  This is the equivalent of 
// SELECT MAX(estimatedvalue) AS estimatedvalue_max ... in SQL.
string estimatedvalue_max = @" 
<fetch distinct='false' mapping='logical' aggregate='true'> 
    <entity name='opportunity'> 
        <attribute name='estimatedvalue' alias='estimatedvalue_max' aggregate='max' /> 
    </entity> 
</fetch>";

EntityCollection estimatedvalue_max_result = service.RetrieveMultiple(new FetchExpression(estimatedvalue_max));

foreach (var c in estimatedvalue_max_result.Entities)
{
    decimal aggregate5 = ((Money)((AliasedValue)c["estimatedvalue_max"]).Value).Value;
    Console.WriteLine("Max estimated value of all opportunities: " + aggregate5);

}
```
  
<a name="min"></a>
 
## <a name="min"></a>分

**Null** 値は、Common Data Service がデータの最小値を計算する場合は考慮されません。 ただし、ゼロ (0) は使用されます。  
  
次の例は、`min``aggregate` 属性の使用方法を示しています。  
  
 ```csharp
// *****************************************************************************************************************
//                FetchXML      estimatedvalue_min   Aggregate 6
// *****************************************************************************************************************
// Fetch the minimum estimatedvalue of all opportunities.  This is the equivalent of 
// SELECT MIN(estimatedvalue) AS estimatedvalue_min ... in SQL.
string estimatedvalue_min = @" 
<fetch distinct='false' mapping='logical' aggregate='true'> 
    <entity name='opportunity'> 
       <attribute name='estimatedvalue' alias='estimatedvalue_min' aggregate='min' /> 
    </entity> 
</fetch>";

EntityCollection estimatedvalue_min_result = _serviceProxy.RetrieveMultiple(new FetchExpression(estimatedvalue_min));

foreach (var c in estimatedvalue_min_result.Entities)
{
    decimal aggregate6 = ((Money)((AliasedValue)c["estimatedvalue_min"]).Value).Value;
    System.Console.WriteLine("Minimum estimated value of all opportunities: " + aggregate6);

}
```
  
<a name="sum"></a>

## <a name="sum"></a>合計

次の例は、`sum``aggregate` 属性の使用方法を示しています。  
  
 ```csharp
// *****************************************************************************************************************
//                FetchXML      estimatedvalue_sum   Aggregate 7
// *****************************************************************************************************************
// Fetch the sum of estimatedvalue for all opportunities.  This is the equivalent of 
// SELECT SUM(estimatedvalue) AS estimatedvalue_sum ... in SQL.
string estimatedvalue_sum = @" 
<fetch distinct='false' mapping='logical' aggregate='true'> 
    <entity name='opportunity'> 
       <attribute name='estimatedvalue' alias='estimatedvalue_sum' aggregate='sum' /> 
    </entity> 
</fetch>";

EntityCollection estimatedvalue_sum_result = _serviceProxy.RetrieveMultiple(new FetchExpression(estimatedvalue_sum));

foreach (var c in estimatedvalue_sum_result.Entities)
{
    decimal aggregate7 = ((Money)((AliasedValue)c["estimatedvalue_sum"]).Value).Value;
    System.Console.WriteLine("Sum of estimated value of all opportunities: " + aggregate7);

}
```
  
<a name="mult_agg"></a>
 
## <a name="multiple-aggregates"></a>複数の集計

次の例は、複数の `aggregate` 属性を使用して最小値と最大値を設定する方法を示しています。  
  
 ```csharp
// *****************************************************************************************************************
//                FetchXML      estimatedvalue_avg, estimatedvalue_sum   Aggregate 8
// *****************************************************************************************************************
// Fetch multiple aggregate values within a single query.
string estimatedvalue_avg2 = @" 
<fetch distinct='false' mapping='logical' aggregate='true'> 
    <entity name='opportunity'> 
       <attribute name='opportunityid' alias='opportunity_count' aggregate='count'/> 
       <attribute name='estimatedvalue' alias='estimatedvalue_sum' aggregate='sum'/> 
       <attribute name='estimatedvalue' alias='estimatedvalue_avg' aggregate='avg'/> 
    </entity> 
</fetch>";

EntityCollection estimatedvalue_avg2_result = _serviceProxy.RetrieveMultiple(new FetchExpression(estimatedvalue_avg2));

foreach (var c in estimatedvalue_avg2_result.Entities)
{
    Int32 aggregate8a = (Int32)((AliasedValue)c["opportunity_count"]).Value;
    System.Console.WriteLine("Count of all opportunities: " + aggregate8a);
    decimal aggregate8b = ((Money)((AliasedValue)c["estimatedvalue_sum"]).Value).Value;
    System.Console.WriteLine("Sum of estimated value of all opportunities: " + aggregate8b);
    decimal aggregate8c = ((Money)((AliasedValue)c["estimatedvalue_avg"]).Value).Value;
    System.Console.WriteLine("Average of estimated value of all opportunities: " + aggregate8c);

}
```
  
<a name="groupby"></a>
 
## <a name="group-by"></a>グループ化

次の例は、複数の `aggregate` 属性およびリンクされた `groupby` 属性の使用方法を示しています。  
  
 ```csharp
// *****************************************************************************************************************
//                FetchXML      groupby1   Aggregate 9
// *****************************************************************************************************************
// Fetch a list of users with a count of all the opportunities they own using groupby.
string groupby1 = @" 
<fetch distinct='false' mapping='logical' aggregate='true'> 
    <entity name='opportunity'> 
       <attribute name='name' alias='opportunity_count' aggregate='countcolumn' /> 
       <attribute name='ownerid' alias='ownerid' groupby='true' /> 
    </entity> 
</fetch>";

EntityCollection groupby1_result = _serviceProxy.RetrieveMultiple(new FetchExpression(groupby1));

foreach (var c in groupby1_result.Entities)
{
    Int32 aggregate9a = (Int32)((AliasedValue)c["opportunity_count"]).Value;
    System.Console.WriteLine("Count of all opportunities: " + aggregate9a + "\n");
    string aggregate9b = ((EntityReference)((AliasedValue)c["ownerid"]).Value).Name;
    System.Console.WriteLine("Owner: " + aggregate9b);
    string aggregate9c = (string)((AliasedValue)c["ownerid_owneridyominame"]).Value;
    System.Console.WriteLine("Owner: " + aggregate9c);
    string aggregate9d = (string)((AliasedValue)c["ownerid_owneridyominame"]).Value;
    System.Console.WriteLine("Owner: " + aggregate9d);
}
```
  
以降の例では、次のグループ化の例を示します。  
  
- [リンクしているエンティティによるグループ化](use-fetchxml-aggregation.md#groupby_linked)
- [年別のグループ化](use-fetchxml-aggregation.md#groupby_year)
- [四半期別のグループ化](use-fetchxml-aggregation.md#groupby_quarter)
- [月別のグループ化](use-fetchxml-aggregation.md#groupby_month)
- [週別のグループ化](use-fetchxml-aggregation.md#groupby_week)  
- [日別のグループ化](use-fetchxml-aggregation.md#groupby_day)  
- [複数のグループ化](use-fetchxml-aggregation.md#Multiple_GroupBy)  
  
<a name="groupby_linked"></a>

### <a name="group-by-with-linked-entity"></a>リンクしているエンティティによるグループ化

次の例は、`sum``aggregate` 属性を使用して、リンクしているエンティティの値を合計する方法を示しています。  
  
 ```csharp
// *****************************************************************************************************************
//                FetchXML      groupby2   Aggregate 10
// *****************************************************************************************************************
// Fetch the number of opportunities each manager's direct reports 
// own using a groupby within a link-entity.
string groupby2 = @" 
<fetch distinct='false' mapping='logical' aggregate='true'> 
    <entity name='opportunity'> 
       <attribute name='name' alias='opportunity_count' aggregate='countcolumn' /> 
       <link-entity name='systemuser' from='systemuserid' to='ownerid'>
           <attribute name='parentsystemuserid' alias='managerid' groupby='true' />
       </link-entity> 
    </entity> 
</fetch>";

EntityCollection groupby2_result = _serviceProxy.RetrieveMultiple(new FetchExpression(groupby2));

foreach (var c in groupby2_result.Entities)
{

      int? aggregate10a = (int?)((AliasedValue)c["opportunity_count"]).Value;
      System.Console.WriteLine("Count of all opportunities: " + aggregate10a + "\n");
}
```
  
<a name="groupby_year"></a>

### <a name="group-by-year"></a>年別のグループ化

日付に対するグループ化では、日、週、月、四半期、または年の値を使用します。 次の例は、`aggregate` 属性と `groupby` 属性を使用して、結果を年別にグループ化する方法を示しています。  
  
 ```csharp

// *****************************************************************************************************************
//                FetchXML      byyear   Aggregate 11           
// *****************************************************************************************************************
// Fetch aggregate information about the opportunities that have 
// been won by year.
string byyear = @" 
<fetch distinct='false' mapping='logical' aggregate='true'> 
    <entity name='opportunity'> 
       <attribute name='opportunityid' alias='opportunity_count' aggregate='count'/> 
       <attribute name='estimatedvalue' alias='estimatedvalue_sum' aggregate='sum'/> 
       <attribute name='estimatedvalue' alias='estimatedvalue_avg' aggregate='avg'/> 
       <attribute name='actualclosedate' groupby='true' dategrouping='year' alias='year' />
       <filter type='and'>
           <condition attribute='statecode' operator='eq' value='Won' />
       </filter>
    </entity> 
</fetch>";

EntityCollection byyear_result = _serviceProxy.RetrieveMultiple(new FetchExpression(byyear));

foreach (var c in byyear_result.Entities)
{
    Int32 aggregate11 = (Int32)((AliasedValue)c["year"]).Value;
    System.Console.WriteLine("Year: " + aggregate11);                      
    Int32 aggregate11a = (Int32)((AliasedValue)c["opportunity_count"]).Value;
    System.Console.WriteLine("Count of all opportunities: " + aggregate11a);
    decimal aggregate11b = ((Money)((AliasedValue)c["estimatedvalue_sum"]).Value).Value;
    System.Console.WriteLine("Sum of estimated value of all opportunities: " + aggregate11b);
    decimal aggregate11c = ((Money)((AliasedValue)c["estimatedvalue_avg"]).Value).Value;
    System.Console.WriteLine("Average of estimated value of all opportunities: " + aggregate11c);
    System.Console.WriteLine("----------------------------------------------");
}
```
  
<a name="groupby_quarter"></a>
 
### <a name="group-by-quarter"></a>四半期別のグループ化

次の例は、`aggregate` 属性と `groupby` 属性を使用して、結果を四半期別にグループ化する方法を示しています。  
  
 ```csharp
 // *****************************************************************************************************************
 //                FetchXML      byquarter   Aggregate 12           
 // *****************************************************************************************************************
// Fetch aggregate information about the opportunities that have 
 // been won by quarter.(returns 1-4)
 string byquarter = @" 
 <fetch distinct='false' mapping='logical' aggregate='true'> 
     <entity name='opportunity'> 
        <attribute name='opportunityid' alias='opportunity_count' aggregate='count'/> 
        <attribute name='estimatedvalue' alias='estimatedvalue_sum' aggregate='sum'/> 
        <attribute name='estimatedvalue' alias='estimatedvalue_avg' aggregate='avg'/> 
        <attribute name='actualclosedate' groupby='true' dategrouping='quarter' alias='quarter' />
        <filter type='and'>
            <condition attribute='statecode' operator='eq' value='Won' />
        </filter>
     </entity> 
 </fetch>";

 EntityCollection byquarter_result = _serviceProxy.RetrieveMultiple(new FetchExpression(byquarter));

 foreach (var c in byquarter_result.Entities)
 {
     Int32 aggregate12 = (Int32)((AliasedValue)c["quarter"]).Value;
     System.Console.WriteLine("Quarter: " + aggregate12);
     Int32 aggregate12a = (Int32)((AliasedValue)c["opportunity_count"]).Value;
     System.Console.WriteLine("Count of all opportunities: " + aggregate12a);
     decimal aggregate12b = ((Money)((AliasedValue)c["estimatedvalue_sum"]).Value).Value;
     System.Console.WriteLine("Sum of estimated value of all opportunities: " + aggregate12b);
     decimal aggregate12c = ((Money)((AliasedValue)c["estimatedvalue_avg"]).Value).Value;
     System.Console.WriteLine("Average of estimated value of all opportunities: " + aggregate12c);
     System.Console.WriteLine("----------------------------------------------");
 }
```
  
<a name="groupby_month"></a>

### <a name="group-by-month"></a>月別のグループ化

次の例は、`aggregate` 属性と `groupby` 属性を使用して、結果を月別にグループ化する方法を示しています。  
  
```csharp
// *****************************************************************************************************************
//                FetchXML      bymonth   Aggregate 13           
// *****************************************************************************************************************
// Fetch aggregate information about the opportunities that have 
// been won by month. (returns 1-12)
string bymonth = @" 
<fetch distinct='false' mapping='logical' aggregate='true'> 
    <entity name='opportunity'> 
       <attribute name='opportunityid' alias='opportunity_count' aggregate='count'/> 
       <attribute name='estimatedvalue' alias='estimatedvalue_sum' aggregate='sum'/> 
       <attribute name='estimatedvalue' alias='estimatedvalue_avg' aggregate='avg'/> 
       <attribute name='actualclosedate' groupby='true' dategrouping='month' alias='month' />
       <filter type='and'>
           <condition attribute='statecode' operator='eq' value='Won' />
       </filter>
    </entity> 
</fetch>";

EntityCollection bymonth_result = _serviceProxy.RetrieveMultiple(new FetchExpression(bymonth));

foreach (var c in bymonth_result.Entities)
{
    Int32 aggregate13 = (Int32)((AliasedValue)c["month"]).Value;
    System.Console.WriteLine("Month: " + aggregate13);
    Int32 aggregate13a = (Int32)((AliasedValue)c["opportunity_count"]).Value;
    System.Console.WriteLine("Count of all opportunities: " + aggregate13a);
    decimal aggregate13b = ((Money)((AliasedValue)c["estimatedvalue_sum"]).Value).Value;
    System.Console.WriteLine("Sum of estimated value of all opportunities: " + aggregate13b);
    decimal aggregate13c = ((Money)((AliasedValue)c["estimatedvalue_avg"]).Value).Value;
    System.Console.WriteLine("Average of estimated value of all opportunities: " + aggregate13c);
    System.Console.WriteLine("----------------------------------------------");
}
``` 

<a name="groupby_week"></a>

### <a name="group-by-week"></a>週別のグループ化

次の例は、`aggregate` 属性と `groupby` 属性を使用して、結果を週別にグループ化する方法を示しています。  
  
 ```csharp
// *****************************************************************************************************************
//                FetchXML      byweek   Aggregate 14           
// *****************************************************************************************************************
// Fetch aggregate information about the opportunities that have 
// been won by week. (Returns 1-52)
string byweek = @" 
<fetch distinct='false' mapping='logical' aggregate='true'> 
    <entity name='opportunity'> 
       <attribute name='opportunityid' alias='opportunity_count' aggregate='count'/> 
       <attribute name='estimatedvalue' alias='estimatedvalue_sum' aggregate='sum'/> 
       <attribute name='estimatedvalue' alias='estimatedvalue_avg' aggregate='avg'/> 
       <attribute name='actualclosedate' groupby='true' dategrouping='week' alias='week' />
       <filter type='and'>
           <condition attribute='statecode' operator='eq' value='Won' />
       </filter>
    </entity> 
</fetch>";

EntityCollection byweek_result = _serviceProxy.RetrieveMultiple(new FetchExpression(byweek));

foreach (var c in byweek_result.Entities)
{
    Int32 aggregate14 = (Int32)((AliasedValue)c["week"]).Value;
    System.Console.WriteLine("Week: " + aggregate14);
    Int32 aggregate14a = (Int32)((AliasedValue)c["opportunity_count"]).Value;
    System.Console.WriteLine("Count of all opportunities: " + aggregate14a);
    decimal aggregate14b = ((Money)((AliasedValue)c["estimatedvalue_sum"]).Value).Value;
    System.Console.WriteLine("Sum of estimated value of all opportunities: " + aggregate14b);
    decimal aggregate14c = ((Money)((AliasedValue)c["estimatedvalue_avg"]).Value).Value;
    System.Console.WriteLine("Average of estimated value of all opportunities: " + aggregate14c);
    System.Console.WriteLine("----------------------------------------------");
}
```
  
<a name="groupby_day"></a>

### <a name="group-by-day"></a>日別のグループ化

 次の例は、`aggregate` 属性と `groupby` 属性を使用して、結果を日別にグループ化する方法を示しています。  
  
 ```csharp
// *****************************************************************************************************************
//                FetchXML      byday   Aggregate 15           
// *****************************************************************************************************************
// Fetch aggregate information about the opportunities that have 
// been won by day. (Returns 1-31)
string byday = @" 
<fetch distinct='false' mapping='logical' aggregate='true'> 
    <entity name='opportunity'> 
       <attribute name='opportunityid' alias='opportunity_count' aggregate='count'/> 
       <attribute name='estimatedvalue' alias='estimatedvalue_sum' aggregate='sum'/> 
       <attribute name='estimatedvalue' alias='estimatedvalue_avg' aggregate='avg'/> 
       <attribute name='actualclosedate' groupby='true' dategrouping='day' alias='day' />
       <filter type='and'>
           <condition attribute='statecode' operator='eq' value='Won' />
       </filter>
    </entity> 
</fetch>";

EntityCollection byday_result = _serviceProxy.RetrieveMultiple(new FetchExpression(byday));

foreach (var c in byday_result.Entities)
{
    Int32 aggregate15 = (Int32)((AliasedValue)c["day"]).Value;
    System.Console.WriteLine("Day: " + aggregate15);
    Int32 aggregate15a = (Int32)((AliasedValue)c["opportunity_count"]).Value;
    System.Console.WriteLine("Count of all opportunities: " + aggregate15a);
    decimal aggregate15b = ((Money)((AliasedValue)c["estimatedvalue_sum"]).Value).Value;
    System.Console.WriteLine("Sum of estimated value of all opportunities: " + aggregate15b);
    decimal aggregate15c = ((Money)((AliasedValue)c["estimatedvalue_avg"]).Value).Value;
    System.Console.WriteLine("Average of estimated value of all opportunities: " + aggregate15c);
    System.Console.WriteLine("----------------------------------------------");
}
```
  
<a name="Multiple_GroupBy"></a>
 
### <a name="multiple-group-by"></a>複数のグループ化

次の例は、`aggregate` 属性および複数の `groupby` 句の使用方法を示しています。  
  
 ```csharp
// *****************************************************************************************************************
//                FetchXML      byyrqtr   Aggregate 16           
// *****************************************************************************************************************
// Fetch aggregate information about the opportunities that have 
// been won by year and quarter.
string byyrqtr = @" 
<fetch distinct='false' mapping='logical' aggregate='true'> 
    <entity name='opportunity'> 
       <attribute name='opportunityid' alias='opportunity_count' aggregate='count'/> 
       <attribute name='estimatedvalue' alias='estimatedvalue_sum' aggregate='sum'/> 
       <attribute name='estimatedvalue' alias='estimatedvalue_avg' aggregate='avg'/> 
       <attribute name='actualclosedate' groupby='true' dategrouping='quarter' alias='quarter' />
       <attribute name='actualclosedate' groupby='true' dategrouping='year' alias='year' />
       <filter type='and'>
           <condition attribute='statecode' operator='eq' value='Won' />
       </filter>
    </entity> 
</fetch>";

EntityCollection byyrqtr_result = _serviceProxy.RetrieveMultiple(new FetchExpression(byyrqtr));

foreach (var c in byyrqtr_result.Entities)
{
    Int32 aggregate16d = (Int32)((AliasedValue)c["year"]).Value;
    System.Console.WriteLine("Year: " + aggregate16d);
    Int32 aggregate16 = (Int32)((AliasedValue)c["quarter"]).Value;
    System.Console.WriteLine("Quarter: " + aggregate16);
    Int32 aggregate16a = (Int32)((AliasedValue)c["opportunity_count"]).Value;
    System.Console.WriteLine("Count of all opportunities: " + aggregate16a);
    decimal aggregate16b = ((Money)((AliasedValue)c["estimatedvalue_sum"]).Value).Value;
    System.Console.WriteLine("Sum of estimated value of all opportunities: " + aggregate16b);
    decimal aggregate16c = ((Money)((AliasedValue)c["estimatedvalue_avg"]).Value).Value;
    System.Console.WriteLine("Average of estimated value of all opportunities: " + aggregate16c);
    System.Console.WriteLine("----------------------------------------------");
}
```
  
<a name="orderby_aggregate"></a>

## <a name="order-by"></a>並べ替え

次の例は、`aggregate` 属性および複数の `orderby` 句の使用方法を示しています。  
  
 ```csharp
// *****************************************************************************************************************
//                FetchXML      byyrqtr2   Aggregate 17           
// *****************************************************************************************************************
// Specify the result order for the previous sample.  Order by year, then quarter.
string byyrqtr2 = @" 
<fetch distinct='false' mapping='logical' aggregate='true'> 
    <entity name='opportunity'> 
       <attribute name='opportunityid' alias='opportunity_count' aggregate='count'/> 
       <attribute name='estimatedvalue' alias='estimatedvalue_sum' aggregate='sum'/> 
       <attribute name='estimatedvalue' alias='estimatedvalue_avg' aggregate='avg'/> 
       <attribute name='actualclosedate' groupby='true' dategrouping='quarter' alias='quarter' />
       <attribute name='actualclosedate' groupby='true' dategrouping='year' alias='year' />
       <order alias='year' descending='false' />
       <order alias='quarter' descending='false' />
       <filter type='and'>
           <condition attribute='statecode' operator='eq' value='Won' />
       </filter>
    </entity> 
</fetch>";

EntityCollection byyrqtr2_result = _serviceProxy.RetrieveMultiple(new FetchExpression(byyrqtr2));

foreach (var c in byyrqtr2_result.Entities)
{
    Int32 aggregate17 = (Int32)((AliasedValue)c["quarter"]).Value;
    System.Console.WriteLine("Quarter: " + aggregate17);
    Int32 aggregate17d = (Int32)((AliasedValue)c["year"]).Value;
    System.Console.WriteLine("Year: " + aggregate17d);
    Int32 aggregate17a = (Int32)((AliasedValue)c["opportunity_count"]).Value;
    System.Console.WriteLine("Count of all opportunities: " + aggregate17a);
    decimal aggregate17b = ((Money)((AliasedValue)c["estimatedvalue_sum"]).Value).Value;
    System.Console.WriteLine("Sum of estimated value of all opportunities: " + aggregate17b);
    decimal aggregate17c = ((Money)((AliasedValue)c["estimatedvalue_avg"]).Value).Value;
    System.Console.WriteLine("Average of estimated value of all opportunities: " + aggregate17c);
    System.Console.WriteLine("----------------------------------------------");
}
```
  
### <a name="see-also"></a>関連項目

[FetchXML による大量の結果セットのページング](org-service/page-large-result-sets-with-fetchxml.md)<br />
[Fetch XML スキーマ](fetchxml-schema.md)<br />
<xref:Microsoft.Xrm.Sdk.IOrganizationService.RetrieveMultiple*><br />
<xref:Microsoft.Xrm.Sdk.Messages.RetrieveMultipleRequest><br />
<xref:Microsoft.Xrm.Sdk.Query.FetchExpression>