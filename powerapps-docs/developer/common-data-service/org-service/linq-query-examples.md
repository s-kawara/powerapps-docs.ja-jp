---
title: Linq クエリの例の (Common Data Service) | Microsoft Docs
description: <Description>
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
# <a name="linq-query-examples-using-organizationservicecontext-with-common-data-service"></a>Common Data Service で OrganizationServiceContext を使用した LINQ クエリの例

ここでは、LINQ クエリの多数のコード例を紹介します。  
  
<a name="SimpleWhereClause"></a>   
## <a name="simple-where-clause"></a>シンプルな Where 句  
 次のサンプルは、Name に "Contoso" が含まれている取引先企業の一覧を取得する方法を示します。  
  
```csharp
using (ServiceContext svcContext = new ServiceContext(_serviceProxy))
{
    var query_where1 = from a in svcContext.AccountSet
        where a.Name.Contains("Contoso")
        select a;
    foreach (var a in query_where1)
    {
        System.Console.WriteLine(a.Name + " " + a.Address1_City);
    }
}
```  
  
 次のサンプルは、Name に "Contoso" が含まれ、Address1_City が “Redmond” である取引先企業の一覧を取得する方法を示します。  
  
```csharp
using (ServiceContext svcContext = new ServiceContext(_serviceProxy))
{
    var query_where2 = from a in svcContext.AccountSet
                    where a.Name.Contains("Contoso")
                    where a.Address1_City == "Redmond"
                    select a;

    foreach (var a in query_where2)
    {
        System.Console.WriteLine(a.Name + " " + a.Address1_City);
    }
}
``` 
  
<a name="JoinandSimpleWhereClause"></a>   
## <a name="join-and-simple-where-clause"></a>結合とシンプルな Where 句  
 次のサンプルは、取引先企業の Name に "Contoso" が含まれ、取引先担当者の LastName に "Smith" が含まれ、取引先担当者が取引先企業の取引先責任者である、取引先企業の Name と取引先担当者の LastName を取得する方法を示します。  
  
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
  
<a name="UsingtheDistinctOperator"></a>   
## <a name="use-the-distinct-operator"></a>Distinct 演算子の使用  
 次のサンプルは、取引先担当者の姓の個別一覧を取得する方法を示します。 重複がある名前でも、一覧には 1 回だけ出現します。  
  
```csharp
using (ServiceContext svcContext = new ServiceContext(_serviceProxy))
{
    var query_distinct = (from c in svcContext.ContactSet
                       select c.LastName).Distinct();
    foreach (var c in query_distinct)
    {
        System.Console.WriteLine(c);
    }
}
```
  
<a name="SimpleInnerJoin"></a>   
## <a name="simple-inner-join"></a>シンプルな内部結合  
次のサンプルは、取引先企業の取引先責任者の一覧に含まれる取引先企業および取引先担当者についての情報を取得する方法を示します。  
  
```csharp
using (ServiceContext svcContext = new ServiceContext(_serviceProxy))
{
    var query_join1 = from c in svcContext.ContactSet
                   join a in svcContext.AccountSet
                  on c.ContactId equals a.PrimaryContactId.Id
                   select new
                   {
                    c.FullName,
                    c.Address1_City,
                    a.Name,
                    a.Address1_Name
                   };
    foreach (var c in query_join1)
    {
        System.Console.WriteLine("acct: " +
        c.Name +
        "\t\t\t" +
        "contact: " +
        c.FullName);
    }
}
```  
  
<a name="SelfJoin"></a>   
## <a name="self-join"></a>自己結合  
 次のサンプルは、取引先企業の親会社である取引先企業についての情報を取得する方法を示します。  
  
```csharp
using (ServiceContext svcContext = new ServiceContext(_serviceProxy))
{
    var query_join5 = from a in svcContext.AccountSet
                   join a2 in svcContext.AccountSet
                   on a.ParentAccountId.Id equals a2.AccountId

                   select new
                   {
                    account_name = a.Name,
                    account_city = a.Address1_City
                   };
    foreach (var c in query_join5)
    {
        System.Console.WriteLine(c.account_name + "  " + c.account_city);
    }
}
```
  
<a name="DoubleJoin"></a>   
## <a name="double-and-multiple-joins"></a>二重結合と複数結合  
 次のサンプルは、取引先担当者が取引先企業の取引先責任者であり、潜在顧客が取引先企業の元の潜在顧客である、取引先企業、取引先担当者、潜在顧客の情報を取得する方法を示します。  
  
```csharp
using (ServiceContext svcContext = new ServiceContext(_serviceProxy))
{
    var query_join4 = from a in svcContext.AccountSet
                   join c in svcContext.ContactSet
                   on a.PrimaryContactId.Id equals c.ContactId
                   join l in svcContext.LeadSet
                   on a.OriginatingLeadId.Id equals l.LeadId
                   select new
                   {
                    contact_name = c.FullName,
                    account_name = a.Name,
                    lead_name = l.FullName
                   };
    foreach (var c in query_join4)
    {
        System.Console.WriteLine(c.contact_name +
        "  " +
        c.account_name +
        "  " +
        c.lead_name);
    }
}
```  
  
 次のサンプルは、取引先企業が別の取引先企業の親企業であり、取引先担当者がその取引先企業の取引先責任者である、取引先企業および取引先担当者の情報を取得する方法を示します。  
  
```csharp
using (ServiceContext svcContext = new ServiceContext(_serviceProxy))
{
    var query_join6 = from c in svcContext.ContactSet
                   join a in svcContext.AccountSet
                   on c.ContactId equals a.PrimaryContactId.Id
                   join a2 in svcContext.AccountSet
                   on a.ParentAccountId.Id equals a2.AccountId
                   select new
                   {
                    contact_name = c.FullName,
                    account_name = a.Name
                   };
    foreach (var c in query_join6)
    {
        System.Console.WriteLine(c.contact_name + "  " + c.account_name);
    }
}
```
  
<a name="JoinUsingEntityFields"></a>   
## <a name="join-using-entity-fields"></a>エンティティ フィールドを使用した結合  
 次のサンプルは、取引先企業の情報を一覧から取得する方法を示します。  
  
```csharp
using (ServiceContext svcContext = new ServiceContext(_serviceProxy))
{
    var list_join = (from a in svcContext.AccountSet
                  join c in svcContext.ContactSet
                  on a.PrimaryContactId.Id equals c.ContactId
                  where a.Name == "Contoso Ltd" &&
                  a.Address1_Name == "Contoso Pharmaceuticals"
                  select a).ToList();
    foreach (var c in list_join)
    {
        System.Console.WriteLine("Account " + list_join[0].Name
        + " and it's primary contact "
        + list_join[0].PrimaryContactId.Id);
    }
}
```  
  
<a name="LeftJoin"></a>   
## <a name="late-binding-left-join"></a>遅延バインド左結合  
 次のサンプルは、左結合を示します。 左結合は、2 つのソースから子を持つ親と持たない親を返します。 親と子の間に関連付けがありますが、実際に子が存在するとは限りません。  
  
```csharp
using (ServiceContext svcContext = new ServiceContext(_serviceProxy))
{
    var query_join8 = from a in svcContext.AccountSet
                   join c in svcContext.ContactSet
                   on a.PrimaryContactId.Id equals c.ContactId
                   into gr
                   from c_joined in gr.DefaultIfEmpty()
                   select new
                   {
                    contact_name = c_joined.FullName,
                    account_name = a.Name
                   };
    foreach (var c in query_join8)
    {
        System.Console.WriteLine(c.contact_name + "  " + c.account_name);
    }
}
``` 
  
<a name="UsingtheEqualsOperator"></a>   
## <a name="use-the-equals-operator"></a>等価演算子の使用  
 次のサンプルは、FirstName が "Colin" である取引先担当者の一覧を取得する方法を示します。  
  
```csharp
using (ServiceContext svcContext = new ServiceContext(_serviceProxy))
{
    var query_equals1 = from c in svcContext.ContactSet
                     where c.FirstName.Equals("Colin")
                     select new
                     {
                      c.FirstName,
                      c.LastName,
                      c.Address1_City
                     };
    foreach (var c in query_equals1)
    {
        System.Console.WriteLine(c.FirstName +
        " " + c.LastName +
        " " + c.Address1_City);
    }
}
``` 
  
 次のサンプルは、FamilyStatusCode が "3" である取引先担当者の一覧を取得する方法を示します。 これは、**離婚**の**婚姻区分**オプションに相応します。  
  
```csharp
using (ServiceContext svcContext = new ServiceContext(_serviceProxy))
{
    var query_equals2 = from c in svcContext.ContactSet
                     where c.FamilyStatusCode.Equals(3)
                     select new
                     {
                      c.FirstName,
                      c.LastName,
                      c.Address1_City
                     };
    foreach (var c in query_equals2)
    {
        System.Console.WriteLine(c.FirstName +
        " " + c.LastName +
        " " + c.Address1_City);
    }
}
``` 
  
<a name="UsingtheNotEqualsOperator"></a>   
## <a name="use-the-not-equals-operator"></a>非等価演算子の使用  
 次のサンプルは、Address1_City が "Redmond" でない取引先担当者の一覧を取得する方法を示します。  
  
```csharp
using (ServiceContext svcContext = new ServiceContext(_serviceProxy))
{
    var query_ne1 = from c in svcContext.ContactSet
                 where c.Address1_City != "Redmond"
                 select new
                 {
                  c.FirstName,
                  c.LastName,
                  c.Address1_City
                 };
    foreach (var c in query_ne1)
    {
        System.Console.WriteLine(c.FirstName + " " +
        c.LastName + " " + c.Address1_City);
    }
}
```  
  
 次のサンプルは、FirstName が "Colin" でない取引先担当者の一覧を取得する方法を示します。  
  
```csharp
using (ServiceContext svcContext = new ServiceContext(_serviceProxy))
{
    var query_ne2 = from c in svcContext.ContactSet
                 where !c.FirstName.Equals("Colin")
                 select new
                 {
                  c.FirstName,
                  c.LastName,
                  c.Address1_City
                 };

    foreach (var c in query_ne2)
    {
        System.Console.WriteLine(c.FirstName + " " +
        c.LastName + " " + c.Address1_City);
    }
}
```  
  
<a name="BKMK_UsingMethodBasedLINQQueryWithWhereClause"></a>   
## <a name="use-a-method-based-linq-query-with-a-where-clause"></a>Where 句によるメソッドベース LINQ クエリの使用  
 次のサンプルは、LastName に "Smith" または “Smi” が含まれている取引先担当者の一覧を取得する方法を示します。  
  
```csharp
using (ServiceContext svcContext = new ServiceContext(_serviceProxy))
{
    var methodResults = svcContext.ContactSet
    .Where(a => a.LastName == "Smith");
    var methodResults2 = svcContext.ContactSet
    .Where(a => a.LastName.StartsWith("Smi"));
    Console.WriteLine();
    Console.WriteLine("Method query using Lambda expression");
    Console.WriteLine("---------------------------------------");
    foreach (var a in methodResults)
    {
        Console.WriteLine("Name: " + a.FirstName + " " + a.LastName);
    }
    Console.WriteLine("---------------------------------------");
    Console.WriteLine("Method query 2 using Lambda expression");
    Console.WriteLine("---------------------------------------");
    foreach (var a in methodResults2)
    {
        Console.WriteLine("Name: " + a.Attributes["firstname"] +
        " " + a.Attributes["lastname"]);
    }
}
``` 
  
<a name="BKMK_UsingGreaterThanOperator"></a>   
## <a name="use-the-greater-than-operator"></a>より大きい演算子の使用  
 次のサンプルは、記念日の日付が 2010 年 2 月 5 日以降の取引先担当者の一覧を取得する方法を示します。  
  
```csharp
using (ServiceContext svcContext = new ServiceContext(_serviceProxy))
{
    var query_gt1 = from c in svcContext.ContactSet
                 where c.Anniversary > new DateTime(2010, 2, 5)
                 select new
                 {
                  c.FirstName,
                  c.LastName,
                  c.Address1_City
                 };

    foreach (var c in query_gt1)
    {
        System.Console.WriteLine(c.FirstName + " " +
        c.LastName + " " + c.Address1_City);
    }
}
``` 
  
 次のサンプルは、CreditLimit が $20,000 より大きい取引先担当者を取得する方法を示します。  
  
```csharp
using (ServiceContext svcContext = new ServiceContext(_serviceProxy))
{
    var query_gt2 = from c in svcContext.ContactSet
                 where c.CreditLimit.Value > 20000
                 select new
                 {
                  c.FirstName,
                  c.LastName,
                  c.Address1_City
                 };
    foreach (var c in query_gt2)
    {
        System.Console.WriteLine(c.FirstName + " " +
        c.LastName + " " + c.Address1_City);
    }
}
``` 
  
<a name="BKMK_UsingGreaterThanOrEqualsAndLessThanOrEqualsOperators"></a>   
## <a name="use-the-greater-than-or-equals-and-less-than-or-equals-operators"></a>以上または以下演算子の使用  
 次のサンプルは、CreditLimit が $200 より大きく $400 未満の取引先担当者を取得する方法を示します。  
  
```csharp
using (ServiceContext svcContext = new ServiceContext(_serviceProxy))
{
 var query_gele1 = from c in svcContext.ContactSet
                   where c.CreditLimit.Value >= 200 &&
                   c.CreditLimit.Value <= 400
                   select new
                   {
                    c.FirstName,
                    c.LastName
                   };
 foreach (var c in query_gele1)
 {
  System.Console.WriteLine(c.FirstName + " " + c.LastName);
 }
}
``` 
  
<a name="BKMK_UsingContainsOperator"></a>   
## <a name="use-the-contains-operator"></a>"含む" 演算子の使用  
 次のサンプルは、説明が "Alpine" である取引先担当者の一覧を取得する方法を示します。  
  
```csharp
using (ServiceContext svcContext = new ServiceContext(_serviceProxy))
{
    var query_contains1 = from c in svcContext.ContactSet
                       where c.Description.Contains("Alpine")
                       select new
                       {
                        c.FirstName,
                        c.LastName
                       };
    foreach (var c in query_contains1)
    {
        System.Console.WriteLine(c.FirstName + " " + c.LastName);
    }
}
```
  
<a name="BKMK_UsingDoesNotContainOperator"></a>   
## <a name="use-the-does-not-contain-operator"></a>"含まない" 演算子の使用  
 次のサンプルは、説明が "Coho" でない取引先担当者の一覧を取得する方法を示します。  
  
```csharp
using (ServiceContext svcContext = new ServiceContext(_serviceProxy))
{
    var query_contains2 = from c in svcContext.ContactSet
                       where !c.Description.Contains("Coho")
                       select new
                       {
                        c.FirstName,
                        c.LastName
                       };
    foreach (var c in query_contains2)
    {
        System.Console.WriteLine(c.FirstName + " " + c.LastName);
    }
}
```  
  
<a name="BKMK_UsingEndsWithOperator"></a>   
## <a name="use-the-startswith-and-endswith-operators"></a>StartsWith および EndsWith 演算子の使用  
 次のサンプルは、FirstName が “Bri” で始まる取引先担当者を取得する方法を示します。  
  
```csharp
using (ServiceContext svcContext = new ServiceContext(_serviceProxy))
{
    var query_startswith1 = from c in svcContext.ContactSet
                         where c.FirstName.StartsWith("Bri")
                         select new
                         {
                          c.FirstName,
                          c.LastName
                         };
    foreach (var c in query_startswith1)
    {
        System.Console.WriteLine(c.FirstName + " " + c.LastName);
    }
}
```  

  
 次のサンプルは、LastName が “cox” で終わる取引先担当者を取得する方法を示します。  
  
```csharp
using (ServiceContext svcContext = new ServiceContext(_serviceProxy))
{
    var query_endswith1 = from c in svcContext.ContactSet
                       where c.LastName.EndsWith("cox")
                       select new
                       {
                        c.FirstName,
                        c.LastName
                       };
    foreach (var c in query_endswith1)
    {
        System.Console.WriteLine(c.FirstName + " " + c.LastName);
    }
}
```  

  
<a name="BKMK_UsingAndOrOperators"></a>   
## <a name="use-the-and-and-or-operators"></a>And および Or 演算子の使用  
 次のサンプルは、Address1_City が "Redmond" または "Bellevue" で、かつ CreditLimit が $200 より大きい取引先担当者を取得する方法を示します。  
  
```csharp
using (ServiceContext svcContext = new ServiceContext(_serviceProxy))
{
    var query_andor1 = from c in svcContext.ContactSet
                    where ((c.Address1_City == "Redmond" ||
                    c.Address1_City == "Bellevue") &&
                    (c.CreditLimit.Value != null &&
                    c.CreditLimit.Value >= 200))
                    select c;

    foreach (var c in query_andor1)
    {
        System.Console.WriteLine(c.LastName + ", " + c.FirstName + " " +
        c.Address1_City + " " + c.CreditLimit.Value);
    }
}
```  

  
<a name="BKMKUsingOrderByOperator"></a>   
## <a name="use-the-orderby-operator"></a>OrderBy 演算子の使用  
 次のサンプルは、CreditLimit の降順で並べ替えた取引先担当者を取得する方法を示します。  
  
```csharp
using (ServiceContext svcContext = new ServiceContext(_serviceProxy))
{
    var query_orderby1 = from c in svcContext.ContactSet
                      where !c.CreditLimit.Equals(null)
                      orderby c.CreditLimit descending
                      select new
                      {
                       limit = c.CreditLimit,
                       first = c.FirstName,
                       last = c.LastName
                      };
    foreach (var c in query_orderby1)
    {
        System.Console.WriteLine(c.limit.Value + " " +
        c.last + ", " + c.first);
    }
}
```   

  
 次のサンプルは、LastName を降順で、FirstName を昇順で並べ替えた取引先担当者を取得する方法を示します。  
  
```csharp
using (ServiceContext svcContext = new ServiceContext(_serviceProxy))
{
    var query_orderby2 = from c in svcContext.ContactSet
                      orderby c.LastName descending,
                      c.FirstName ascending
                      select new
                      {
                       first = c.FirstName,
                       last = c.LastName
                      };

    foreach (var c in query_orderby2)
    {
        System.Console.WriteLine(c.last + ", " + c.first);
    }
}
```  

  
<a name="BKMK_UsingFirstAndSingleOperators"></a>   
## <a name="use-the-first-and-single-operators"></a>First および Single 演算子の使用  
 次のサンプルは、返される最初の取引先担当者レコードだけを取得する方法、および条件に一致する取引先担当者レコードを 1 つだけ取得する方法を示します。  
  
```csharp
using (ServiceContext svcContext = new ServiceContext(_serviceProxy))
{
    Contact firstcontact = svcContext.ContactSet.First();

    Contact singlecontact = svcContext.ContactSet.Single(c => c.ContactId == _contactId1);
    System.Console.WriteLine(firstcontact.LastName + ", " +
    firstcontact.FirstName + " is the first contact");
    System.Console.WriteLine("==========================");
    System.Console.WriteLine(singlecontact.LastName + ", " +
    singlecontact.FirstName + " is the single contact");
}
```  

  
<a name="BKMK_RetrievingFormattedValues"></a>   
## <a name="retrieving-formatted-values"></a>書式設定された値の取得  
 次のサンプルは、optionset オプションのラベル (この場合は現在のレコード ステータスの値) を取得する方法を示します。  
  
```csharp
using (ServiceContext svcContext = new ServiceContext(_serviceProxy))
{
    var list_retrieve1 = from c in svcContext.ContactSet
                      where c.ContactId == _contactId1
                      select new { StatusReason = c.FormattedValues["statuscode"] };
    foreach (var c in list_retrieve1)
    {
        System.Console.WriteLine("Status: " + c.StatusReason);
    }
}
```  

  
<a name="BKMK_UsingTheSkipAndTakeOperatorsWithoutPaging"></a>   
## <a name="use-the-skip-and-take-operators-without-paging"></a>Skip および Take 演算子の使用 (ページングなし) 

 次のサンプルは、[Skip](https://msdn.microsoft.com/library/bb358985.aspx) および [Take](https://msdn.microsoft.com/library/bb503062.aspx) 演算子を使用して、LastName が "Parker" ではないレコードを 2 つスキップした後で 2 レコードだけ取得する方法を示します。  
  
```csharp
using (ServiceContext svcContext = new ServiceContext(_serviceProxy))
{

    var query_skip = (from c in svcContext.ContactSet
                   where c.LastName != "Parker"
                   orderby c.FirstName
                   select new
                       {
                        last = c.LastName,
                        first = c.FirstName
                       }).Skip(2).Take(2);
    foreach (var c in query_skip)
    {
        System.Console.WriteLine(c.first + " " + c.last);
    }
}
```  

  
<a name="BKMK_UsingTheFirstOrDefaultAndSingleOrDefaultOperators"></a>   
## <a name="use-the-firstordefault-and-singleordefault-operators"></a>FirstOrDefault および SingleOrDefault 演算子の使用  
 [FirstOrDefault](https://msdn.microsoft.com/library/system.linq.enumerable.firstordefault.aspx) 演算子は、シーケンスの最初の要素を返し、要素が見つからない場合は既定値を返します。 [SingleOrDefault](https://msdn.microsoft.com/library/system.linq.enumerable.singleordefault.aspx) 演算子は、シーケンスの特定の要素を 1 つだけ返し、その要素が見つからない場合は既定値を返します。 次のサンプルは、これらの演算子の使用方法を示します。  
  
```csharp
using (ServiceContext svcContext = new ServiceContext(_serviceProxy))
{

    Contact firstorcontact = svcContext.ContactSet.FirstOrDefault();

    Contact singleorcontact = svcContext.ContactSet
        .SingleOrDefault(c => c.ContactId == _contactId1);


    System.Console.WriteLine(firstorcontact.FullName +
        " is the first contact");
    System.Console.WriteLine("==========================");
    System.Console.WriteLine(singleorcontact.FullName +
        " is the single contact");
}
```  

  
<a name="BKMK_UsingASelfJoinWithConditionOnLinkedEntity"></a>   
## <a name="use-a-self-join-with-a-condition-on-the-linked-entity"></a>リンクされたエンティティの条件に基づく自己結合の使用  
 次のサンプルは、一方の取引先企業が他方の取引先企業の親会社である 2 つの取引先企業の名前を取得する方法を示します。  
  
```csharp
using (ServiceContext svcContext = new ServiceContext(_serviceProxy))
{
    var query_joincond = from a1 in svcContext.AccountSet
                      join a2 in svcContext.AccountSet
                      on a1.ParentAccountId.Id equals a2.AccountId
                      where a2.AccountId == _accountId1
                      select new { Account = a1, Parent = a2 };
    foreach (var a in query_joincond)
    {
        System.Console.WriteLine(a.Account.Name + " " + a.Parent.Name);
    }
}
```  

  
<a name="BKMK_UsingTransformationInTheWhereClause"></a>   
## <a name="use-a-transformation-in-the-where-clause"></a>Where 句での変換の使用  
 次のサンプルは、記念日の日付が 2010 年 1 月 1 日より後である特定の取引先担当者を取得する方法を示します。  
  
```csharp
using (ServiceContext svcContext = new ServiceContext(_serviceProxy))
{
    var query_wheretrans = from c in svcContext.ContactSet
                        where c.ContactId == _contactId1 &&
                        c.Anniversary > DateTime.Parse("1/1/2010")
                        select new
                        {
                         c.FirstName,
                         c.LastName
                        };
    foreach (var c in query_wheretrans)
    {
        System.Console.WriteLine(c.FirstName + " " + c.LastName);
    }
}
```  

  
<a name="BKMK_UsingAPagingSort"></a>   
## <a name="use-a-paging-sort"></a>ページングの並べ替えの使用  
 次のサンプルは、追加条件を使用して複数の列を並べ替える方法を示します。  
  
```csharp
using (ServiceContext svcContext = new ServiceContext(_serviceProxy))
{
    var query_pagingsort1 = (from c in svcContext.ContactSet
                          where c.LastName != "Parker"
                          orderby c.LastName ascending,
                          c.FirstName descending
                          select new { c.FirstName, c.LastName })
                          .Skip(2).Take(2);
    foreach (var c in query_pagingsort1)
    {
        System.Console.WriteLine(c.FirstName + " " + c.LastName);
    }
}
```  

  
 次のサンプルは、並べ替えに使用する列が取得する列とは異なる場合のページングの並べ替えを示します。  
  
```csharp
using (ServiceContext svcContext = new ServiceContext(_serviceProxy))
{
    var query_pagingsort2 = (from c in svcContext.ContactSet
                          where c.LastName != "Parker"
                          orderby c.FirstName descending
                          select new { c.FirstName }).Skip(2).Take(2);
    foreach (var c in query_pagingsort2)
    {
        System.Console.WriteLine(c.FirstName);
    }
}
```  

  
 次のサンプルは、最初の 10 件のレコードを取得する方法を示します。  
  
```csharp
using (ServiceContext svcContext = new ServiceContext(_serviceProxy))
{
    var query_pagingsort3 = (from c in svcContext.ContactSet
                          where c.LastName.StartsWith("W")
                          orderby c.MiddleName ascending,
                          c.FirstName descending
                          select new
                          {
                           c.FirstName,
                           c.MiddleName,
                           c.LastName
                          }).Take(10);
    foreach (var c in query_pagingsort3)
    {
        System.Console.WriteLine(c.FirstName + " " +
            c.MiddleName + " " + c.LastName);
    }
}
```  

  
<a name="BKMK_RetrievingRelatedEntityColumns"></a>   
## <a name="retrieve-related-entity-columns-for-1-to-n-relationships"></a>関連するエンティティ列の取得 (一対多の関係の場合)  
 次のサンプルは、関連する取引先企業と取引先担当者のレコードから列を取得する方法を示します。  
  
```csharp
using (ServiceContext svcContext = new ServiceContext(_serviceProxy))
{
     var query_retrieve1 = from c in svcContext.ContactSet
                       join a in svcContext.AccountSet
                       on c.ContactId equals a.PrimaryContactId.Id
                       where c.ContactId != _contactId1
                       select new { Contact = c, Account = a };
     foreach (var c in query_retrieve1)
    {
          System.Console.WriteLine("Acct: " + c.Account.Name +
           "\t\t" + "Contact: " + c.Contact.FullName);
     }
}
```  
  
<a name="BKMK_UsingValueToRetrieveTheValueOfAnAttribute"></a>   
## <a name="use-value-to-retrieve-the-value-of-an-attribute"></a>.value による属性値の取得  
 次のサンプルは、属性の値にアクセスするための値の使用方法を示します。  
  
```csharp
using (ServiceContext svcContext = new ServiceContext(_serviceProxy))
{

     var query_value = from c in svcContext.ContactSet
                   where c.ContactId != _contactId2
                   select new
                   {
                    ContactId = c.ContactId != null ?
                     c.ContactId.Value : Guid.Empty,
                    NumberOfChildren = c.NumberOfChildren != null ?
                     c.NumberOfChildren.Value : default(int),
                    CreditOnHold = c.CreditOnHold != null ?
                     c.CreditOnHold.Value : default(bool),
                    Anniversary = c.Anniversary != null ?
                     c.Anniversary.Value : default(DateTime)
                   };

     foreach (var c in query_value)
     {
      System.Console.WriteLine(c.ContactId + " " + c.NumberOfChildren + 
           " " + c.CreditOnHold + " " + c.Anniversary);
     }
}
```  
  
<a name="BKMK_MultipleProjectionsNewDataTypeCastingToDifferentTypes"></a>   
## <a name="multiple-projections-new-data-type-casting-to-different-types"></a>複数のプロジェクション (新しいデータ型を別の型にキャスト)  
 次のサンプルは、複数のプロジェクションおよび値を異なるデータ型にキャストする方法を示します。  
  
```csharp
using (ServiceContext svcContext = new ServiceContext(_serviceProxy))
{
     var query_projections = from c in svcContext.ContactSet
                         where c.ContactId == _contactId1
                         && c.NumberOfChildren != null && 
                         c.Anniversary.Value != null
                         select new
                         {
                          Contact = new Contact { 
                           LastName = c.LastName, 
                           NumberOfChildren = c.NumberOfChildren 
                          },
                          NumberOfChildren = (double)c.NumberOfChildren,
                          Anniversary = c.Anniversary.Value.AddYears(1),
                         };
     foreach (var c in query_projections)
     {
          System.Console.WriteLine(c.Contact.LastName + " " + 
               c.NumberOfChildren + " " + c.Anniversary);
     }
}
```  
  
<a name="BKMK_UsingTheGetAttributeValueMethod"></a>   
## <a name="use-the-getattributevalue-method"></a>GetAttributeValue メソッドの使用  
 次のサンプルは、<xref:Microsoft.Xrm.Sdk.Entity.GetAttributeValue``1(System.String)> メソッドの使用方法を示します。  
  
```csharp
using (ServiceContext svcContext = new ServiceContext(_serviceProxy))
{
    var query_getattrib = from c in svcContext.ContactSet
                       where c.GetAttributeValue<Guid>("contactid") != _contactId1
                       select new
                       {
                        ContactId = c.GetAttributeValue<Guid?>("contactid"),
                        NumberOfChildren = c.GetAttributeValue<int?>("numberofchildren"),
                        CreditOnHold = c.GetAttributeValue<bool?>("creditonhold"),
                        Anniversary = c.GetAttributeValue<DateTime?>("anniversary"),
                       };

    foreach (var c in query_getattrib)
    {
        System.Console.WriteLine(c.ContactId + " " + c.NumberOfChildren + 
            " " + c.CreditOnHold + " " + c.Anniversary);
    }
}
```  
  
<a name="mathoperators"></a>   
## <a name="use-math-methods"></a>Math メソッドの使用  
 次のサンプルは、各種 [Math](https://msdn.microsoft.com/library/system.math.aspx) メソッドの使用方法を示します。  
  
```csharp
using (ServiceContext svcContext = new ServiceContext(_serviceProxy))
{
    var query_math = from c in svcContext.ContactSet
                  where c.ContactId != _contactId2
                  && c.Address1_Latitude != null && 
                  c.Address1_Longitude != null
                  select new
                  {
                   Round = Math.Round(c.Address1_Latitude.Value),
                   Floor = Math.Floor(c.Address1_Latitude.Value),
                   Ceiling = Math.Ceiling(c.Address1_Latitude.Value),
                   Abs = Math.Abs(c.Address1_Latitude.Value),
                  };
    foreach (var c in query_math)
    {
        System.Console.WriteLine(c.Round + " " + c.Floor + 
            " " + c.Ceiling + " " + c.Abs);
    }
}
```  
  
<a name="BKMK_UsingMultipleSelectAndWhereClauses"></a>   
## <a name="use-multiple-select-and-where-clauses"></a>複数の Select 句と Where 句の使用  
 次のサンプルは、メソッド ベースのクエリ構文を使用する複数の Select 句と Where 句を示します。  
  
```csharp
using (ServiceContext svcContext = new ServiceContext(_serviceProxy))
{
    var query_multiselect = svcContext.IncidentSet
                        .Where(i => i.IncidentId != _incidentId1)
                        .Select(i => i.incident_customer_accounts)
                        .Where(a => a.AccountId != _accountId2)
                        .Select(a => a.account_primary_contact)
                        .OrderBy(c => c.FirstName)
                        .Select(c => c.ContactId);
    foreach (var c in query_multiselect)
    {
        System.Console.WriteLine(c.GetValueOrDefault());
    }
}
```  
  
<a name="BKMK_UsingSelectMany"></a>   
## <a name="use-selectmany"></a>SelectMany の使用  
 次のサンプルは、[SelectMany メソッド](https://msdn.microsoft.com/library/system.linq.enumerable.selectmany.aspx)の使用方法を示します。  
  
```csharp
using (ServiceContext svcContext = new ServiceContext(_serviceProxy))
{
    var query_selectmany = svcContext.ContactSet
                        .Where(c => c.ContactId != _contactId2)
                        .SelectMany(c => c.account_primary_contact)
                        .OrderBy(a => a.Name);
    foreach (var c in query_selectmany)
    {
        System.Console.WriteLine(c.AccountId + " " + c.Name);    
    }
}
```
  
<a name="BKMK_UsingStringOperations"></a>   
## <a name="use-string-operations"></a>文字列操作の使用  
 次のサンプルは、各種文字列メソッドの使用方法を示します。  
  
```csharp
using (ServiceContext svcContext = new ServiceContext(_serviceProxy))
{
    var query_string = from c in svcContext.ContactSet
                    where c.ContactId == _contactId2
                    select new
                    {
                     IndexOf = c.FirstName.IndexOf("contact"),
                     Insert = c.FirstName.Insert(1, "Insert"),
                     Remove = c.FirstName.Remove(1, 1),
                     Substring = c.FirstName.Substring(1, 1),
                     ToUpper = c.FirstName.ToUpper(),
                     ToLower = c.FirstName.ToLower(),
                     TrimStart = c.FirstName.TrimStart(),
                     TrimEnd = c.FirstName.TrimEnd(),
                    };

    foreach (var c in query_string)
    {
        System.Console.WriteLine(c.IndexOf + "\n" + c.Insert + "\n" + 
            c.Remove + "\n" + c.Substring + "\n"
            + c.ToUpper + "\n" + c.ToLower + 
            "\n" + c.TrimStart + " " + c.TrimEnd);
    }
}
```
  
<a name="BKMK_UsingTwoWhereClauses"></a>   
## <a name="use-two-where-clauses"></a>2 つの Where 句の使用  
 次のサンプルは、2 つの Where 句の使用方法を示します。  
  
```csharp
using (ServiceContext svcContext = new ServiceContext(_serviceProxy))
{
    var query_twowhere = from a in svcContext.AccountSet
                      join c in svcContext.ContactSet 
                      on a.PrimaryContactId.Id equals c.ContactId
                      where c.LastName == "Smith" && c.CreditOnHold != null
                      where a.Name == "Contoso Ltd"
                      orderby a.Name
                      select a;
    foreach (var c in query_twowhere)
    {
         System.Console.WriteLine(c.AccountId + " " + c.Name);
    }
}
``` 
  
<a name="BKMK_UseLoadProperty"></a>   
## <a name="use-loadproperty-to-retrieve-related-records"></a>関連するレコードを取得するために LoadProperty を使用します。  
 次のサンプルは、関連レコードにアクセスする [Relationship)]<xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext.LoadProperty(Microsoft.Xrm.Sdk.Entity,Microsoft.Xrm.Sdk.Relationship)> の方法を示します。  
  
```csharp
Contact benAndrews = svcContext.ContactSet.Where(c => c.FullName == "Ben Andrews").FirstOrDefault();
if (benAndrews != null)
{
     //benAndrews.Contact_Tasks is null until LoadProperty is used.
     svcContext.LoadProperty(benAndrews, "Contact_Tasks");
     Task benAndrewsFirstTask = benAndrews.Contact_Tasks.FirstOrDefault();
     if (benAndrewsFirstTask != null)
     {
          Console.WriteLine("Ben Andrews first task with Subject: '{0}' retrieved.", benAndrewsFirstTask.Subject);
     }
}
```
  
