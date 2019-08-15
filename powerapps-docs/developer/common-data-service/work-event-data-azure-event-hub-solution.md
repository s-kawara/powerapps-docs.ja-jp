---
title: Azure イベント ハブソリューション の Dynamics 365 イベント データで作業 (Common Data Service)| Microsoft Docs
description: このトピックでは、Azure イベント ハブ ソリューションでイベント データを使用する方法を説明します。
keywords: ''
ms.date: 05/08/2019
ms.service: powerapps
ms.custom:
  - ''
ms.topic: article
ms.assetid: a3732c49-7f47-d87c-5062-585ef28ab511
author: brandonsimons
ms.author: jdaly
manager: ryjones
ms.reviewer: pehecke
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---

# <a name="work-with-common-data-service-event-data-in-your-azure-event-hub-solution"></a>Azure イベント ハブ ソリューションの Common Data Service イベント データで作業

Azure Event Hub は非常に拡張性の高いパブリッシュ/サブスクライブ サービスであり、毎秒数百万のイベントを取得して、複数のアプリケーションに流すことができます。 Common Data Service Azure インターフェイスにより、 イベント データを Azure Service Bus で公開可能になり、イベント ハブ ソリューションのサブスクライバーで利用できます。 次の情報は、イベント ハブ ソリューションに Azure イベント データを送信するために実行する必要がある一般的なタスクについて説明します。  
  
> [!NOTE]
> Azure サブスクリプションとイベント ハブ ライセンスがイベント ハブへのアクセスに必要です。
  
## <a name="1-create-an-event-hub"></a>1. イベント ハブの作成  
 Azure では、API プログラミングによって、または [Azure クラシック ポータル](https://manage.windowsazure.com) を使用して対話的に、イベント ハブを作成できます 。 どちらの場合も、イベント ハブの作成後に、イベント ハブの接続文字列のコピーを取得して、次のセクションで詳細に説明する Azure サービス エンドポイントを登録するときにその文字列を指定する必要があります。  
  
 イベント ハブの作成方法の詳細については、[Event Hub のドキュメント](https://azure.microsoft.com/documentation/services/event-hubs/) を参照してください。  
  
## <a name="2-register-an-endpoint"></a>2. エンドポイントの登録  
 イベント ハブのサービス エンドポイントの登録は、キューやトピックなどの他のサポートされている契約の種類の登録と似ています。 SDK のダウンロードで提供されるプラグイン登録ツールを使用して、サービス エンドポイントを登録します。  登録フォームに入力するとき、**イベント ハブ**の契約の種類を指定します。 メッセージの本文の形式については、**XML** または **JSON** を選択します。 また、SAS 認証のみが使用可能であり、イベント ハブの作成時に取得した接続文字列を指定する必要があります。 詳細: [ チュートリアル: Common Data Service との統合用の Microsoft Azure (SAS) の構成](walkthrough-configure-azure-sas-integration.md)。  
  
## <a name="3-register-code"></a>3. コードの登録  
 Dynamics 365 は、Azure 対応プラグインの実行を操作時に引き起こす正確な操作 (エンティティ/メッセージの組み合わせ) を知る必要があります。 イベント ハブを作成するので、この操作は Azure のイベント データの処理に特に関連しています。 Azure 対応プラグインのステップを Azure イベント実行パイプラインに登録する必要があります。  詳細については、「[チュートリアル: プラグイン登録ツールを使用した Azure 対応プラグインの登録」 を参照してください。](walkthrough-register-azure-aware-plug-in-using-plug-in-registration-tool.md)  
  
 プラグインの代わり、Azure 対応のユーザー定義ワークフロー活動を使用する場合は、プラグイン登録ツールを使用して活動のアセンブリを登録し、その活動をワークフローに組み込みます。 詳細については、[サンプル: Azure 対応のユーザー定義ワークフロー活動](/dynamics365/customer-engagement/developer/sample-azure-aware-custom-workflow-activity) を参照してください。
  
## <a name="4-start-listening"></a>4. リッスンを開始  
 サービス エンドポイントで、Azure サービス ハブ ソリューション アプリケーションのリスニングを開始します。  
  
## <a name="5-trigger"></a>5. トリガー  
 ユーザー定義のワークフロー活動が含まれているプラグインまたはワークフローの実行を起動する Azure の操作を実行します。 これは、このトピックの前のセクションのプラグイン ステップを登録した操作 (エンティティとメッセージの組み合わせ) と同じです。 Web アプリケーションを使用して、または Azure の Web サービスにアクセスするアプリケーション コードを使用して、目的の操作を実行できます。  
  
## <a name="6-verification"></a>6. 検証  
 Azure Web アプリケーションで関連するシステム ジョブをチェックして、**成功しました**のステータスを確認できます。 **失敗しました**のステータスを確認した場合は、ステータス情報を使用して失敗の原因を特定します。 次に、失敗の種類に基づいて、両方のシステムの構成を再確認するか、またはアプリケーション コードをデバッグして、問題を特定して解決することができます。  
  
### <a name="see-also"></a>関連項目  
 [Common Data Service との Azure 統合](azure-integration.md)
