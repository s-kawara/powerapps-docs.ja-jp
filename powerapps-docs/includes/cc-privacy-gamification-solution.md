---
ms.openlocfilehash: 747ea34b784b852261debe91f587d64ee3277804
ms.sourcegitcommit: 4042388fa5e7ef50bc59f9e35df330613fea29ae
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61574945"
---
[!INCLUDE[pn_gamification](pn-gamification.md)] ソリューションをインストールして有効にすることで、それを有効にしたユーザーのアカウントを識別するもの (名、姓、メール アドレスなど) が [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] に保存され、[!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] でホストされている [!INCLUDE[pn_gamification_shortest](pn-gamification-shortest.md)] サービスで認証できるようになります。 これは、管理者によって [!INCLUDE[pn_gamification_shortest](pn-gamification-shortest.md)] サービスで有効にされているすべてのユーザーに適用されます。 [!INCLUDE[pn_gamification_shortest](pn-gamification-shortest.md)] ソリューションにより、管理者によって構成された KPI (主要業績評価指標) データが [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] サービスに送信されます。そのデータは [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] 構造化ストレージと BLOB ストレージに保存されます。  各ユーザーのアバター、カスタム特典、会社ロゴは [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] に保存されますが、情報は [!INCLUDE[pn_crm_shortest](pn-crm-shortest.md)] に返されません。  
  
管理者と承認されたユーザーは、通話、営業案件、帳簿に記載された収益など、[!INCLUDE[pn_crm_shortest](pn-crm-shortest.md)] データを活用し、ゲームで使用する KPI を構成できます。 [!INCLUDE[pn_gamification_shortest](pn-gamification-shortest.md)] サービスが [!INCLUDE[pn_crm_shortest](pn-crm-shortest.md)] の呼び出しを開始することはなく、KPI が使用されているゲームなど、[!INCLUDE[pn_crm_shortest](pn-crm-shortest.md)] に戻ってくるデータに応答するだけです。  
  
管理者は [!INCLUDE[pn_gamification_shortest](pn-gamification-shortest.md)] TV ストリームを公開することもできます。 ゲーム マネージャーが [!INCLUDE[pn_gamification_shortest](pn-gamification-shortest.md)] TV ストリームを設定し、公開ストリーミングを有効にすると、TV ストリームは、ストリーム リンクが与えられたインターネット上のあらゆるユーザーに視聴されます。  
  
管理者は後で、[!INCLUDE[pn_microsoftcrm](pn-microsoftcrm.md)] 組織からこのソリューションをアンインストールすることで [!INCLUDE[pn_gamification_shortest](pn-gamification-shortest.md)] 機能を削除できます。  
  
[!INCLUDE[pn_gamification_shortest](pn-gamification-shortest.md)] に関係する [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] のコンポーネントやサービスについては、以下のセクションで説明しています。  
  
[!INCLUDE[cc_privacy_note_azure_trust_center](cc-privacy-note-azure-trust-center.md)]  
  
[Cloud Services](https://azure.microsoft.com/services/cloud-services/)  
  
 **デザイナー サービス (Web ロール)**  
  
これは、[!INCLUDE[pn_crm_shortest](pn-crm-shortest.md)] 組織とマルチテナント型 [!INCLUDE[pn_gamification_shortest](pn-gamification-shortest.md)] [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] コンポーネント間の通信のために複数の Web サービスを提供します。 たとえば、ゲーミフィケーションの詳細は [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] SQL Storage に保存されます。  ゲーム計算では、サービスでスコアを付け、表示する目的で返される [!INCLUDE[pn_azure_service_bus](pn-azure-service-bus.md)] キューが使用されます。  顧客やユーザーがアップロードしたイメージは [!INCLUDE[pn_azure_blob_storage](pn-azure-blob-storage.md)] に保存されます。 すべての要求は [!INCLUDE[pn_azure_active_directory](pn-azure-active-directory.md)] に対して認証されます。  
  
[Azure Key Vault](https://azure.microsoft.com/services/key-vault/)  
  
すべてのサービスは構成データを [!INCLUDE[pn_azure_key_vault](pn-azure-key-vault.md)] に格納します。  
  
[Azure SQL Database](https://azure.microsoft.com/services/sql-database/)  
  
[!INCLUDE[pn_gamification_shortest](pn-gamification-shortest.md)] では SQL [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] を利用して次を格納します。  
  
- KPI データ  
  
- ゲーム計算  
  
- 組織 (テナント) データ  
  
[Azure Blob Storage](https://azure.microsoft.com/services/storage/)  
  
アバター、会社ロゴ、顧客がアップロードしたその他のイメージは [!INCLUDE[pn_azure_blob_storage](pn-azure-blob-storage.md)] に保存されます。  
  
[Azure Content Delivery Network (CDN)](https://azure.microsoft.com/services/cdn/)  
  
[!INCLUDE[pn_gamification_shortest](pn-gamification-shortest.md)] では、(お客様のロゴなどのアップロードされた画像などの) 画像、[!INCLUDE[pn_JavaScript](pn-javascript.md)]、CSS などの静的なコンテンツをランタイムに提供するために、[!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] Content Delivery Network を使用します。  
  
[Azure Active Directory](https://azure.microsoft.com/services/active-directory/)  
  
[!INCLUDE[pn_gamification_shortest](pn-gamification-shortest.md)] では [!INCLUDE[pn_azure_active_directory](pn-azure-active-directory.md)] を使用してユーザーを認証したり、プラットフォームを使用する資格を判断したりします。