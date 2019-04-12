---
title: Web API データ操作サンプル (Common Data Service) | Microsoft Docs
description: 'Common Data Service SDK では、Web API をさまざまな異なる方法で使用する方法を示すサンプルのマトリックスが提供されます。 ここから C# および JavaScript の基本操作、クエリ データ、条件付き演算および機能およびアクションのサンプルの実装を表示します。'
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
ms.assetid: cdcb02f5-3baa-4fb7-8fb3-6fe53c2d4271
caps.latest.revision: 11
author: brandonsimons
ms.author: jdaly
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="web-api-data-operations-samples"></a>Web API データ操作のサンプル

Common Data Service Web API をさまざまなプログラミング言語やライブラリで使用できます。 本ガイドでは、Web API をさまざまな異なる方法で使用する方法を示すサンプルのマトリックスが提供されます。 このトピックでは、各グループの操作に使用できるサンプルと、さまざまな言語およびライブラリを使用してこれらの操作を実行する方法を紹介します。

<!-- TODO:
> [!NOTE]
> With the availability of the new [Xrm.WebApi](../clientapi/reference/xrm-webapi.md) client API methods, we are working on updating the client-side JavaScript samples to use the new client API methods. Check back soon.   -->
  
## <a name="web-api-sample-matrix"></a>Web API のサンプルマトリックス

次の表は、Common Data Service Web API のサンプルと言語固有の実装を示しています。  
  
|ニュートラル言語の説明|C# 実装|クライアント側の JavaScript 実装|  
|-----------------------------------|------------------------|--------------------------------------------|  
|[Web API のサンプル](web-api-samples.md) (このトピック)|[Web API のサンプル (C#)](web-api-samples-csharp.md)|[Web API のサンプル (クライアント側の JavaScript)](web-api-samples-client-side-javascript.md)|  
<!-- TODO:
|[Web API Basic Operations Sample](web-api-basic-operations-sample.md)|[Web API Basic Operations Sample (C#)](samples/basic-operations-csharp.md)|Under construction. See [Xrm.WebApi](../clientapi/reference/xrm-webapi.md)|  
|[Web API Query Data Sample](web-api-query-data-sample.md)|[Web API Query Data Sample (C#)](samples/query-data-csharp.md)|Under construction. See [Xrm.WebApi](../clientapi/reference/xrm-webapi.md)|   
|[Web API Conditional Operations Sample](web-api-conditional-operations-sample.md)|[Web API Conditional Operations Sample (C#)](samples/conditional-operations-csharp.md)|Under construction. See [Xrm.WebApi](../clientapi/reference/xrm-webapi.md)|  
|[Web API Functions and Actions Sample](web-api-functions-actions-sample.md)|[Web API Functions and Actions Sample (C#)](samples/functions-actions-csharp.md)|Under construction. See [Xrm.WebApi](../clientapi/reference/xrm-webapi.md)|  -->
  
 次の表では、示されている操作のグループと実装の問題によってサンプル トピックを分類しています。  
  
### <a name="groups-of-operations"></a>操作のグループ
 
次の表では、示されている操作グループによってサンプルを分類しています。  
  
|グループ|内容|  
|-----------|-----------------|  
|[Web API Operations 操作のサンプル](web-api-basic-operations-sample.md)|基本的な CRUD (作成、取得、更新、削除) の実行方法や関連した操作の実行方法。<br /><br /> 詳細: <br /><br /> -   [Web API を使用してエンティティを作成する](create-entity-web-api.md)<br />-   [Web API を使用してエンティティを取得する](retrieve-entity-using-web-api.md)<br />-   [Web API を使用したエンティティの更新と削除](update-delete-entities-using-web-api.md)<br />-   [Web API を使用したエンティティの関連付けと関連付け解除](associate-disassociate-entities-using-web-api.md)|  
|[Web API クエリ データのサンプル](web-api-query-data-sample.md)|基本的なクエリ要求を実行する方法。<br /><br /> 詳細: <br /><br /> -   [Web API を使用したクエリ データ](query-data-web-api.md)<br />-   [定義済みクエリの取得と実行](retrieve-and-execute-predefined-queries.md)|  
|[Web API 条件付き演算サンプル](web-api-conditional-operations-sample.md)|サーバーに含まれている、またはクライアントによって現在管理されているエンティティ レコードのバージョンに基づいて条件付きで特定の操作のカテゴリを実行する方法。 詳細: [Web API を使用する条件付き演算を実行](perform-conditional-operations-using-web-api.md)|  
|[Web API 機能およびアクションのサンプル](web-api-functions-actions-sample.md)|ユーザー定義アクションを含む、バインドされた関数とバインドされていない関数およびアクションの使用方法。<br /><br /> 詳細: <br /><br /> -   [Web API 関数の使用](use-web-api-functions.md)<br />-   [Web API アクションの使用](use-web-api-actions.md)|  
  
### <a name="language-or-library"></a>言語またはライブラリ
 
次の表では、共通言語またはライブラリ固有の実装問題に対応するトピックを示します。  
  
|言語またはライブラリ|内容|  
|-------------------------|-----------------|  
|[Web API のサンプル (C#)](web-api-samples-csharp.md)|基本的な .NET クラスと最小限のヘルパー ライブラリを使用した操作を示す C# サンプルのグループで使用される共通要素について説明します。|  
|[Web API のサンプル (クライアント側の JavaScript)](web-api-samples-client-side-javascript.md)|準備中。|  
  
### <a name="see-also"></a>関連項目

[Common Data Service Web API の使用](overview.md)<br />
[Web API Operations 操作のサンプル](web-api-basic-operations-sample.md)<br />
[Web API クエリ データのサンプル](web-api-query-data-sample.md)<br />
[Web API 条件付き演算サンプル](web-api-conditional-operations-sample.md)<br />
[Web API 機能およびアクションのサンプル](web-api-functions-actions-sample.md)<br />
[Web API のサンプル (C#)](web-api-samples-csharp.md)<br />
