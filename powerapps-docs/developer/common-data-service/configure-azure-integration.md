---
title: Azure 統合の構成 (Common Data Service) | Microsoft Docs
description: このトピックは Common Data Service との Azure 統合の構成について説明します。
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
# <a name="configure-azure-integration-with-common-data-service"></a>Common Data Service との Azure 統合の構成

現在のコア操作のメッセージ要求データを、Azure Service Bus 上でリスニングする、クラウドでホストされたアプリケーションに投稿することができます。 Common Data Service でこの機能を有効にするには、このトピックで説明するタスクを実行する必要があります。

## <a name="configure-azure-for-common-data-service-integration"></a>Common Data Service 統合のために Azure を構成する

承認のためには SAS を使用しているため、Azure ソリューションの規則および発行者を構成して、リスナー アプリケーションが Azure Service Bus に投稿された Common Data Service メッセージを読み取り可能にする必要があります。 さらに、Common Data Service 発行者要求を受け入れるためのサービス バス規則を構成する必要があります。 Azure を構成する推奨方法は、プラグイン登録ツール (PRT) を使用することです。

認証を構成する詳細な手順については、[チュートリアル: Common Data Service との統合のために Azure (SAS) を構成](walkthrough-configure-azure-sas-integration.md) を参照してください。

## <a name="test-configuration"></a>構成のテスト

Azure の統合を構成した後で、以下の追加タスクを実行する必要があります。

1. リスナー アプリケーションを作成し、Azure Service Bus ソリューションのエンドポイントに登録します。 詳細については、Azure Service Bus [ドキュメント](/azure/service-bus-messaging/service-bus-messaging-overview) を参照してください。
1. Azure 対応のプラグインまたは Azure 対応のユーザー定義のワークフロー活動を Common Data Service に登録します。 詳細: [チュートリアル: プラグイン登録ツールを使用した Azure 対応プラグインの登録](walkthrough-register-azure-aware-plug-in-using-plug-in-registration-tool.md)
1. プラグインまたはユーザー定義ワークフロー活動の実行をトリガーするために必要な Common Data Service の操作を実行します。

先行の手順がすべて正しく実行されると、Common Data Service のデータ コンテキストを含んだメッセージは Azure キューまたはトピックへ送信され、最終的にリスナー アプリケーションが受け取るようになります。 Azure Service Bus への投稿が成功したかどうかを調べるには、Common Data Service Web アプリケーションのシステム ジョブ グリッドに移動して、関連するシステム ジョブの状態を確認します。 エラーが発生した場合は、システム ジョブのメッセージ セクションにエラーの詳細が表示されます。

### <a name="see-also"></a>関連項目

[Azure 統合](azure-integration.md)<br />
[ビジネス プロセスを拡張するためのプラグインの使用](plug-ins.md)<br />
[Azure ソリューションの Common Data Service データに関する作業](work-data-azure-solution.md)<br />
[Azure ソリューション用のリスナー アプリケーションの記述](write-listener-application-azure-solution.md)<br />
[Azure Service Bus とは何か](/azure/service-bus-messaging/service-bus-messaging-overview)