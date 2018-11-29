---
title: クライアント アプリケーションの作成 (アプリ用 Common Data Service) | Microsoft Docs
description: コードを使用して、アプリ用 CDS に接続するカスタム クライアント アプリケーションを作成するために必要な概念を紹介します。
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
# <a name="create-client-applications"></a>クライアント アプリケーション作成

キャンバスおよびモデル駆動型アプリを使用して、コードの記述なしでクライアント アプリケーションを作成できます。
詳細: [PowerApps でのアプリの作成の概要](../../maker/index.md)

PowerApps オプションが要件を満たさない場合、コードを使用してクライアント アプリケーションを作成できます。

## <a name="connecting-to-cds-for-apps"></a>アプリ用 CDS への接続

アプリ用 CDS 環境に接続するには、環境への URL およびその環境にアクセスできるユーザー アカウントの資格情報が必要です。 使用する戦略は、この情報があるかどうか、またはアプリケーションのユーザーからこの情報を取得する必要があるかによって異なります。 

### <a name="discovery-service"></a>探索サービス

ユーザーは複数のアプリ用 CDS 環境にアクセスできる可能性があります。 アプリケーションが特定の環境にのみ接続する場合を除いて、ユーザーはその資格情報を使用して接続する環境を選択でき、その資格情報で使用が許可されている環境を*検出*できるようにします。 

検出サービスを使用するには、検出サービスに対するユーザーを認証し、使用可能な環境を取得する必要があります。 通常、接続する環境を選択するための何らかの方法を実装する必要があります。 次のステップは、その環境に関する情報を使用して、特定の環境へのアクセスをもう一度認証します。

詳細: [検出サービス](discovery-service.md)

### <a name="authentication"></a>認証

ユーザーを接続する環境が分かっている場合、その環境で認証する必要があります。

詳細: [アプリ用 Common Data Service Web サービスでの認証](authentication.md)