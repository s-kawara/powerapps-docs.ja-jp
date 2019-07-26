---
ms.openlocfilehash: fa4a17c2a3131f49f8a702388bdb405661855c10
ms.sourcegitcommit: 483c777a1537ccab6a2a2da6a5d1fe4470dd0e7e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2019
ms.locfileid: "61550021"
---
イベント管理の使用条件を承諾すると、ウェビナー統合機能が有効になります。 ウェビナー統合機能では、パートナー ウェビナー プロバイダーを活用し、ウェビナーとしてイベントやセッションが実施されます。 ウェビナー プロバイダー サービスを使用するには、サービスのアカウントを用意する必要があります。 現時点ですぐに利用できる唯一のパートナー ウェビナー プロバイダー サービスが ON24 です。 ウェビナー統合機能を使用するとき、ウェビナーを提供し、実行するために不可欠なデータが処理され、[!INCLUDE[pn-azure-service-fabric](../includes/pn-azure-service-fabric.md)] に保存され、ON24 に送信されます。 このようなデータには、名前、メール、社名など、ウェビナー参加者の登録データが含まれることがあります。 また、ON24 は、ウェビナーの視聴時間など、ウェビナーの指標を [!INCLUDE[pn-azure-service-fabric](../includes/pn-azure-service-fabric.md)] 経由で [!INCLUDE[pn-microsoftcrm](../includes/pn-microsoftcrm.md)] に送信することがあります。

イベント管理ソリューションの残りの部分を使用する目的でウェビナー機能を有効にする必要はありません。 管理者は、ウェビナー構成で資格情報を削除することで、ウェビナー統合機能をオフにすることができます。

ウェビナー統合機能によって使用される [!INCLUDE[pn-windows-azure](../includes/pn-windows-azure.md)] のコンポーネントとサービス:

- [!INCLUDE[pn_azure_key_vault](../includes/pn_azure_key_vault.md)] ([!INCLUDE[proc-more-information](../includes/proc-more-information.md)] [Azure Key Vault とは](https://docs.microsoft.com/azure/key-vault/key-vault-whatis))
  - 顧客の ON24 アカウント資格情報を暗号化/復号するための暗号化キーを提供します
- [!INCLUDE[pn-azure-service-fabric](../includes/pn-azure-service-fabric.md)] ([!INCLUDE[proc-more-information](../includes/proc-more-information.md)] [Azure Service Fabric の概要](https://docs.microsoft.com/azure/service-fabric/service-fabric-overview))
  - 登録データとウェビナー アカウント資格情報を処理し、ON24 に送信します
  - ON24 からウェビナーの指標を読み出し、[!INCLUDE[pn-microsoftcrm](../includes/pn-microsoftcrm.md)] に送信します - 顧客の ON24 アカウント資格情報を保存します (カスタム暗号化)