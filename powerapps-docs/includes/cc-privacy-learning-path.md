---
ms.openlocfilehash: 3840a097743111f6ae89e65426a366207f8364d9
ms.sourcegitcommit: 4042388fa5e7ef50bc59f9e35df330613fea29ae
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61574920"
---
ラーニング パス機能 (静的 HTML) を有効にすることで、イメージやスクリプトを [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] Content Delivery Network (CDN) 上に格納することができます。 さらに、表示されるすべての動的なコンテンツが [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] Redis Cache に格納されます。これは [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] SQL データベースから事前キャッシュするために使用されます。  
  
 管理者は、[!INCLUDE[pn_microsoftcrm](pn-microsoftcrm.md)] 組織の [ガイド付きヘルプを有効にする] 設定を使用することで、[!INCLUDE[pn_crm_online_shortest](pn-crm-online-shortest.md)] インスタンス内でのラーニング パス機能の使用を有効または無効にすることができます。  
  
 ラーニング パス機能と関係する [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] のコンポーネントやサービスについては、以下のセクションで詳しく説明します。  
  
> [!NOTE]
>  その他の Azure サービスについて詳しくは、[Microsoft Azure セキュリティ センター](https://azure.microsoft.com/en-us/support/trust-center/)をご覧ください。  
  
 [Cloud Services](https://azure.microsoft.com/en-us/services/cloud-services/)  
  
 **ラーニング パス ランタイム (Web ロール)**  
  
 これがユーザーにコンテンツを提供する Web アプリケーションです。  
  
 **ラーニング パス サービス (worker ロール)**  
  
 worker ロールは、[!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] SQL Database からのデータの処理と、そのデータの [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] Redis Cache へのキャッシュを担当します。  
  
 [Azure SQL Database](https://azure.microsoft.com/en-us/services/sql-database/)  
  
 ラーニング パスでは次のものを格納するために SQL Database が使用されます。  
  
-   コンテンツ  
  
-   コンテンツのメタデータ  
  
-   システムのメタデータ  
  
 [Azure Blob Storage](https://azure.microsoft.com/en-us/services/storage/)  
  
 HTML、イメージ、[!INCLUDE[pn_JavaScript](pn-javascript.md)]、CSS はすべて [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)]Blob ストレージに格納されます。  
  
 [Azure Content Delivery Network (CDN)](https://azure.microsoft.com/en-us/services/cdn/)  
  
 ラーニングパスでは、調査ランタイムに静的コンテンツを提供するために [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] Content Delivery Network が使用されます (HTML、イメージ、[!INCLUDE[pn_JavaScript](pn-javascript.md)]、CSS など)。  
  
 [Azure Active Directory](https://azure.microsoft.com/en-us/services/active-directory/)  
  
 ラーニングパスでは、デザイナー専用に Web サービスを認証するために、[!INCLUDE[pn_azure_active_directory](pn-azure-active-directory.md)] サービスが使用されます。 現時点では、デザイナーは顧客やパートナーには公開されません。 したがって、認証は [!INCLUDE[cc_Microsoft](cc-microsoft.md)] ドメイン内でのみ行われます。  
  
 [Azure Redis Cache](https://azure.microsoft.com/en-us/services/cache/)  
  
 ラーニングパスでは、ユーザーに提供する動的コンテンツをキャッシュするために [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] Redis Cache が使用されます。  
  
 [Azure Traffic Manager](https://azure.microsoft.com/en-us/services/traffic-manager/)  
  
 ラーニングパスでは、重要なアプリケーションの可用性を向上させるために Traffic Manager が使用されます。[!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] または外部のサイトとサービスが監視され、障害発生時には必ず自動的にユーザーが新しい場所に転送されます。  
  
 [Azure Resource Manager](https://azure.microsoft.com/en-us/features/resource-manager/)  
  
 ラーニングパスでは、CDN、Redis Cache、SQL Database、クラウド サービスをリソース グループとして配置するために、[!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] Resource Manager が使用されます。こうすることで、これらを一貫した状態に保ち、繰り返し配置することが可能になります。