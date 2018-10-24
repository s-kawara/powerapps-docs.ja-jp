---
title: 開発者向けリソースを表示またはダウンロードする | MicrosoftDocs
description: 開発者向けリソースとサービスのエンドポイントの URL を探します
keywords: ''
ms.date: 06/06/2018
ms.service: crm-online
ms.custom: ''
ms.topic: article
applies_to:
- Dynamics 365 (online)
- Dynamics 365 Version 9.x
- powerapps
ms.assetid: e200d242-ff3f-48e5-af32-aed050e02441
author: Mattp123
ms.author: matp
manager: kvivek
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.openlocfilehash: ae93b57d9ead3a62fb538ae986eb524367259545
ms.sourcegitcommit: aba996b1773ecdf62758e06b34eaf57bede29e08
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/08/2018
ms.locfileid: "39696143"
---
<!-- TODO: The Developer Resources page have to be updated to match this page -->

# <a name="view-or-download-developer-resources"></a>開発者向けリソースを表示またはダウンロードする

このページには、開発者用のリソースと、作業している特定のインスタンスについての情報が記載されています。 

## <a name="view-the-developer-resources-page-for-your-environment"></a>環境の開発者向けリソース ページを表示する

1. PowerApps ポータルで ![設定ボタン](../../administrator/media/settings-button-nav-bar.png) [設定] ボタンを選択し、**[高度なカスタマイズ]** を選択します。

    ![高度なカスタマイズ](media/advanced-customizations-menu.png)

1. **[高度なカスタマイズ]** パネル内で **[開発者向けリソース]** のリンクを選択します。<br />![開発者向けリソースのリンク](media/developer-resources-link.png)

## <a name="getting-started"></a>作業の開始 

このセクションでは、開発者がリソースを探すためのリンクを示します。 次のリソースを使用できます。


|リンク |説明|
|---------|---------|
|[デベロッパー センター](https://go.microsoft.com/fwlink/?LinkId=551006)|開発者向けドキュメントへの主要な入り口です。|
|[開発者フォーラム](https://go.microsoft.com/fwlink/?LinkId=550993)|他の開発者と質問や回答をやり取りします。|
|[NuGet パッケージ](https://go.microsoft.com/fwlink/?LinkId=550994)|プロジェクトに SDK アセンブリを追加する NuGet パッケージを探します。|
|[ダウンロード ツール](https://go.microsoft.com/fwlink/?LinkID=512122)|必要になるツールは、NuGet からダウンロードできます。 このページ上で PowerShell スクリプトを使用して、最新バージョンを取得します。|
|[サンプル コード](https://go.microsoft.com/fwlink/?LinkId=553007)|使用可能なサンプルの一覧です。|
|[開発者向け概要](https://go.microsoft.com/fwlink/?LinkId=550995)|開発者向けの概要を提供するトピックへのリンクです。|

<!-- TODO update 512122 to go to https://docs.microsoft.com/dynamics365/customer-engagement/developer/download-tools-nuget -->


## <a name="connect-your-apps-to-this-instance-of-common-data-service-for-apps"></a>この Common Data Service for Apps のインスタンスにアプリを接続する

このセクションには、Common Data Service for Apps のインスタンスに接続するために必要な情報が記載されています。

### <a name="instance-web-api"></a>インスタンスの Web API

これは、インスタンスの Web API の URL です。 Web API は OData v4 RESTful API です。 インスタンスで使用できるメタデータと操作について説明したサービス ドキュメントをダウンロードすることもできます。 詳細情報: [開発者ドキュメント: Dynamics 365 Customer Engagement Web API を使用する](/dynamics365/customer-engagement/developer/use-microsoft-dynamics-365-web-api)

### <a name="organization-service"></a>組織のサービス

これは、インスタンスに対する組織のサービスの SOAP エンドポイントの URL です。
このサービス向けの WSDL をここでダウンロードできますが、通常はコード生成ツール CrmSvcUtil.exe を使用して .NET プロジェクト用のエンティティ クラスを構築します。 詳細情報: 
- [開発者ドキュメント: コード生成ツール (CrmSvcUtil.exe) を使用して事前バインド型エンティティ クラスを作成する](/dynamics365/customer-engagement/developer/org-service/create-early-bound-entity-classes-code-generation-tool)
- [開発者ドキュメント: 組織サービスを使用したデータまたはメタデータの読み取りと書き込み](/dynamics365/customer-engagement/developer/org-service/use-organization-service-read-write-data-metadata)

### <a name="instance-reference-information"></a>インスタンスの参照情報

この情報によってインスタンスが一意に表現されます。 GUID の **[ID]** と **[一意の名前]** があります。
この情報は、インスタンスで Azure 拡張機能を使用する場合に必要となります。
詳細情報: [開発者ドキュメント: Dynamics 365 Customer Engagement の Azure 拡張機能](/dynamics365/customer-engagement/developer/azure-extensions)

## <a name="connect-your-apps-to-the-common-data-service-for-apps-discovery-service"></a>Common Data Service for Apps の探索サービスにアプリを接続する

ユーザーが複数の CDS for Apps 環境に対するアクセスを持っている可能性があるため、探索サービスでは、各ユーザー資格情報に基づいて、ユーザーがアクセスできる使用可能な環境を取得することができます。

### <a name="discovery-web-api"></a>Web API の検出

これは、インスタンスに対して使用する、RESTful OData v4 バージョンの探索サービスのエンドポイント アドレスです。 ここでサービス ドキュメントをダウンロードすることもできます。
詳細情報: [開発者ドキュメント: Web API を使用して組織の URL を検出します](/dynamics365/customer-engagement/developer/webapi/discover-url-organization-web-api)


### <a name="discovery-service"></a>探索サービス

これは、インスタンスに対して使用する、SOAP バージョンの探索サービスのエンドポイント アドレスです。 ここでサービス ドキュメントをダウンロードすることもできます。
詳細情報: [開発者ドキュメント: 探索サービスを使用して組織の URL を検出する](/dynamics365/customer-engagement/developer/org-service/discover-url-organization-organization-service)
  
### <a name="more-information"></a>詳細

[開発者ドキュメント: 開発者リソース ページ](/dynamics365/customer-engagement/developer/developer-resources-page)<br />
[開発者ドキュメント: Dynamics 365 Customer Engagement Web API を使用する](/dynamics365/customer-engagement/developer/use-microsoft-dynamics-365-web-api)<br />
[開発者ドキュメント: 組織サービスを使用したデータまたはメタデータの読み取りと書き込み](/dynamics365/customer-engagement/developer/org-service/use-organization-service-read-write-data-metadata)<br />
[開発者ドキュメント: Dynamics 365 Customer Engagement の Azure 拡張機能](/dynamics365/customer-engagement/developer/azure-extensions)<br />
[開発者ドキュメント: Web API を使用して組織の URL を検出します](/dynamics365/customer-engagement/developer/webapi/discover-url-organization-web-api)<br />
[開発者ドキュメント: 探索サービスを使用して組織の URL を検出する](/dynamics365/customer-engagement/developer/org-service/discover-url-organization-organization-service)
  

