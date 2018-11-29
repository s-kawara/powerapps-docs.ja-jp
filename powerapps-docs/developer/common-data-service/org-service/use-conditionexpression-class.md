---
title: ConditionExpression クラスの使用 (アプリ用 Common Data Service) | Microsoft Docs
description: ConditionExpression クラスで &quot;等しい&quot; 、 &quot;より大きい&quot;などの演算子を用い、属性を値または一連の値と比較する方法について説明します。
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
# <a name="use-the-conditionexpression-class"></a>ConditionExpression クラスの使用

アプリ用 Common Data Service で <xref:Microsoft.Xrm.Sdk.Query.ConditionExpression> class を用いることにより、 “等しい”、“より大きい”といった演算子で属性を値もしくは一連の値と比較することができます。 `ConditionExpression` クラスは、条件式をパラメーターとして他のクラス (<xref:Microsoft.Xrm.Sdk.Query.QueryExpression>、<xref:Microsoft.Xrm.Sdk.Query.FilterExpression> など) に引き渡せるようにします。  
  
 `ConditionExpression` クラスを使用して条件を作成する際に設定できるプロパティを次の表に示します。  
  
|プロパティ|説明|  
|--------------|-----------------|  
|<xref:Microsoft.Xrm.Sdk.Query.ConditionExpression.AttributeName>|条件式内の属性の論理名を指定します。|  
|<xref:Microsoft.Xrm.Sdk.Query.ConditionExpression.Operator>|条件演算子を指定します。 これは、<xref:Microsoft.Xrm.Sdk.Query.ConditionOperator> 列挙体を使用して設定します。|  
|<xref:Microsoft.Xrm.Sdk.Query.ConditionExpression.Values>|属性の値を指定します。|  
  
 <xref:Microsoft.Xrm.Sdk.Query.FilterExpression.AddCondition(Microsoft.Xrm.Sdk.Query.ConditionExpression)> メソッド (または <xref:Microsoft.Xrm.Sdk.Query.ConditionExpression> のコンストラクター) を使用するときは、配列が複数の値として追加されるか、配列として追加されるかをよく理解したうえで、作業を行ってください。  
  
 次のコードは、配列の使い方によって結果が異なる例です。  
  
```csharp  
string[] values = new string[] { "Value1", "Value2" };  
ConditionExpression c = new ConditionExpression("name", ConditionOperator.In, values);  
Console.WriteLine(c.Values.Count); //This will output 2   
string[] values = new string[] { "Value1", "Value2" }object value = values;  
ConditionExpression c = new ConditionExpression("name", ConditionOperator.In, value);  
Console.WriteLine(c.Values.Count); //This will output 1  
  
```  
  
 希望する動作に応じて、`object[]` か `object` に型を変換しなければならない場合があります。  
  
 状態コードなどの列挙体と属性値を比較する条件を作成する場合は、必ず `ToString` メソッドを使用して値を文字列に変換してください。  
  
## <a name="example"></a>例  
 次のコード例は、`ConditionExpression` クラスの使用方法を示しています。  
  
```csharp  
  
//  Query using ConditionExpression    
ConditionExpression condition1 = new ConditionExpression();  
condition1.AttributeName = "lastname";    
condition1.Operator = ConditionOperator.Equal;    
condition1.Values.Add("Brown");                    
FilterExpression filter1 = new FilterExpression();    
filter1.Conditions.Add(condition1);    
QueryExpression query = new QueryExpression("contact");    
query.ColumnSet.AddColumns("firstname", "lastname");    
query.Criteria.AddFilter(filter1);    
EntityCollection result1 = _serviceProxy.RetrieveMultiple(query);    
Console.WriteLine();    
Console.WriteLine("Query using Query Expression with ConditionExpression and FilterExpression");    
Console.WriteLine("---------------------------------------");    
foreach (var a in result1.Entities)    
{  
      Console.WriteLine("Name: " + a.Attributes["firstname"] + " " + a.Attributes["lastname"]);    
}    
Console.WriteLine("---------------------------------------");  
```  
  
## <a name="example"></a>例  
 次のコード例は、`ConditionExpression` クラスを使用して非アクティブ状態をテストする方法を示しています。  
  
```csharp  
  
ConditionExpression condition3 = new ConditionExpression();  
condition3.AttributeName = "statecode";  
condition3.Operator = ConditionOperator.Equal;  
condition3.Values.Add(AccountState.Active);  
  
```  
  
### <a name="see-also"></a>関連項目  
 [クエリの作成](build-queries-with-queryexpression.md)   
 [QueryExpression でクエリを作成する](build-queries-with-queryexpression.md)   
 [FilterExpression クラスの使用](use-filterexpression-class.md)   
 <xref:Microsoft.Xrm.Sdk.Query.ConditionExpression>