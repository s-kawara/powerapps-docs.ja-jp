---
ms.openlocfilehash: ac90bfc27e03047cf422c44c83f550608d67b57e
ms.sourcegitcommit: ad203331ee9737e82ef70206ac04eeb72a5f9c7f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/18/2019
ms.locfileid: "67212848"
---
[!INCLUDE[pn_microsoftcrm](pn-microsoftcrm.md)] のポータル機能を有効にすると、顧客名、製品名、サポート案件番号、カスタム エンティティ データなどの [!INCLUDE[pn_dynamics_crm](pn-dynamics-crm.md)] データを、外部に開かれた [!INCLUDE[pn_dynamics_crm](pn-dynamics-crm.md)] ポータルを通じて公開できます。 ポータルを通じて公開されたデータは、キャッシュのために Microsoft [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] Web Apps のメモリに格納され、ポータル検索機能を有効にするためにローカル ハード ドライブ上のファイルとしても格納されます。

テナント管理者は、[!INCLUDE[pn_dyn_365_admin_center](../includes/pn-dyn-365-admin-center.md)]を使用して構成することで [!INCLUDE[pn_dynamics_crm](pn-dynamics-crm.md)] ポータルを有効にし、それにより選択した [!INCLUDE[pn_dynamics_crm](pn-dynamics-crm.md)] インスタンスにパッケージ (ソリューションとデータ) もインストールされます。 テナント管理者、またはポータル管理者として設定された [!INCLUDE[pn_dynamics_crm](pn-dynamics-crm.md)] ユーザーは、ポータルを通じて公開されるデータを指定できます。 後でポータル機能を無効にするには、テナント管理者は [!INCLUDE[pn_Office_365](pn-office-365.md)] でポータル アドオンのサブスクリプションをキャンセルできます。

ポータル機能に関連する重要な [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] のコンポーネントとサービスは次のとおりです。
- [Azure Web Apps](https://azure.microsoft.com/services/app-service/web/):[!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)]Web Apps は、で[!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)]ポータルをホストするために使用されます。
- [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/):[!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)]Traffic Manager は、実行中の Web Apps にユーザーをルーティングすることによって、サービスの高可用性を確保するために使用されます。 
- [Azure Service Bus](https://azure.microsoft.com/services/service-bus/):[!INCLUDE[pn_azure_service_bus](pn-azure-service-bus.md)](トピック/サブスクリプション) は、ポータルのキャッシュの無効化に使用されます。 [!INCLUDE[pn_azure_service_bus](pn-azure-service-bus.md)] はメッセージを一時的に格納します。これは、[!INCLUDE[pn_dynamics_crm](pn-dynamics-crm.md)] でポータル関連のレコードが変更されるとトリガーされ、キャッシュの無効化を行うために Web Apps に渡されます。 
- [Azure Key Vault](https://azure.microsoft.com/services/key-vault/):すべてのサービスは構成データを [!INCLUDE[pn_azure_key_vault](pn_azure_key_vault.md)] に格納します。
- [Azure Storage](https://azure.microsoft.com/services/storage/):組織、テナント、およびポータルに関連するデータは、ストレージ[!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)]に格納されます。
- [Azure Active Directory](https://azure.microsoft.com/services/active-directory/):すべての web サービスが[!INCLUDE[pn_azure_active_directory](pn-azure-active-directory.md)]認証に使用します。
