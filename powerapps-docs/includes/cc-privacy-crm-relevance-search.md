---
ms.openlocfilehash: dff813dcdf6d025ba47e29699e2047f79cf85600
ms.sourcegitcommit: ad203331ee9737e82ef70206ac04eeb72a5f9c7f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/18/2019
ms.locfileid: "67225480"
---
関連性検索を有効にすると、[!INCLUDE[pn_dynamics_crm_online](pn-dynamics-crm-online.md)] インスタンス内の関与しているエンティティおよび属性のデータが [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] 検索インデックスと同期し始め、インデックスに格納されます。  
  
 関連性検索は既定では無効になっています。 システム管理者は [!INCLUDE[pn_dynamics_crm_online](pn-dynamics-crm-online.md)] インスタンス内のこの機能を有効にする必要があります。 関連性検索を有効にすると、システム管理者およびカスタマイザーは [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] 検索インデックスに同期されるデータを完全に制御できるようになります。  
  
 システム カスタマイザーは **[Customization Tools]\(カスタマイズ ツール\)** の **[関連性検索の構成]** ダイアログ ボックスを使用して検索用に特定のエンティティを有効にした後、有効になったエンティティ上でクイック検索ビューを構成して検索可能な属性を選択することができます。 データの変更は、[!INCLUDE[pn_dynamics_crm_online](pn-dynamics-crm-online.md)] および [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] 検索の間で、セキュリティで保護された接続を通じて継続的に同期されます。  構成データは暗号化され、必須シークレットは [!INCLUDE[pn_azure_key_vault](pn-azure-key-vault.md)] に格納されます。  
  
 関連性検索の機能と関係する Azure のコンポーネントやサービスについては、以下のセクションで詳しく説明します。  
  
 [!INCLUDE[cc_privacy_note_azure_trust_center](cc_privacy_note_azure_trust_center.md)]  
  
 [Azure Search サービス](https://azure.microsoft.com/services/search/)  
  
 [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] 検索インデックスは、短い応答時間で質の高い検索結果を提供するために使用されます。  [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] 検索によって、強力で洗練された次世代の検索機能が [!INCLUDE[pn_dynamics_crm_online](pn-dynamics-crm-online.md)] に追加されます。  これは [!INCLUDE[pn_Windows_Azure](pn-windows-azure.md)] によって提供される [!INCLUDE[pn_dynamics_crm_online](pn-dynamics-crm-online.md)] には含まれない、専用の検索サービスです。 新しい [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] 検索インデックスは、保存時にすべて暗号化されます。  2018 年 1 月 24 日より前にオプトインした場合は、関連性検索からオプトアウトして 1 時間待機してから再度オプトインすることで、データのインデックスを作成し直す必要があります。  
  
 [Azure SQL Database](https://azure.microsoft.com/services/sql-database/)  
  
 関連性検索では次のものを格納するために [!INCLUDE[pn_Azure_SQL_Database_long](pn-azure-sql-database-long.md)] が使用されます。  
  
-   組織およびその対応するインデックスに関連する構成データ  
  
-   検索サービスおよびインデックスに関連するメタデータ  
  
-   システムのメタデータおよび変更を同期する場合のデータへのポインター  
  
-   行レベルのセキュリティ強化を有効にするための認証データ  
  
[Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/)  
  
[!INCLUDE[pn_azure_event_hubs](pn-azure-event-hubs.md)] コンポーネントは、[!INCLUDE[pn_dynamics_crm_online](pn-dynamics-crm-online.md)] と [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] の間でメッセージを交換するため、また同期プロセスによって管理される作業項目を保持するために使用されます。 各メッセージには、データの同期のために使用する組織 ID やエンティティ名などの情報が格納されます。  
  
[Azure Service Fabric クラスター](https://azure.microsoft.com/services/service-fabric/)  
  
データの処理とインデックス作成は、Service Fabric ランタイムを通じて管理される仮想マシン上に展開されたマイクロサービス内で行われます。 検索 API とデータの同期プロセスも Service Fabric クラスター上でホストされます。  
  
Service Fabric は、Microsoft がミッションクリティカルなクラウドサービスを提供する長年の経験から生まれたものであり、5年以上にわたって実稼働証明が実証されています。 これは [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] のコア インフラストラクチャを稼働するための基盤となるテクノロジであり、[!INCLUDE[pn_skype_for_business](pn-skype-for-business.md)]、[!INCLUDE[pn_intune](pn-intune.md)]、[!INCLUDE[pn_azure_event_hubs](pn-azure-event-hubs.md)]、[!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] Data Factory、[!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] DocumentDB、[!INCLUDE[pn_Azure_SQL_Database_long](pn-azure-sql-database-long.md)]、[!INCLUDE[pn_cortana](pn-cortana.md)] などのサービスを支えています。また、毎秒 5 億件を超える評価を処理できるようスケーリングすることも可能です。  
  
[Azure Virtual Machine Scale Sets](https://azure.microsoft.com/services/virtual-machine-scale-sets/)  
  
[!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] Virtual Machine Scale Sets は柔軟性を備えており、ハイパー スケールアウト ワークロードをサポートするように設計されています。 [!INCLUDE[pn_azure_service_fabric](pn_azure_service_fabric.md)] クラスターは仮想マシン スケール セット上で実行されます。 データの処理とインデックス作成を実行するためのマイクロサービスは、スケール セット上でホストされ、Service Fabric ランタイムによって管理されます。  
  
[Azure Key Vault](https://azure.microsoft.com/services/key-vault/)  
  
[!INCLUDE[pn_azure_key_vault](pn-azure-key-vault.md)] は、検索プロセスで使用される証明書、キー、およびその他のシークレットを安全に管理するために使用されます。  
  
[Azure Storage (Blob Storage)](https://azure.microsoft.com/services/storage/blobs/?b=16.38)  
  
顧客データの変更は最大 2 日間 [!INCLUDE[pn_azure_blob_storage](pn_azure_blob_storage.md)] に格納されます。  各 BLOB は [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] Storage SDK の最新機能を活用して暗号化されます。この SDK は対称と非対称の暗号化をサポートしており、[!INCLUDE[pn_azure_key_vault](pn-azure-key-vault.md)] と統合されています。 [!INCLUDE[pn_crm_8_2_0_online_subsequent](pn-crm-8-2-0-online-subsequent.md)] を使用すると、電子メール メッセージおよび予定のメモおよび添付ファイルにあるドキュメントも BLOB ストレージに同期されます。  
  
[Azure Active Directory サービス](https://azure.microsoft.com/services/active-directory/)  
  
[!INCLUDE[pn_azure_active_directory](pn-azure-active-directory.md)] は、[!INCLUDE[pn_dynamics_crm_online](pn-dynamics-crm-online.md)] と [!INCLUDE[pn_Windows_Azure](pn-windows-azure.md)] サービス間の認証のために使用されます。  
  
[Azure Load Balancer](https://azure.microsoft.com/services/load-balancer/)  
  
[!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] Load Balancer は、一連のロード バランサーで定義されたクラウド サービスや仮想マシンの正常なサービス インスタンス間に、受信トラフィックを分散するために使用されます。 関連性検索では、デプロイのエンド ポイントを負荷分散するためにこれが使用されます。  
  
[Azure Virtual Network](https://azure.microsoft.com/documentation/articles/virtual-networks-overview/)  
  
1 つまたは複数のサブネットで稼働している Service Fabric クラスター上の仮想マシンは、[!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] Virtual Network によって接続されます。 セキュリティ ポリシー、DNS 設定、ルート テーブル、および IP アドレスは、この仮想ネットワーク内で完全に制御されます。 この仮想ネットワークでセキュリティ規則を適用するために、ネットワーク セキュリティ グループが活用されます。 各規則では、仮想ネットワーク内の VM に対するネットワーク トラフィックが許可または拒否されます。