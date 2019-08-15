---
title: QueryExpression を使用してクエリを作成する (Common Data Service) | Microsoft Docs
description: QueryExpression クラスを使用して、データベース検索の範囲を定義した検索条件とデータ フィルターが含まれるクエリをプログラムで作成する方法をご覧ください。
ms.custom: ''
ms.date: 06/25/2019
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

Common Data Service では、<xref:Microsoft.Xrm.Sdk.Query.QueryExpression> クラスを使用して、データベース検索の範囲を定義した検索条件とデータ フィルターが含まれるクエリをプログラムで作成できます。 クエリ式は単一オブジェクトの検索に使用されます。 たとえば、ある特定の検索条件に合致するすべての取引先企業を返す検索を作成できます。 <xref:Microsoft.Xrm.Sdk.Query.QueryBase> クラスは、クエリ式の基本クラスです。 次の3つの派生するクラスがあります: <xref:Microsoft.Xrm.Sdk.Query.QueryExpression>、 <xref:Microsoft.Xrm.Sdk.Query.QueryByAttribute> 、 <xref:Microsoft.Xrm.Sdk.Query.FetchExpression>です `QueryExpression` クラスは、複雑なクエリをサポートします。 `QueryByAttribute` クラスでは、指定した値と属性が一致するエンティティを簡単に検索することができます。 

> [!NOTE]
> 3つめのクラス `FetchExpression` は、独自の Common Data Service クエリ言語であるFetchXMLとともに使用され、XMLベースのクエリーを使用して複数のクエリを実行することが可能です。 詳細: [FetchXML の使用によるクエリの作成](../use-fetchxml-construct-query.md)
  
クエリ式は <xref:Microsoft.Xrm.Sdk.IOrganizationService>.<xref:Microsoft.Xrm.Sdk.IOrganizationService.RetrieveMultiple*> など、複数のレコードを取得するメソッドで使用されます。 <xref:Microsoft.Crm.Sdk.Messages.BulkDeleteRequest> などのクエリ式で指定された結果セットで操作を実行するメッセージで、特定のレコードの ID が不明な場合のメソッド。  

> [!WARNING]
>  パフォーマンスへの悪影響があるため、クエリの全属性を取得しないようにしてください。 これは、クエリが更新要求へのパラメーターとして使用される場合は特に true になります。 更新では、すべての属性が含まれている場合、これによりすべてのフィールド値が、変更されなくても設定されます。また、多くの場合子レコードへ更新の伝播が発生します。

クエリを節約し再利用をするには、 <xref:Microsoft.Crm.Sdk.Messages.QueryExpressionToFetchXmlRequest> を使用してFetchXMLに変換し、保存されたクエリとして保存しておくことが可能です。 詳細: [保存済みクエリ](../saved-queries.md) 
 
## <a name="alternatives-to-queryexpression"></a>QueryExpression の代替

Common Data Service からレコードを取得するためのクエリを作成する方法は、さらに 2 つあります。 

- FetchXML (Common Data Service 独自のクエリ言語) を使用すると、XML ベースのクエリを使用してクエリを実行できます。 詳細情報は次を参照してください: [FetchXMLを使用してクエリを作成する](../use-fetchxml-construct-query.md) 
- .NET 統合言語クエリ (LINQ) 詳細: [LINQ (.NET 統合言語クエリ) を使用してクエリを作成する](build-queries-with-linq-net-language-integrated-query.md)。  

<!-- This doesn't belong here. It should be in model driven app configuration -->
## <a name="configuration-for-quick-find"></a>クイック検索の設定

モデル駆動型アプリには、クイック検索機能が実装されています。 ユーザーが十分な選択性のない検索条件を指定した場合、システムはこれを検出し、検索を停止します。 これにより、より迅速な簡易検索がサポートされ、パフォーマンスを大幅に向上させることができます。 [組織 エンティティ QuickFindRecordLimitEnabled](/powerapps/developer/common-data-service/reference/entities/organization#BKMK_QuickFindRecordLimitEnabled) 属性にて管理されています。 この `Boolean` 属性の値が `true` の場合、クイック検索のクエリには制限があります。

## <a name="in-this-section"></a>このセクションの内容

[QueryByAttribute クラスの使用](use-querybyattribute-class.md)<br />
[QueryExpression クラスの使用](use-queryexpression-class.md)<br />
[ColumnSet クラスの使用](use-the-columnset-class.md)<br />
[ConditionExpression クラスの使用](use-conditionexpression-class.md)<br />
[FilterExpression クラスの使用](use-filterexpression-class.md)<br />
[左外部結合を QueryExpression で使用して "存在しない" 記録をクエリする](use-left-outer-join-queryexpression-query-records-not-in.md)<br />
[NULL 値のテスト](/dynamics365/customer-engagement/developer/test-null-value)<br />
[クエリ式および FetchXML による大きな結果セットのページング](page-large-result-sets-with-queryexpression.md)<br />
[サンプル: 一対多関連付けでの取得](/dynamics365/customer-engagement/developer/org-service/sample-retrieve-with-one-to-many-relationship)<br />
[サンプル: 属性によるクエリでの複数取得](/org-service/samples/retrieve-multiple-querybyattribute-class.md)<br />
[サンプル: クエリ式による複数取得](/org-service/samples/retrieve-multiple-queryexpression-class.md)<br />
[サンプル: ページング Cookie を使用した QueryExpression の使用](/dynamics365/customer-engagement/developer/org-service/sample-use-queryexpression-with-a-paging-cookie)  
  
## <a name="reference"></a>参照

<xref:Microsoft.Xrm.Sdk.Query.QueryBase><br />
<xref:Microsoft.Xrm.Sdk.Query.QueryExpression><br />
<xref:Microsoft.Xrm.Sdk.Query.QueryByAttribute><br />
<xref:Microsoft.Xrm.Sdk.IOrganizationService.RetrieveMultiple*><br />
<xref:Microsoft.Xrm.Sdk.Query.ColumnSet><br />
<xref:Microsoft.Xrm.Sdk.Query.ConditionExpression><br />
<xref:Microsoft.Xrm.Sdk.Query.FilterExpression><br />
<xref:Microsoft.Xrm.Sdk.Query.PagingInfo.PagingCookie><br />
  
### <a name="see-also"></a>関連項目

[サンプル: Fetch と QueryExpression の間でクエリを変換する](/dynamics365/customer-engagement/developer/org-service/sample-convert-queries-fetch-queryexpression)
