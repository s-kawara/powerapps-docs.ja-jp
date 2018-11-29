---
title: アプリ用 Common Data Service Web サービスでの認証 (アプリ用 Common Data Service) | Microsoft Docs
description: 使用するソフトウェア フレームワークに依存する認証オプションを紹介します。
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: paulliew
ms.author: jdaly
manager: ryjones
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="authentication-with-common-data-service-for-apps-web-services"></a>アプリ用 Common Data Service Web サービスでの認証

アプリ Web サービス用 CDS を使用するクライアント アプリケーションを作成する場合、データへアクセスできるようにするための認証が必要です。 認証方法は、使用するソフトウェア フレームワークと、接続する Web サービスによって異なります。

## <a name="net-framework-applications"></a>.NET Framework アプリケーション

クライアント アプリケーションが .NET Framework を使用する場合、2 つのバージョンがあります。

- OAuth
- Office 365

### <a name="oauth"></a>OAuth

OAuthは、OData RESTful Web サービス (Web API および OData グローバル検索サービス) および SOAP Web サービス (組織サービスおよび探索サービス) の*両方*へのアクセスを提供するため、認証に適した手段です。 

OAuth は以下のものをサポートすることも必要です。 
 - 2 要素認証 (2FA) などの条件付きアクセスに対する Azure Active Directory の構成
 - サーバー間認証シナリオを有効にするクライアント シークレットを使用する
 - Single Page Application (SPA) に接続するクロス オリジン リソース共有 (CORS)

詳細: [アプリ用 Common Data Service で OAuth を使用する](authenticate-oauth.md)

### <a name="office-365"></a>Office 365

Office 365 認証では、SOAP Web サービスのみで .NET Framework SDK アセンブリを使用する必要があります。

Office 365 認証を使用する場合、OAuth で行うようにアプリケーションを登録する必要はありません。 有効なユーザーに対して、ユーザー プリンシパル名 (UPN) およびパスワードを単に提供する必要があります。

詳細: [.NET Framework アプリケーションでの認証](authenticate-dot-net-framework.md)

## <a name="all-other-software-frameworks"></a>他のすべてのソフトウェア フレームワーク

.NET Framework 以外を使用している場合は、OAuth を使用して認証し、OData RESTful Web サービス (Web API および OData グローバル検索サービス) を使用する必要があります。

詳細: [アプリ用 Common Data Service で OAuth を使用する](authenticate-oauth.md)
