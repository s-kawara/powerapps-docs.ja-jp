---
title: LINQ を使用してクエリを作成する (Common Data Service) | Microsoft Docs
description: クエリを作成するために Dynamics 365 で .NET 統合言語クエリ (LINQ) クエリ プロバイダーを使用する方法について説明します
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
# <a name="use-linq-to-construct-a-query"></a>LINQ を使用したクエリの構築

Common Data Service の .NET 統合言語クエリ (LINQ) クエリ プロバイダーは、標準の LINQ 構文を使用します。 LINQ クエリを作成するには、最初に関連するエンティティの種類およびそれらの関係を特定します。 その後、データ ソースや他のクエリ パラメーターを指定します。  

 `from` 句は、単一の "ルート" エンティティに戻るために使用されます。 クエリ プロバイダーは 1 種類のエンティティにのみ戻ることができます。 `orderby` 句および `select` 句は、このルート エンティティを参照する必要があります。 "ルート" エンティティとの関係を追加するには `join` 句を使用します。  

<a name="bkmk_operators"></a>   

## <a name="linq-operators"></a>LINQ 演算子  
 すべての LINQ クエリ式は類似した形式を持っています。 次の表に、Common Data Service の LINQ クエリ プロバイダーを使用する際の最も一般的な LINQ クエリ式を示します。  

### <a name="from"></a>から  
 生成されたサービス コンテキストで事前バインドを行う場合、生成されたコンテキスト内で `IQueryable` エンティティ セット (`AccountSet` など) を使用します。  

 生成されたコンテキストを使用しない場合、組織サービス コンテキスト オブジェクトの `CreateQuery` メソッドを使用して Common Data Service エンティティにアクセスできます。  

 例:   

 生成されたサービス コンテキストを使用する場合  

```csharp  
var query1 = from c in context.ContactSet  
select c;  
```  

 `CreateQuery` メソッドを使用する場合  

```csharp  
var query1 = from c in context.CreateQuery<Contact>()  
select c;  
```  

### <a name="join"></a>join (結合)  
 `join` 句は内部結合を表します。 共通の属性値を持つ 2 つ以上のエンティティを操作する場合に使用します。  

 例:   

```csharp  
from c in context.ContactSet  
join a in context.AccountSet on c.ContactId equals a.PrimaryContactId.Id  
```  

### <a name="where"></a>ここで、  
 `where` 句では、一般にブール式を使用して結果にフィルターを適用します。 フィルターは、ソース シーケンスから除外する要素を指定します。 各 `where` 句には 1 種類のエンティティに対する条件のみを含めることができます。 複数のエンティティが関係する複合条件は無効です。 このような場合は、各エンティティを個別の `where` 句でフィルタリングする必要があります。  

 例:   

```csharp  
from a in context.AccountSet  
where (a.Name.StartsWith("Contoso") && a.Address1_StateOrProvince == "WA")  
```  

### <a name="orderby"></a>orderby  
 `orderby` 演算子は、返されたクエリ属性を指定された順番に並べます。  

 例:   

```csharp  
var query1 = from c in context.CreateQuery<Contact>()     
    orderby c.FullName ascending     
    select c;  
foreach ( var q in query1)     
{  
    Console.WriteLine(q.FirstName + " " + q.LastName);     
}  
```  

### <a name="select"></a>選択  
 `select` 句は、返されるデータのフォームを指定します。 この句は、クエリ式の結果に基づいた列セットを作成します。 作業に使用する新しいオブジェクトのインスタンスを定義することもできます。 `select` 句を使用して新しく作成されたオブジェクトは、サーバー上ではなくローカルでインスタンスとして作成されます。  

 例:   

```csharp  
select new Contact     
{  
    ContactId = c.ContactId,  
    FirstName = c.FirstName,  
    LastName = c.LastName,  
    Address1_Telephone1 = c.Address1_Telephone1     
};  
```  

<a name="limitations"></a>   

## <a name="linq-limitations"></a>LINQ の制限  

 LINQ クエリ プロバイダーは LINQ 演算子のサブセットをサポートします。 LINQ で表現できるすべての条件がサポートされているわけではありません。 次の表に、基本的な LINQ 演算子の制限の一部を示します。  


|   LINQ 演算子   |                                                                                                                                              制限                                                                                                                                              |
|-------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      `join`       |                                                                                                                内部結合または外部結合を表します。 左外部結合のみがサポートされます。                                                                                                                |
|      `from`       |                                                                                                                                 1 クエリにつき 1 つの `from` 句をサポートします。                                                                                                                                 |
|      `where`      | 句の左側は属性名、右側は値である必要があります。 左側に定数を設定することはできません。 句の両側を定数にすることはできません。<br /><br /> `String` 関数の `Contains`、`StartsWith`、`EndsWith`、および `Equals` をサポートします。 |
|     `groupBy`     |                               サポートされていません。 FetchXML では、LINQ クエリ プロバイダーで使用できないグループ化オプションがサポートされています。 詳細: [FetchXML の集計の使用](/dynamics365/customer-engagement/developer/use-fetchxml-aggregation)                               |
|     `orderBy`     |                                                                                                                  エンティティ属性 (`Contact.FullName` など) による並べ替えがサポートされています。                                                                                                                  |
|     `select`      |                                                                                                                       匿名型、コンストラクター、初期化子がサポートされています。                                                                                                                       |
|      `last`       |                                                                                                                                 `last` 演算子はサポートされていません。                                                                                                                                 |
| `skip`および`take` |                                                                                       サーバー側のページングを使用する `skip` および `take` はサポートされています。 `skip` の値は `take` の値以上である必要があります。                                                                                        |
|    `aggregate`    |                             サポートされていません。 FetchXML では、LINQ クエリ プロバイダーで使用できない集計オプションがサポートされています。 詳細: [FetchXML の集計の使用](/dynamics365/customer-engagement/developer/use-fetchxml-aggregation)                              |

<a name="filter"></a>   

## <a name="filter-multiple-entities"></a>複数のエンティティのフィルター処理  

 Common Data Service では、複雑な .NET 統合言語クエリ (LINQ) クエリを作成できます。 フィルター句を指定して複数の `Join` 句を使用し、複数のエンティティからの属性をフィルター処理した結果を作成します。  

 次のサンプルは、2 つのエンティティを操作し、各エンティティからの値に基づき結果をフィルター処理する LINQ クエリの作成方法を示します。  

 ```csharp
 using (ServiceContext svcContext = new ServiceContext(_serviceProxy))
{
 var query_where3 = from c in svcContext.ContactSet
                    join a in svcContext.AccountSet
                    on c.ContactId equals a.PrimaryContactId.Id
                    where a.Name.Contains("Contoso")
                    where c.LastName.Contains("Smith")
                    select new
                    {
                     account_name = a.Name,
                     contact_name = c.LastName
                    };

 foreach (var c in query_where3)
 {
  System.Console.WriteLine("acct: " +
   c.account_name +
   "\t\t\t" +
   "contact: " +
   c.contact_name);
 }
}
 ```
### <a name="see-also"></a>関連項目  
 [サンプル: LINQ クエリの作成](/dynamics365/customer-engagement/developer/org-service/sample-create-linq-query.md)   
 [サンプル: LINQ クエリの例](/dynamics365/customer-engagement/developer/org-service/sample-complex-linq-queries.md)   
 [LINQ (.NET Language-Integrated Query) を使用してクエリを作成する](/dynamics365/customer-engagement/developer/org-service/build-queries-with-linq-net-language-integrated-query.md)   
 [LINQ クエリでの遅延バインド エンティティ クラスの使用](/dynamics365/customer-engagement/developer/org-service/use-late-bound-entity-class-linq-query.md)   
 [ブログ: LINQPad 4 Driver for Dynamics CRM REST/Web API are available on CodePlex (CodePlex で使用できる Dynamics CRM REST/Web API 用の LINQPad 4 ドライバー)](http://blogs.msdn.com/b/crminthefield/archive/2015/06/11/linqpad-4-driver-for-dynamics-crm-rest-webapi-are-available-on-codeplex.aspx)