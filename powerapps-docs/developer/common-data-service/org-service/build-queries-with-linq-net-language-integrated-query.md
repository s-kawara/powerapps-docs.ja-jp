---
title: LINQ を使用してクエリを作成する (.NET 統合言語クエリ) (Common Data Service) | Microsoft Docs
description: .NET 統合言語クエリ (LINQ) の使用方法を確認し、 Common Data Service でクエリを作成する。
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

.NET 統合言語クエリ (LINQ) を使うことで、 Common Data Service にてクエリを作成することができます。 <xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext> クラス、または CrmSvcUtil ツールによって作成された派生クラスを使用して、SOAP エンドポイント (Organization.svc) にアクセスする [LINQ](https://msdn.microsoft.com/library/bb397897.aspx) クエリを作成できます。 <xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext> クラスにはLINQクエリ プロバイダが備わっており、これによってLINQクエリを Visual C#または Visual Basic .NET 構文から Common Data Serviceが使用するクエリAPIに変換することができます。  
  
 事前バインド プログラミング クラスを使用する場合は、コード生成ツール (CrmSvcUtil.exe) の使用時に **servicecontextname** パラメーターを使用してクラス名を指定すると、 <xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext> クラスの派生クラスを生成できます。 このクラスを使用すると、 `<entity schema name>+Set` というパターンを使用して [IQueryable](https://msdn.microsoft.com/library/system.linq.iqueryable.aspx) エンティティ セットを参照できます。たとえば、 **AccountSet** で `Account` エンティティ レコードのコレクションを参照できます。 Common Data Service ウェブサービスに含まれるすべてのサンプルは、このクラスの名前として **ServiceContext** を使用していますが、コードでは別の名前を使用することも可能です。 詳細については次を参照してください: [組織サービスの事前バインドクラスを生成する](generate-early-bound-classes.md)
  
### <a name="see-also"></a>関連項目

 [LINQ を使用したクエリの構築](use-linq-construct-query.md)  
  
 [LINQ クエリでの遅延バインド エンティティ クラスの使用](use-late-bound-entity-class-linq-query.md)  
  
 [LINQ によるエンティティ検索属性の使用](order-results-entity-attributes-linq.md)  

 [LINQ クエリの例](linq-query-examples.md)