---
title: 開発者リソースの表示またはダウンロード | MicrosoftDocs
description: 開発者リソースおよびサービス エンドポイント URL を検索する
keywords: ''
ms.date: 06/06/2018
ms.service: powerapps
ms.custom: null
ms.topic: article
applies_to:
  - Dynamics 365 (online)
  - Dynamics 365 Version 9.x
  - powerapps
ms.assetid: e200d242-ff3f-48e5-af32-aed050e02441
author: Mattp123
ms.author: matp
manager: kvivek
ms.reviewer: null
ms.suite: null
ms.tgt_pltfrm: null
search.audienceType:
  - maker
search.app:
  - PowerApps
  - D365CE
---
<!-- TODO: The Developer Resources page have to be updated to match this page -->

# <a name="view-or-download-developer-resources"></a>開発者リソースの表示またはダウンロード

このページには、開発者のリソースと、作業中の特定のインスタンスに関する情報があります。 

## <a name="view-the-developer-resources-page-for-your-environment"></a>環境の開発者リソース ページを表示する

1. PowerApps ポータルから、![設定ボタン](../../administrator/media/settings-button-nav-bar.png) [設定] ボタンを選択し、**高度なカスタマイズ** を選択します。

    ![高度なカスタマイズ](media/advanced-customizations-menu.png)

1. **高度なカスタマイズ** パネル内で、**開発者リソース** リンクを選択します。<br />![開発者リソース リンク](media/developer-resources-link.png)

## <a name="getting-started"></a>はじめに 

このセクションには、開発者がリソースを見つけることができるリンクを提供します。 次のリソースを使用できます。


|リンク |説明|
|---------|---------|
|[ディベロッパー センター](https://go.microsoft.com/fwlink/?LinkId=551006)|開発者用ドキュメントのメイン エントリ ポイント。|
|[開発者フォーラム](https://go.microsoft.com/fwlink/?LinkId=550993)|他の開発者にして質問して答えをもらいます。|
|[NuGet パッケージ](https://go.microsoft.com/fwlink/?LinkId=550994)|SDK アセンブリをプロジェクトに追加するには NuGet パッケージを検出します。|
|[ツールのダウンロード](https://go.microsoft.com/fwlink/?LinkID=512122)|必要なツールは NuGet からダウンロードできます。 最新バージョンを取得する際にこのページの PowerShell スクリプトを使用します。|
|[サンプル コード](https://go.microsoft.com/fwlink/?LinkId=553007)|使用できるサンプルの一覧。|
|[開発者向けの概要](https://go.microsoft.com/fwlink/?LinkId=550995)|開発者の概要について説明するトピックにリンクします。|

<!-- TODO update 512122 to go to https://docs.microsoft.com/dynamics365/customer-engagement/developer/download-tools-nuget -->


## <a name="connect-your-apps-to-this-instance-of-common-data-service"></a>Common Data Service のこのインスタンスにアプリを接続する

このセクションには、Common Data Service インスタンスに接続するために必要な情報を提供します。

### <a name="instance-web-api"></a>インスタンスの Web API

これは、インスタンスの Web API の URL です。 Web API は OData v4 RESTful API です。 また、インスタンスで使用できるメタデータおよび操作を説明するサービス ドキュメントもダウンロードできます。 詳細: [開発者ドキュメント: Dynamics 365 Customer Engagement Web API の使用](/dynamics365/customer-engagement/developer/use-microsoft-dynamics-365-web-api)

### <a name="organization-service"></a>組織のサービス

これは、インスタンスの組織サービスの SOAP エンドポイントの URL です。
ここでは、このサービスについての WSDL をダウンロードできますが、通常、CrmSvcUtil.exe コード生成ツールを使用して .NET プロジェクトのエンティティ クラスを構築します。 詳細: 
- [開発者ドキュメント: コード生成ツール (CrmSvcUtil.exe) を使用して事前バインド型エンティティ クラスを作成する](/dynamics365/customer-engagement/developer/org-service/create-early-bound-entity-classes-code-generation-tool)
- [開発者ドキュメント: 組織サービスを使用したデータまたはメタデータの読み取りと書き込み](/dynamics365/customer-engagement/developer/org-service/use-organization-service-read-write-data-metadata)

### <a name="instance-reference-information"></a>インスタンス参照情報

この情報はインスタンスについて独自に説明しています。 GUID **ID** と**一意の名前**があります。
この情報は、インスタンスと共に Azure 拡張を使用するときに必要です。
詳細: [開発者ドキュメント: Dynamics 365 Customer Engagement の Azure 拡張機能](/dynamics365/customer-engagement/developer/azure-extensions)

## <a name="connect-your-apps-to-the-common-data-service-discovery-service"></a>Common Data Service の探索サービスにアプリを接続する

ユーザーはアプリ環境の複数の Common Data Service にアクセスできる場合があるので、探索サービスでは、ユーザーがユーザーの資格情報に基づいてアクセスできる使用可能な環境を取得できます。

### <a name="discovery-web-api"></a>検出 Web API

これは、インスタンスで使用するための探索サービスの RESTful OData v4 バージョンのエンドポイント アドレスです。 サービス ドキュメントはここでダウンロードできます。
詳細情報: [開発者ドキュメント: Web API を使用して組織の URL を検出する](/dynamics365/customer-engagement/developer/webapi/discover-url-organization-web-api)


### <a name="discovery-service"></a>探索サービス

これは、インスタンスで使用するための探索サービスの SOAP バージョンのエンドポイント アドレスです。 サービス ドキュメントはここでダウンロードできます。
詳細情報: [開発者ドキュメント: 探索サービスを使用して組織の URL を検出する](/dynamics365/customer-engagement/developer/org-service/discover-url-organization-organization-service)
  
### <a name="more-information"></a>詳細

[開発者ドキュメント: 開発者リソース ページ](/dynamics365/customer-engagement/developer/developer-resources-page)<br />
[開発者ドキュメント: Dynamics 365 Customer Engagement Web API の使用](/dynamics365/customer-engagement/developer/use-microsoft-dynamics-365-web-api)<br />
[開発者ドキュメント: 組織サービスを使用したデータまたはメタデータの読み取りと書き込み](/dynamics365/customer-engagement/developer/org-service/use-organization-service-read-write-data-metadata)<br />
[開発者ドキュメント: Dynamics 365 Customer Engagement の Azure 拡張機能](/dynamics365/customer-engagement/developer/azure-extensions)<br />
[開発者ドキュメント: Web API を使用して組織の URL を検出する](/dynamics365/customer-engagement/developer/webapi/discover-url-organization-web-api)<br />
[開発者ドキュメント: 探索サービスを使用して組織の URL を検出する](/dynamics365/customer-engagement/developer/org-service/discover-url-organization-organization-service)
  

