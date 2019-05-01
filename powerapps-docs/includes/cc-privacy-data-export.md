---
ms.openlocfilehash: e9b0446c2fb09cad33f5a3ae4bb69103f7d07d70
ms.sourcegitcommit: 4042388fa5e7ef50bc59f9e35df330613fea29ae
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61579121"
---
Data Export Service を使用する場合、[!INCLUDE[pn_microsoftcrm](pn-microsoftcrm.md)] 内からデータ エクスポート プロファイルをアクティブ化すると、そのプロファイルに追加されたエンティティのデータが [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] に送信されます。 初回の同期には、エクスポート プロファイルに追加されたエンティティに関連付けられているすべてのデータが含まれますが、以降、同期には新しい変更のみが含まれ、継続的に Data Export Service に送信されます。 Data Export Service に送信されたデータは、[!INCLUDE[pn_azure_service_bus](pn_azure_service_bus.md)] および [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] Storage に一時的に保存され、[!INCLUDE[pn_azure_service_fabric](pn_azure_service_fabric.md)] で処理され、最後に [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] サブスクリプションで指定された宛先データベースに同期 (挿入、更新、または削除) されます。 データが同期された後、[!INCLUDE[pn_azure_service_bus](pn_azure_service_bus.md)] および [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] Storage からデータが削除されます。 データ同期中に障害が発生した場合、エンティティの種類、レコード ID、および同期のタイムスタンプに対応する最小限のデータが [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] Storage に保存され、更新されなかったレコードの一覧をダウンロードできます。  
  
 管理者はいつでもデータ エクスポート プロファイルを無効にし、データの同期を停止できます。 また、管理者は、エクスポート プロファイルを削除して失敗したレコード ログを削除することができます。また、Data Export Service の使用を停止するには Data Export Service ソリューションをアンインストールすることができます。  
  
 データ同期は [!INCLUDE[pn_crm_shortest](pn-crm-shortest.md)] と Data Export Service の間で安全に継続的に行われます。 データは、[!INCLUDE[pn_crm_shortest](pn-crm-shortest.md)] と Data Export Service の間で継続的に交換されるときに暗号化されます。  
  
 Data Export Service と関係する Azure のコンポーネントやサービスについては、以下のセクションで詳しく説明します。  
  
 [!INCLUDE[cc_privacy_note_azure_trust_center](cc_privacy_note_azure_trust_center.md)]  
  
 [Azure Service Fabric](https://azure.microsoft.com/services/service-fabric/)  
  
 [!INCLUDE[pn_crm_shortest](pn-crm-shortest.md)] から受信したレコードの同期通知を処理し、宛先データベースのレコード データの挿入、更新、または削除を処理する、API とコンピューティング [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] VM が用意されています。 [!INCLUDE[pn_azure_service_fabric](pn_azure_service_fabric.md)] ランタイムによって管理される仮想マシンに展開されるマイクロサービスは、データ同期に関連するすべてのコンピューティング サービスを処理します。  
  
 [Azure Service Bus](https://azure.microsoft.com/services/service-bus/)  
  
 [!INCLUDE[pn_crm_shortest](pn-crm-shortest.md)] が [!INCLUDE[pn_azure_service_fabric](pn_azure_service_fabric.md)] のコンピューティング ノードによって処理された同期通知メッセージを挿入するメッセージ バスが用意されています。 各メッセージには、データを同期するための組織 ID やレコードなどの情報が格納されます。 Azure Service Bus のデータは、保存時には暗号化されません。Data Export Service からのみアクセスすることができます。  
  
 [Azure Blob Storage](https://azure.microsoft.com/services/storage/)  
  
 レコード同期通知のデータが大きすぎてメッセージに格納できない場合、または同期通知を処理するために一時的な障害が発生した場合、データは [!INCLUDE[pn_azure_blob_storage](pn_azure_blob_storage.md)] に一時的に格納されます。 各 BLOB は [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] Storage SDK の最新機能を活用して暗号化されます。この SDK は対称と非対称の暗号化をサポートしており、[!INCLUDE[pn_azure_key_vault](pn-azure-key-vault.md)] と統合されています。  
  
 [Azure SQL](https://azure.microsoft.com/services/sql-database/)  
  
 [!INCLUDE[pn_Azure_SQL_Database_long](pn-azure-sql-database-long.md)] には、データ エクスポート プロファイルの構成とデータ同期メトリックが格納されます。