---
ms.openlocfilehash: ce9db35844f46e9779055ec30dcba0f9459c3a16
ms.sourcegitcommit: 4042388fa5e7ef50bc59f9e35df330613fea29ae
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61575528"
---
[!INCLUDE[pn_connected_field_service_msdyn365](pn-connected-field-service-msdyn365.md)] をインストールすることで、[!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] のサブスクリプション情報を指定すると、必要な [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] リソース (後述) がデプロイされ、[!INCLUDE[pn_dynamics_crm_online](pn-dynamics-crm-online.md)] インスタンスから [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] にデータ (コマンドや登録など) に送信されるようになります。その結果、デバイスを登録してから、登録されたデバイスとの間でコマンドを送受信する IoT 対応のシナリオが可能になります。 管理者は、Connected Field Service をアンインストールしてこの機能を削除してから、[!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] portal に移動して不要になった関連する [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] サービスを管理することができます。  
  
 Connected Field Service 機能と関係する [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] のコンポーネントやサービスについては、以下のセクションで詳しく説明します。  
  
 [!INCLUDE[cc_privacy_note_azure_trust_center](cc-privacy-note-azure-trust-center.md)]  
  
 [Service Bus キュー](https://azure.microsoft.com/documentation/articles/service-bus-dotnet-get-started-with-queues/)  
  
 [!INCLUDE[pn_dynamics_crm](pn-dynamics-crm.md)] と [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] 間に流れる受信メッセージと送信メッセージ (コマンド) の両方にキューが用意されています。 IoT アラートが [!INCLUDE[pn_dynamics_crm](pn-dynamics-crm.md)] に送信されるか、コマンドが [!INCLUDE[pn_dynamics_crm](pn-dynamics-crm.md)] から IoT ハブに送信されると、このキューに格納されます。  
  
 [Logic Apps](https://azure.microsoft.com/services/logic-apps/)  
  
 [!INCLUDE[pn_dynamics_crm](pn-dynamics-crm.md)] コネクタとキュー コネクタを使用するオーケストレーション サービスが提供されます。 [!INCLUDE[pn_dynamics_crm](pn-dynamics-crm.md)] コネクタは [!INCLUDE[pn_dynamics_crm](pn-dynamics-crm.md)] に固有のエンティティを構築するために使用され、キュー コネクタはキューのポーリングに使用されます。  
  
 [Stream Analytics](https://azure.microsoft.com/services/stream-analytics/)  
  
 データから詳細な分析情報を取得できるフル マネージドでリアルタイムのイベント処理エンジンが用意されています。 Stream Analytics を使用すると、デバイス、センサー、Web サイト、ソーシャル メディア、アプリケーション、インフラストラクチャ システムなどからのデータ ストリーミングに関するリアルタイムの分析コンピューティングを簡単に設定できます。 これは [!INCLUDE[pn_dynamics_crm](pn-dynamics-crm.md)] に対して選択的な IoT アラートを送信するじょうごとして機能しています。  
  
 [IoT Hub](https://azure.microsoft.com/services/iot-hub/)  
  
 Connected Field Services は、IoT Hub を使用して登録済みのデバイスと資産の状態を管理します。 さらに、IoT Hub は、接続されたデバイスにコマンドと通知を送信し、確認応答の受信を使用してメッセージの配信を追跡します。 デバイスのメッセージは、断続的に接続されるデバイスに対応できるように、持続的な方法で送信されます。  
  
 **Simulator**  
  
 IoT ハブからコマンドを送信するか、コマンドを受信して​​いるデバイスをエミュレートするテスト Web アプリケーションです。  
  
 [Azure SQL Database](https://azure.microsoft.com/services/sql-database/)  
  
 Connected Field Service は、SQL [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] を使用してデバイスのハートビート メッセージを格納します。このメッセージは、後で PowerBI によって[!INCLUDE[pn_dynamics_crm](pn-dynamics-crm.md)] にデバイスの状態を表示するために使用されます。  
  
 [Azure Blob Storage](https://azure.microsoft.com/services/storage/)  
  
 Stream Analytics に使用されるクエリは [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] BLOB ストレージに保存されます。