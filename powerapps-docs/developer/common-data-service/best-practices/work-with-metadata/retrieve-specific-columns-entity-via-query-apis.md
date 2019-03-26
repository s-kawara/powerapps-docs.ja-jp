---
title: クエリ API によってエンティティの特定の列を取得します。_=_ MicrosoftDocs
description: データを取得するために送信されたクエリには、All Columns ではなく、クエリに関連付けられている ColumnSet のインスタンス内の特定の列を含める必要があります。
services: ''
suite: powerapps
documentationcenter: na
author: jowells
manager: austinj
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/12/2018
ms.author: jowells
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
--- 
# <a name="do-not-retrieve-entity-all-columns-via-query-apis"></a>クエリ API を使用してエンティティのすべての列を取得することはできません

**カテゴリ**: パフォーマンス

**影響の可能性**: 高い

<a name='symptoms'></a>

## <a name="symptoms"></a>現象

すべての列を取得すると、次のことが発生する可能性があります:

- 取得するデータの量によって起こるパフォーマンスの問題
- 意図しないプラグイン/プロセス実行

<a name='guidance'></a>

## <a name="guidance"></a>ガイダンス

最良のパフォーマンスを得るためには、アプリ用 Common Data Service のクエリを実行時に、アプリケーション サービスと呼ばれるデータを使用して必要なデータの最小金額を選択する必要があります。 

### <a name="columnset-parameter"></a>ColumnSet パラメーター

<xref:Microsoft.Xrm.Sdk.IOrganizationService>.<xref:Microsoft.Xrm.Sdk.IOrganizationService.Retrieve*> メソッドを使う時、指定したインスタンスに <xref:Microsoft.Xrm.Sdk.Query.ColumnSet> 列の `columnSet` パラメーターを設定します。  <xref:Microsoft.Xrm.Sdk.Query.QueryExpression> セットを使う時、<xref:Microsoft.Xrm.Sdk.Query.QueryExpression.ColumnSet> の必要な属性のプロパティを使用します。

以下はその例です。

- [ColumnSet (文字列パラメーター[] の列)](/dotnet/api/microsoft.xrm.sdk.query.columnset.-ctor#Microsoft_Xrm_Sdk_Query_ColumnSet__ctor_System_String___) <xref:Microsoft.Xrm.Sdk.Query.QueryExpression> のコンストラクター オーバーロード。

    ```csharp
        var query = new QueryExpression("account")
        {
            ColumnSet = new ColumnSet("name", "address1_city")
        };

        var results = service.RetrieveMultiple(query);
    ```

- [ColumnSet (文字列パラメーター[] の列)](/dotnet/api/microsoft.xrm.sdk.query.columnset.-ctor#Microsoft_Xrm_Sdk_Query_ColumnSet__ctor_System_String___) <xref:Microsoft.Xrm.Sdk.Messages.RetrieveRequest> のコンストラクター オーバーロード。

    ```csharp
        var entity = service.Retrieve("account", Guid.NewGuid(), new ColumnSet("name", "address1_city"));
    ```

- <xref:Microsoft.Xrm.Sdk.Query.ColumnSet> <xref:Microsoft.Xrm.Sdk.Query.ColumnSet.AddColumn(System.String)> メソッドの呼び出し。

    ```csharp
        var query = new QueryExpression("account");
        query.ColumnSet.AddColumn("name");
        query.ColumnSet.AddColumn("address1_city");

        var results = service.RetrieveMultiple(query);
    ```

- <xref:Microsoft.Xrm.Sdk.Query.ColumnSet> <xref:Microsoft.Xrm.Sdk.Query.ColumnSet.AddColumns(System.String[])> メソッドの呼び出し。

    ```csharp
        var query = new QueryExpression("account");
        query.ColumnSet.AddColumns("name", "address1_city");

        var results = service.RetrieveMultiple(query);
    ```

以下のクラスは <xref:Microsoft.Xrm.Sdk.Query.ColumnSet> インスタンスを含みます。

- <xref:Microsoft.Crm.Sdk.Messages.ConvertQuoteToSalesOrderRequest>
- <xref:Microsoft.Crm.Sdk.Messages.GenerateInvoiceFromOpportunityRequest>
- <xref:Microsoft.Crm.Sdk.Messages.GenerateQuoteFromOpportunityRequest>
- <xref:Microsoft.Crm.Sdk.Messages.GenerateSalesOrderFromOpportunityRequest>
- <xref:Microsoft.Crm.Sdk.Messages.RetrieveAllChildUsersSystemUserRequest>
- <xref:Microsoft.Crm.Sdk.Messages.RetrieveBusinessHierarchyBusinessUnitRequest>
- <xref:Microsoft.Crm.Sdk.Messages.RetrieveMembersTeamRequest>
- <xref:Microsoft.Xrm.Sdk.Messages.RetrieveRequest>
- <xref:Microsoft.Crm.Sdk.Messages.RetrieveSubsidiaryTeamsBusinessUnitRequest>
- <xref:Microsoft.Crm.Sdk.Messages.RetrieveSubsidiaryUsersBusinessUnitRequest>
- <xref:Microsoft.Crm.Sdk.Messages.RetrieveTeamsSystemUserRequest>
- <xref:Microsoft.Crm.Sdk.Messages.RetrieveUnpublishedRequest>
- <xref:Microsoft.Crm.Sdk.Messages.RetrieveUserSettingsSystemUserRequest>
- <xref:Microsoft.Crm.Sdk.Messages.ReviseQuoteRequest>
- <xref:Microsoft.Crm.Sdk.Messages.SearchByBodyKbArticleRequest>
- <xref:Microsoft.Xrm.Sdk.IOrganizationService>.<xref:Microsoft.Xrm.Sdk.IOrganizationService.Retrieve*>
- <xref:Microsoft.Xrm.Sdk.Query.QueryExpression>

<a name='problem'></a>

## <a name="problematic-patterns"></a>問題となるパターン

<xref:Microsoft.Xrm.Sdk.Query.ColumnSet.AllColumns> プロパティが  `true` である定義済みの <xref:Microsoft.Xrm.Sdk.Query.ColumnSet> を含むクエリは、SQL を発行するようにプラットフォームに指示します。 クエリプランに含まれるすべての物理データに対して ["選択 *"](https://technet.microsoft.com/library/ms189287.aspx) にコマンドを入力します。  このシナリオは回避する必要があります。

> [!WARNING]
> これらのシナリオを回避する必要があります。

- <xref:Microsoft.Xrm.Sdk.Query.ColumnSet> <xref:Microsoft.Xrm.Sdk.Query.ColumnSet.AllColumns> セッターのメソッド呼び出し。

    ```csharp
        var columns = new ColumnSet();
        columns.AllColumns = true;

        var query = new QueryExpression("account");
        query.ColumnSet = columns;

        var results = service.RetrieveMultiple(query);
    ```

- [ColumnSet (allColumns ブール値)](/dotnet/api/microsoft.xrm.sdk.query.columnset.-ctor#Microsoft_Xrm_Sdk_Query_ColumnSet__ctor_System_Boolean_)  コンストラクター オーバーロード。

    ```csharp
        var query = new QueryExpression("account")
        {
            ColumnSet = new ColumnSet(true)
        };

        var results = service.RetrieveMultiple(query);
    ```

-  <xref:Microsoft.Xrm.Sdk.Messages.RetrieveRequest> の [ColumnSet (allColumns ブール値)](/dotnet/api/microsoft.xrm.sdk.query.columnset.-ctor#Microsoft_Xrm_Sdk_Query_ColumnSet__ctor_System_Boolean_)  コンストラクター オーバーロード。

    ```csharp
        var entity = service.Retrieve("account", Guid.Parse("bec45132-392a-4617-b935-a64ef04738e4"), new ColumnSet(true));
    ```

<a name='additional'></a>

## <a name="additional-information"></a>追加情報

Dynamics 365 からデータを取得するために実行されたクエリは、すべての列を選択する必要があります。  特定のサーバーの役割を個々の列の場合は、クエリに関連付けられた <xref:Microsoft.Xrm.Sdk.Query.ColumnSet> インスタンスを指定してください。 エンティティのすべての列を検索するとパフォーマンスに悪い影響を与える可能性があります。 加えて、作業していない列を検索して更新プログラムを出すことによって、意図せずにプラグイン登録イベントをトリガーすることがあります。

<a name='seealso'></a>

### <a name="see-also"></a>関連項目

<xref href="Microsoft.Xrm.Sdk.Query.ColumnSet?text=ColumnSet Class" /><br />
[ColumnSet クラスの使用](../../org-service/use-the-columnset-class.md)<br />
[QueryExpression でクエリを作成する](../../org-service/build-queries-with-queryexpression.md)<br />