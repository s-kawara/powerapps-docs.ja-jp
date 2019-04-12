---
title: LINQ クエリと共に遅延バインド型エンティティ クラスを使用する (Common Data Service) | Microsoft Docs
description: .NET 統合言語クエリ (LINQ) で遅延バインドを使用する方法について説明します
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
# <a name="use-late-bound-entity-class-with-a-linq-query"></a>LINQ クエリでの遅延バインド エンティティ クラスの使用

Common Data Service では、.NET 統合言語クエリ (LINQ) と共に遅延バインドを使用することができます。 遅延バインドは属性の論理名を使用し、そのため、実行時に解決されます。  
  
<a name="usinglatebindingjoin"></a>   

## <a name="using-late-binding-in-a-join-clause"></a>Join (結合) 句での遅延バインドの使用  

 次のサンプルは、LINQ クエリの `join` 句での遅延バインドの使い方を示しています。  
  
 取引先企業の取引先責任者を表す取引先担当者の氏名と取引先企業名を取得する。  
  
 ```csharp
 using (OrganizationServiceContext orgSvcContext = new OrganizationServiceContext(_serviceProxy))
{
 var query_join2 = from c in orgSvcContext.CreateQuery("contact")
                   join a in orgSvcContext.CreateQuery("account")
                   on c["contactid"] equals a["primarycontactid"]
                   select new
                   {
                    contact_name = c["fullname"],
                    account_name = a["name"]
                   };
 foreach (var c in query_join2)
 {
  System.Console.WriteLine(c.contact_name + "  " + c.account_name);
 }
}
 ```
 取引先担当者、取引先企業、および潜在顧客 (この潜在顧客が元の潜在顧客で、取引先担当者の姓が "Parker" でない) のデータを取得する。  
  
 ```csharp
 using (OrganizationServiceContext orgSvcContext = new OrganizationServiceContext(_serviceProxy))
{
 var query_dejoin = from c in orgSvcContext.CreateQuery("contact")
                    join a in orgSvcContext.CreateQuery("account") 
                    on c["contactid"] equals a["primarycontactid"]
                    join l in orgSvcContext.CreateQuery("lead") 
                    on a["originatingleadid"] equals l["leadid"]
                    where (string)c["lastname"] != "Parker"
                    select new { Contact = c, Account = a, Lead = l };
 foreach (var c in query_dejoin)
 {
  System.Console.WriteLine(c.Account.Attributes["name"] + " " + 
   c.Contact.Attributes["fullname"] + " " + c.Lead.Attributes["leadid"]);
 }
}
 ```
<a name="Usinglatebindingleft"></a>   

## <a name="using-late-binding-in-a-left-join"></a>左結合での遅延バインドの使用  

 次の例では、左結合を使用して、取引先担当者と取引先企業の一覧を取得する方法について説明します。 左結合は、2 つのソースから子を持つ親と持たない親を返します。 親と子の間に関連付けがありますが、実際に子が存在するとは限りません。  
  
 ```csharp
 using (OrganizationServiceContext orgSvcContext = new OrganizationServiceContext(_serviceProxy))
{
 var query_join9 = from a in orgSvcContext.CreateQuery("account")
                   join c in orgSvcContext.CreateQuery("contact") 
                   on a["primarycontactid"] equals c["contactid"] into gr
                   from c_joined in gr.DefaultIfEmpty()
                   select new
                   {
                    account_name = a.Attributes["name"]
                   };
 foreach (var c in query_join9)
 {
  System.Console.WriteLine(c.account_name);
 }
}
 ```
<a name="contains"></a>   

## <a name="using-late-binding-and-the-contains-method"></a>遅延バインドと Contains メソッド  

 次の例は、LINQ クエリの `Contains` メソッドでの遅延バインドの使い方を示しています。  
  
 ```csharp
 using (OrganizationServiceContext orgSvcContext = new OrganizationServiceContext(_serviceProxy))
{
 var query_contains3 = from c in orgSvcContext.CreateQuery("contact")
                       where ((string)c["description"]).Contains("Coho")
                       select new
                       {
                        firstname = c.Attributes["firstname"],
                        lastname = c.Attributes["lastname"]
                       };
 foreach (var c in query_contains3)
 {
  System.Console.WriteLine(c.firstname + " " + c.lastname);
 }
}
 ```
 <a name="notequals"></a>   

## <a name="using-late-binding-and-not-equals-operator"></a>遅延バインドと不等演算子  

 次の例では、不等号演算子の使用方法について説明します。  
  
 ```csharp
using (OrganizationServiceContext orgSvcContext = new OrganizationServiceContext(_serviceProxy))
{
 var query_ne3 = from c in orgSvcContext.CreateQuery("contact")
                 where !c["address1_city"].Equals(null)
                 select new
                 {
                  FirstName = c["firstname"],
                  LastName = c["lastname"],
                  Address1_City = c["address1_city"]
                 };
 foreach (var c in query_ne3)
 {
  System.Console.WriteLine(c.FirstName + " " + 
   c.LastName + " " + c.Address1_City);
 }
}
```

 <a name="getattribute"></a>   

## <a name="using-the-getattributevalue-method"></a>GetAttributeValue メソッドの使用  

 次の例では、`GetAttributeValue` メソッドを使用して取引先担当者情報を取得する方法について説明します。  
  
 ```csharp
using (OrganizationServiceContext orgSvcContext = new OrganizationServiceContext(_serviceProxy))
{

 var list_getattrib1 = (from c in orgSvcContext.CreateQuery("contact")
                        where c.GetAttributeValue<Guid?>("contactid") != _contactId1
                        select new { 
                         FirstName = c.GetAttributeValue<string>("firstname"), 
                         LastName = c.GetAttributeValue<string>("lastname") 
                        }).ToList();
 foreach (var c in list_getattrib1)
 {
  System.Console.WriteLine(c.FirstName + " " + c.LastName);
 }
}
```
  
### <a name="see-also"></a>関連項目  
 [LINQ (.NET Language-Integrated Query) を使用してクエリを作成する](build-queries-with-linq-net-language-integrated-query.md)   
 [エンティティ属性と LINQ を使用した結果の順序指定](order-results-entity-attributes-linq.md)   
 <xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext.CreateQuery``1>