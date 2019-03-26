---
title: 'プレビュー機能: アプリ用 Common Data Service で Azure Cosmos DB for SQL API データ プロバイダーを使用する | MicrosoftDocs'
description: Azure Cosmos DB for SQL API データ プロバイダーを構成して仮想エンティティで使用する方法について説明します。
keywords: SQL API
ms.date: 02/15/2019
ms.service: crm-online
ms.custom: null
ms.topic: article
applies_to:
  - Dynamics 365 (online)
  - Dynamics 365 Version 9.x
  - powerapps
ms.assetid: d0031ffc-8754-4a12-b8c1-e08edc49ff73
author: Mattp123
ms.author: matp
manager: kvivek
ms.reviewer: null
ms.suite: null
ms.tgt_pltfrm: null
caps.latest.revision: null
topic-status: Drafting
search.audienceType:
  - maker
search.app:
  - PowerApps
  - D365CE
---

# <a name="preview-feature-azure-cosmos-db-sql-api-data-provider-requirements"></a>プレビュー機能: Azure Cosmos DB SQL API データ プロバイダーの要件

このトピックでは、SQL API データ プロバイダーの Azure Cosmos DB の要件、および仮想エンティティが含まれる SQL API データ プロバイダー用に Azure Cosmos DB を使用するときに推奨されるベスト プラクティスを構成する方法について説明します。 

> [!IMPORTANT]
> - [!INCLUDE [cc-preview-features-definition](../../includes/cc-preview-features-definition.md)]
> - [!INCLUDE [cc-preview-features-definition](../../includes/cc-preview-features-expect-changes.md)]
> - [!INCLUDE [cc-preview-features-definition](../../includes/cc-preview-features-no-ms-support.md)]


## <a name="what-is-azure-cosmos-db"></a>Azure Cosmos DB とは

Azure Cosmos DB は、ミッションクリティカルなアプリケーションのための Microsoft のグローバル分散マルチモデル データベース サービスです。 これは、スキーマのない JSON データ全体で豊富でよく知られた SQL クエリ機能に一貫性のある低遅延を提供します。 詳細: [Azure Cosmos DBの概要: SQL API](https://docs.microsoft.com/azure/cosmos-db/sql-api-introduction)

## <a name="requirements"></a>要件

- Azure Cosmos DB を含む Azure サブスクリプション。
- Azure Cosmos DB SQL API コレクション。
- Azure Cosmos DB データベースの種類は SQL でなければなりません。 

## <a name="data-type-mapping"></a>データの種類のマッピング

次の JSON 構造を持つ*受注*という名前のコレクションに Azure Cosmos DB ドキュメントがあるとします。

![SQL API ドキュメント用の JSON の例。](media/documentdbexample.png)

この表に、*受注* コレクション内の SQL API ドキュメントの、アプリ用 Common Data Service を用いたデータ タイプ マッピングを示します。

|SQL API データ|アプリ用 CDS|
|--|--|
|`id`|主キー|
|`name`|1 行テキスト|
|`quantity`|整数|
|`orderid`|1 行テキスト|
|`ordertype`|[オプション セット]|
|`amount`|少数または通貨|
|`delivered`|2 つのオプション|
|`datetimeoffset`|日付と時間|

> [!NOTE]
> - アンダースコア (_) 接頭辞の付いた属性は、SQL API によって生成されます。
> - SQL API ドキュメントで任意として構成され、アプリ用 CDS で**必須項目**としてマップされている属性は、ランタイム エラーが発生する原因になります。
> - ID 属性値は GUID である必要があります。
> - SQL API での日付の使用方法の詳細については、「[Azure Cosmos DB での日付の操作](https://azure.microsoft.com/blog/working-with-dates-in-azure-documentdb-4/)」を参照してください。

## <a name="supported-sql-query-filtering"></a>サポートされる SQL クエリのフィルター処理

SQL クエリのフィルター処理は次の演算子をサポートします。 

- 比較演算子:`<`、`>`、`<=`、`>=`、`!=`
- 論理演算子: `and`、`or` 
- 集合演算子: `in`、`not in`
- 文字列演算子: `like`、`contains`、b`egins with`、`ends with`

> [!NOTE]
> like 演算子の使用は、同等の `contains`/`begins with`/`ends with` 演算子に変換されます。 SQL API は、トピック「[類似 (Transact-SQL)](/sql/t-sql/language-elements/like-transact-sql)」で説明されているパターン引数をサポートしません。 Azure Cosmos DB for SQL API データ プロバイダーは、単一の特殊なケース `Like('[aA]%')` を `BeginsWith('a')` または `BeginsWith('A')` に変換できます。 SQL API の文字列比較は、大文字と小文字が区別されることに注意してください。

## <a name="add-a-data-source-using-the-azure-cosmos-db-for-sql-api-data-provider"></a>Azure Cosmos DB for SQL API データ プロバイダーを使用してデータ ソースを追加する

1. [AppSource](https://appsource.microsoft.com/product/dynamics-365/mscrm.documentdb_data_provider?tab=Overview) に移動して、**今すぐ取得**を選択し、指示に従って v9x 以降を使用するの環境にアプリケーションを追加します。
2. ソリューションがインストールされた後に、 環境サインインし、**設定** > **管理** > **仮想エンティティ データ ソース**の順に移動します。
3. 操作ツール バーで**新規**を選択して、**データ プロバイダーの選択**ダイアログ ボックスで **Azure Cosmos DB for SQL API データ プロバイダー**を選択し、**OK** を選択します。
![Azure Cosmos DB for SQL API データ プロバイダーを選択します。](media/createdatasource.png)
1. 以下の情報を入力し、**保存して閉じる**を選択します。

    |フィールド|説明|
    |--|--|
    |**名前**|データ ソースを説明する名前を入力します。|
    |**コレクション名**|仮想エンティティで公開するコレクションを含む Azure Cosmos DB *データベース* コレクションの名前。  |
    |**認証キー**|Azure Cosmos DB アカウントの主キーまたは予備キー。 Azure Cosmos DB アカウントのキー設定の下にある Azure 管理用ポータルから**キー**を見つけることができます。|
    |**Uri**|Azure Cosmos DB コレクションがあるリソース グループの URI。 URI は `https://contoso/documents.azure.com:443` と同様に作成されます。 Azure Cosmos DB アカウントのキー設定の下にある Azure 管理用ポータルから **URI** を見つけることができます。 |
    |**タイムアウト (秒)**|データ リクエストがタイムアウトする前に Azure Cosmos DB サービスからの応答を待機する時間を秒数で入力します。たとえば、タイムアウトが発生する前に最大 30 秒待つには、30 を入力します。 既定のタイムアウトは 120 秒です。|

    > [!div class="mx-imgBorder"] 
    > ![SQL API データ プロバイダーを使用してデータ ソースを作成します。](media/cosmosdb-datasource.png)

## <a name="best-practices-and-limitations"></a>ベスト プラクティスと制限

- Azure Cosmos DB をデータ ソースとして使用するときは、以下に注意します。
   - 各 Azure Cosmos DB データ ソースは、1 つの仮想エンティティにのみ関連付けることができます。
   - 複数のデータ ソースを Azure Cosmos DB 内の同じコレクションに接続できます。
- コレクション内のデータをエンティティでセグメント化できません。
- Azure Cosmos DB データベースはスキーマを必要としませんが、Azure Cosmos DB 内のデータは予測可能なスキーマを使用して構造化する必要があります。 
- Azure Cosmos DB for SQL API データ プロバイダーは、プロジェクション、フィルター処理、および並べ替え演算子を実装しますが、結合処理はサポートしません。
- SQL API では、単一の列によってのみフィルタ処理できます。

## <a name="see-also"></a>関連項目

[外部データ ソースからのデータを格納する仮想エンティティの作成および編集](create-edit-virtual-entities.md)
