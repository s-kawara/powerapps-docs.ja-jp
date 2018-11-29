---
title: QueryExpression を使用したクエリの構築 (アプリ用 Common Data Service) | Microsoft Docs
description: QueryExpression クラスを使用して、データベース検索の範囲を定義した検索条件とデータ フィルターが含まれるクエリをプログラムで作成する方法をご覧ください。
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
# <a name="build-queries-with-queryexpression"></a>QueryExpression でクエリを作成する

アプリ用 Common Data Service では、<xref:Microsoft.Xrm.Sdk.Query.QueryExpression> クラスを使用して、データベース検索の範囲を定義した検索条件とデータ フィルターが含まれるクエリをプログラムで作成できます。 クエリ式は単一オブジェクトの検索に使用されます。 たとえば、ある特定の検索条件に合致するすべての取引先企業を返す検索を作成できます。 <xref:Microsoft.Xrm.Sdk.Query.QueryBase> クラスは、クエリ式の基本クラスです。 派生クラスには <xref:Microsoft.Xrm.Sdk.Query.QueryExpression> と <xref:Microsoft.Xrm.Sdk.Query.QueryByAttribute> の 2 つがあります。 `QueryExpression` クラスは、複雑なクエリをサポートします。 `QueryByAttribute` クラスでは、指定した値と属性が一致するエンティティを簡単に検索することができます。  
  
 クエリ式は <xref:Microsoft.Xrm.Sdk.IOrganizationService>.<xref:Microsoft.Xrm.Sdk.IOrganizationService.RetrieveMultiple*> など、複数のレコードを取得するメソッドで使用されます。 <xref:Microsoft.Crm.Sdk.Messages.BulkDeleteRequest> などのクエリ式で指定された結果セットで操作を実行するメッセージで、特定のレコードの ID が不明な場合のメソッド。  
  
 さらに、`Organization.QuickFindRecordLimitEnabled` という新しい組織エンティティの属性もあります。 この `Boolean` 属性が `true` の場合、簡易検索クエリに制限が適用されます。 ユーザーが十分な選択性のない検索条件を指定した場合、システムはこれを検出し、検索を停止します。 これにより、より迅速な簡易検索がサポートされ、パフォーマンスを大幅に向上させることができます。  
  
> [!WARNING]
>  パフォーマンスへの悪影響があるため、クエリの全属性を取得しないようにしてください。 これは、クエリが更新要求へのパラメーターとして使用される場合は特に true になります。 更新では、すべての属性が含まれている場合、これによりすべてのフィールド値が、変更されなくても設定されます。また、多くの場合子レコードへ更新の伝播が発生します。  
  
 アプリ用 CDS からレコードを取得するためのクエリを作成する方法は、さらに 2 つあります。 FetchXML ( 独自のアプリ用 CDS クエリ言語) を使用すると、XML ベースのクエリを使用してクエリを実行できます。 詳細については、「[FetchXMLでのクエリの作成](/dynamics365/customer-engagement/developer/org-service/build-queries-fetchxml)」を参照してください。 .NET 統合言語クエリ (LINQ) も使用してクエリを作成できます。 詳細: [LINQ (.NET 統合言語クエリ) を使用してクエリを作成する](build-queries-with-linq-net-language-integrated-query.md)。  
  
 クエリを保存するには、<xref:Microsoft.Crm.Sdk.Messages.QueryExpressionToFetchXmlRequest> を使用してクエリを FetchXML に変換し、`userquery` エンティティを使用して、それを保存されたビューとして保存します。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [QueryByAttribute クラスの使用](use-querybyattribute-class.md)  
  
 [QueryExpression クラスの使用](use-queryexpression-class.md)  
  
 [ColumnSet クラスの使用](use-the-columnset-class.md)  
  
 [ConditionExpression クラスの使用](use-conditionexpression-class.md)  
  
 [FilterExpression クラスの使用](use-filterexpression-class.md)  
  
 [左外部結合を QueryExpression で使用して "存在しない" 記録をクエリする](use-left-outer-join-queryexpression-query-records-not-in.md)  
  
 [NULL 値のテスト](/dynamics365/customer-engagement/developer/test-null-value)  
  
 [クエリ式および FetchXML による大きな結果セットのページング](page-large-result-sets-with-queryexpression.md)  
  
 [サンプル: 一対多関連付けでの取得](/dynamics365/customer-engagement/developer/org-service/sample-retrieve-with-one-to-many-relationship)  
  
 [サンプル: 属性によるクエリでの複数取得](/org-service/samples/retrieve-multiple-querybyattribute-class.md)  
  
 [サンプル: クエリ式による複数取得](/org-service/samples/retrieve-multiple-queryexpression-class.md)  
  
 [サンプル: ページング Cookie を使用した QueryExpression の使用](/dynamics365/customer-engagement/developer/org-service/sample-use-queryexpression-with-a-paging-cookie)  
  
## <a name="reference"></a>参照  
 <xref:Microsoft.Xrm.Sdk.Query.QueryBase>  
  
 <xref:Microsoft.Xrm.Sdk.Query.QueryExpression>  
  
 <xref:Microsoft.Xrm.Sdk.Query.QueryByAttribute>  
  
 <xref:Microsoft.Xrm.Sdk.IOrganizationService.RetrieveMultiple*>  
  
 <xref:Microsoft.Xrm.Sdk.Query.ColumnSet>  
  
 <xref:Microsoft.Xrm.Sdk.Query.ConditionExpression>  
  
 <xref:Microsoft.Xrm.Sdk.Query.FilterExpression>  
  
 <xref:Microsoft.Xrm.Sdk.Query.PagingInfo.PagingCookie>  
  
### <a name="see-also"></a>関連項目  
 [サンプル: Fetch と QueryExpression の間でクエリを変換する](/dynamics365/customer-engagement/developer/org-service/sample-convert-queries-fetch-queryexpression)
