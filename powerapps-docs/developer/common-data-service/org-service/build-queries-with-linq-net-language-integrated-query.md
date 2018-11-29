---
title: LINQ (.NET 統合言語クエリ) を使用してクエリを作成する (アプリ用 Common Data Service) | Microsoft Docs
description: アプリ用 Common Data Service でクエリを作成するため、.NET 統合言語クエリ (LINQ) を使用する方法をご覧ください
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
# <a name="build-queries-with-linq-net-language-integrated-query"></a>LINQ (.NET 統合言語クエリ) を使用してクエリを作成する

アプリ用 Common Data Service でクエリを作成するため、.NET 統合言語クエリ (LINQ) を使用できます。 <xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext> クラス、または CrmSvcUtil ツールによって作成された派生クラスを使用して、SOAP エンドポイント (Organization.svc) にアクセスする [LINQ](https://msdn.microsoft.com/library/bb397897.aspx) クエリを作成できます。 <xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext> クラスには、Visual C# 構文または Visual Basic .NET 構文の LINQ クエリを、アプリ用 CDS が使用するクエリ API に変換する、基になる .NET 統合言語クエリ (LINQ) クエリ プロバイダーが含まれています。  
  
 事前バインド プログラミング クラスを使用する場合は、コード生成ツール (CrmSvcUtil.exe) の使用時に **servicecontextname** パラメーターを使用してクラス名を指定すると、 <xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext> クラスの派生クラスを生成できます。 このクラスを使用すると、 `<entity schema name>+Set` というパターンを使用して [IQueryable](https://msdn.microsoft.com/library/system.linq.iqueryable.aspx) エンティティ セットを参照できます。たとえば、 **AccountSet** で `Account` エンティティ レコードのコレクションを参照できます。 アプリ用 CDS の Web サービスのサンプルはすべて、このクラスの名前として **ServiceContext** を使用していますが、異なる名前を使用することもできます。 詳細: [コード生成ツール (CrmSvcUtil.exe) を使用して事前バインド型エンティティ クラスを作成する](/dynamics365/customer-engagement/developer/org-service/create-early-bound-entity-classes-code-generation-tool.md) 
  
## <a name="in-this-section"></a>このセクションの内容  
 [LINQ を使用したクエリの構築](use-linq-construct-query.md)  
  
 [LINQ クエリでの遅延バインド エンティティ クラスの使用](use-late-bound-entity-class-linq-query.md)  
  
 [LINQ によるエンティティ検索属性の使用](order-results-entity-attributes-linq.md)  
  
 [エンティティ属性と LINQ を使用した結果の順序指定](/dynamics365/customer-engagement/developer/org-service/order-results-entity-attributes-linq)  
  
 [LINQ による大量の結果セットのページング](/dynamics365/customer-engagement/developer/org-service/page-large-result-sets-linq)  
  
 [LINQ クエリの例](/dynamics365/customer-engagement/developer/org-service/linq-query-examples)  
  
 [サンプル: LINQ クエリの作成](/dynamics365/customer-engagement/developer/org-service/sample-create-linq-query)  
  
 [サンプル: LINQ クエリの例](/dynamics365/customer-engagement/developer/org-service/sample-complex-linq-queries)  
  
 [サンプル: LINQ を使用した条件演算子による RetrieveMultiple](/dynamics365/customer-engagement/developer/org-service/sample-retrieve-multiple-with-condition-operators-using-linq)  
  
 [サンプル: その他の LINQ クエリの例](/dynamics365/customer-engagement/developer/org-service/sample-more-linq-query-examples)  
  
 [サンプル: 遅延バインドで LINQ を使用](/dynamics365/customer-engagement/developer/org-service/sample-create-linq-query-late-binding)