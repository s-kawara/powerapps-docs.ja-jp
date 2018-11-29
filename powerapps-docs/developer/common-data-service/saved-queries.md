---
title: 保存されたクエリ (Common Data Service for Apps) | Microsoft Docs
description: CDS for Apps で保存されたクエリによって検索環境を拡張する方法について説明します。
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
# <a name="saved-queries"></a>保存済みクエリ

保存済みクエリは、Common Data Service (CDS) for Apps 環境検索のパラメーターおよび条件を定義するビジネス エンティティです。 保存済みクエリでは、複数のエンティティにまたがる検索がサポートされます。 Common Data Service (CDS) for Apps 環境に対するクエリに使用できる 2 つのエンティティがあります。  
  
- *ユーザー クエリ* (アプリケーションでは保存されているビューと呼ばれます) は、個々のユーザーによって所有され、他のユーザーに割り当てたり、他のユーザーと共有することができます。また、クエリのアクセス特権に応じて、他のユーザーがクエリを表示することもできます。 これは、頻繁に使用される、複数のエンティティの種類にまたがるクエリや、集計を実行するクエリに適しています。 詳細: [UserQuery エンティティ](reference/entities/userquery.md) 

- *保存済みクエリ* (アプリケーションではビューと呼ばれます) は、組織によって所有され、組織内のすべてのユーザーが表示できます。 保存済みクエリ (ビュー) は、エンティティおよびフィルターに定義するビューと Dynamics 365 for Outlook のテンプレートの両方に使用されます。 詳細: [SavedQuery エンティティ](reference/entities/savedquery.md) 
  
 クエリは FetchXML ステートメントの形式で作成され、`UserQuery.FetchXml` 属性に割り当てられます。 このクエリを実行するには、<xref:Microsoft.Crm.Sdk.Messages.ExecuteByIdUserQueryRequest> メッセージを使用します。  
  
 ユーザー クエリは、モデル駆動型アプリの **高度な検索** セクションおよびエンティティの **ビュー** ドロップダウン リストで確認できます。  **高度な検索**ダイアログ ボックスで **Fetch XML のダウンロード**ボタンを使用して、 `UserQuery.FetchXml` 属性の値をエクスポートできます。  
  
## <a name="use-web-api-to-execute-saved-queries"></a>Web API を使って保存済みクエリを実行する

Web API を使用してユーザー クエリとおよび保存済みクエリを実行する方法については、[定義済みクエリの取得と実行](webapi/retrieve-and-execute-predefined-queries.md)を参照してください

## <a name="use-organization-service-to-execute-saved-queries"></a>組織サービスを使用して保存済みクエリを実行する

<xref:Microsoft.Crm.Sdk.Messages.ExecuteByIdUserQueryRequest> および <xref:Microsoft.Crm.Sdk.Messages.ExecuteByIdSavedQueryRequest> メッセージを使用して、それぞれユーザー クエリおよび保存済みクエリを実行できます。
