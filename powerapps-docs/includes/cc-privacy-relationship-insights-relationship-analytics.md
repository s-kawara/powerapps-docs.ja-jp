---
ms.openlocfilehash: 864bb7bde775f88cdf43ba5c453bd1ff02f81b85
ms.sourcegitcommit: 4042388fa5e7ef50bc59f9e35df330613fea29ae
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61577521"
---
リレーションシップ分析、埋め込みインテリジェンス機能、[!INCLUDE[pn_dynamics_crm](pn-dynamics-crm.md)] 顧客データ (ユーザーを特定できる情報など) は、[!INCLUDE[pn_customerinsight_full](pn-customer-insights-full.md)] に送信され、格納されます。これは、[!INCLUDE[pn_dynamics_crm](pn-dynamics-crm.md)] ユーザーおよび顧客間のリレーションシップ KPI を計算する目的で、Azure 内で実行されるサービスです。 データは一時的に [!INCLUDE[pn_azure_service_fabric](pn-azure-service-fabric.md)] に格納され、関係の正常性や傾向などの追加の出力用に処理され、さらにその情報は [!INCLUDE[pn_customerinsight_short](pn-customer-insights-short.md)] に、次に [!INCLUDE[pn_dynamics_crm](pn-dynamics-crm.md)] に返されます。  
  
 管理者は、[!INCLUDE[pn_microsoftcrm](pn-microsoftcrm.md)] 組織のソリューションとしてインストールすることで、Relationship Analytics 機能を有効にすることができます。 また、[!INCLUDE[pn_microsoftcrm](pn-microsoftcrm.md)] 組織から管理者がこの機能をアンインストールすることで、この機能を後で無効にすることができます。  
  
 データ ソースとして [!INCLUDE[pn_Exchange](pn-exchange.md)] データを有効にして、KPI の計算と他の分析の作成に使用される追加データを収集する目的で、[!INCLUDE[pn_customerinsight_full](pn-customer-insights-full.md)] から [!INCLUDE[pn_Exchange_Online](pn-exchange-online.md)] に [!INCLUDE[pn_dynamics_crm](pn-dynamics-crm.md)] 顧客データ (エンドユーザーを特定できる情報など) を送信します。  この機能を完全に有効にするには、[!INCLUDE[pn_Office_365](pn-office-365.md)][!INCLUDE[pn_Exchange](pn-exchange.md)] 管理者も [!INCLUDE[pn_Exchange](pn-exchange.md)] アプリケーションの別の同意書に同意するように依頼する必要があります。  両方の管理者が該当する製品を介して同意すると、[!INCLUDE[pn_Exchange](pn-exchange.md)] からメールと会議のメタデータが提供されます。この情報は [!INCLUDE[pn_customerinsight_full](pn-customer-insights-full.md)] に格納され、[!INCLUDE[pn_customerinsight_full](pn-customer-insights-full.md)] 管理者が決定した KPI 計算や場合によっては他の分析を改善する目的で使用されます。 リレーションシップ分析の構成でデータ ソースとして [!INCLUDE[pn_Exchange](pn-exchange.md)] データを無効にしても、[!INCLUDE[pn_Exchange](pn-exchange.md)] のデータは [!INCLUDE[pn_customerinsight_full](pn-customer-insights-full.md)] から削除されません。  [!INCLUDE[pn_customerinsight_full](pn-customer-insights-full.md)] の [!INCLUDE[pn_Exchange](pn-exchange.md)] データを削除するには、[!INCLUDE[pn_customerinsight_full](pn-customer-insights-full.md)] から直接削除する必要があります。  
  
 リレーションシップ分析に関係する [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] のコンポーネントやサービスについては、以下のセクションで説明します。  
  
 [!INCLUDE[cc_privacy_note_azure_trust_center](cc-privacy-note-azure-trust-center.md)]  
  
 **[!INCLUDE[pn_customerinsight_full](pn-customer-insights-full.md)]**  
  
 [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] で実行されるサービスである [!INCLUDE[pn_customerinsight_short](pn-customer-insights-short.md)] には、リレーションシップ分析機能の出力を計算する目的で、顧客に関する個人を特定できる情報などの [!INCLUDE[pn_dynamics_crm](pn-dynamics-crm.md)] データが格納されています。 [!INCLUDE[pn_customerinsight_short](pn-customer-insights-short.md)] のプレビューは、このような[プレビュー機能の補足的な使用条件](http://go.microsoft.com/fwlink/p/?LinkId=511446)に従います。  
  
 [Customer Insights のプレビューの詳細情報](https://azure.microsoft.com/en-us/services/customer-insights/)。  
  
 [Azure Service Fabric](https://azure.microsoft.com/services/service-fabric/)  
  
 [!INCLUDE[pn_azure_service_fabric](pn-azure-service-fabric.md)] は、リレーションシップ分析機能の出力を計算する目的で、顧客に関する個人を特定できる情報などの [!INCLUDE[pn_dynamics_crm](pn-dynamics-crm.md)] データを一時的に格納するために使用されます。