---
title: Azure 統合の構成 (アプリ用 Common Data Service) | Microsoft Docs
description: このトピックは、アプリ用 Common Data Service との Azure 統合の構成について説明します。
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
# <a name="configure-azure-integration-with-common-data-service-for-apps"></a>アプリ用 Common Data Service との Azure 統合の構成

現在のコア操作のメッセージ要求データを、Azure Service Bus 上でリスニングする、クラウドでホストされたアプリケーションに投稿することができます。 アプリ用 CDS でこの機能を有効にするには、このトピックで説明するタスクを実行する必要があります。

## <a name="configure-azure-for-cds-for-apps-integration"></a>アプリ用 CDS 統合に対する Azure の構成

承認のためには SAS を使用しているため、Azure ソリューションの規則および発行者を構成して、リスナー アプリケーションが Azure Service Bus に投稿されたアプリ用 CDS メッセージを読み取りることができるようにする必要があります。 さらに、アプリ用 CDS 発行者要求を受け入れるためのサービス バス規則を構成する必要があります。 Azure を構成する推奨方法は、プラグイン登録ツール (PRT) を使用することです。

認証の構成の詳細については、[チュートリアル: アプリ用 Common Data Service との統合のために Azure (SAS) を構成](walkthrough-configure-azure-sas-integration.md) を参照してください。

## <a name="test-configuration"></a>構成のテスト

Azure の統合を構成した後で、以下の追加タスクを実行する必要があります。

1. リスナー アプリケーションを作成し、Azure Service Bus ソリューションのエンドポイントに登録します。 詳細については、Azure Service Bus [ドキュメント](/azure/service-bus-messaging/service-bus-messaging-overview) を参照してください。
1. Azure 対応のプラグインまたは Azure 対応のユーザー定義のワークフロー活動をアプリ用 CDS に登録します。 詳細: [チュートリアル: プラグイン登録ツールを使用した Azure 対応プラグインの登録](walkthrough-register-azure-aware-plug-in-using-plug-in-registration-tool.md)
1. プラグインまたはユーザー定義ワークフロー活動の実行をトリガーするために必要なアプリ用 CDS の操作を実行します。

先行の手順がすべて正しく実行されると、アプリ用 CDS のデータ コンテキストを含んだメッセージは、Azure キューまたはトピックへ送信され、最終的にリスナー アプリケーションが受け取るようになります。 Azure Service Bus への投稿が成功したかどうかを調べるには、アプリ用 CDS Web アプリケーションのシステム ジョブ グリッドに移動して、関連するシステム ジョブの状態を確認します。 エラーが発生した場合は、システム ジョブのメッセージ セクションにエラーの詳細が表示されます。

### <a name="see-also"></a>関連項目

[Azure 統合](azure-integration.md)<br />
[ビジネス プロセスを拡張するためのプラグインの使用](plug-ins.md)<br />
[Azure ソリューションのアプリ用 Common Data Service データとの連携](work-data-azure-solution.md)<br />
[Azure ソリューション用のリスナー アプリケーションの記述](write-listener-application-azure-solution.md)<br />
[Azure Service Bus とは何か](/azure/service-bus-messaging/service-bus-messaging-overview)