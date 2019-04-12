---
title: Common Data Service のコードを使用したデータに関する作業 (PowerApps) | Microsoft Docs
description: 'Common Data Service は、データと対話するために使用できる 2 つの Web サービス: Web API と組織サービスを提供します。'
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: JimDaly
ms.author: jdaly
manager: ryjones
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="work-with-data-using-code-in-common-data-service"></a>Common Data Service のコードを使用したデータに関する作業

Common Data Service には、ビジネス データをモデル化して管理するために使用される [エンティティ](entities.md) があります。 標準のエンティティを使用することも、データを格納するために、独自のユーザー定義エンティティを作成することもできます。 

## <a name="use-web-services-to-work-with-data"></a>Web サービスを使用したデータとの連携

Common Data Service は、データと対話するために使用できる 2 つの Web サービス: **Web API** と**組織サービス**を提供します。 要件とスキルが最高に一致したものを選択します。 

![Webサービスを選択するための流れ図](media/whentousewebapi.png)

### <a name="web-api"></a>Web API

Web API は OData v4 RESTful エンドポイントです。 これは、OAuth 2.0 を使用してHTTP要求および認証をサポートする任意のプログラミング言語用に使用します。

詳細: [Common Data Service Web API の使用](webapi/overview.md) 

### <a name="organization-service"></a>組織のサービス

プラグインまたはワークフローの拡張機能の記述を含むプロジェクト用に .NET Framework SDK アセンブリを使用します。 

詳細: [Common Data Service 組織サービスの使用](org-service/overview.md)

> [!NOTE]
> Windows クライアント アプリケーションを作成している場合は、Xrm.Tooling アセンブリを使用します。 詳細情報: [XRM ツールを使用して Windows のクライアント アプリケーションを作成する](xrm-tooling/build-windows-client-applications-xrm-tools.md)
