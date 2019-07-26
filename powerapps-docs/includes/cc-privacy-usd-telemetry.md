---
ms.openlocfilehash: 7b58f302f694246564d7073a954ecd53b1b25361
ms.sourcegitcommit: 982cab99d84663656a8f73d48c6fae03e7517321
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/28/2019
ms.locfileid: "67456897"
---
[!INCLUDE[pn_unified_service_desk](pn-unified-service-desk.md)] の品質向上プログラム機能では、オペレーティング システムの詳細、ブラウザーの詳細、[!INCLUDE[pn_unified_service_desk](../includes/pn-unified-service-desk.md)] のアプリケーション固有情報、クライアントをインストールするコンピューターの [!INCLUDE[pn_unified_service_desk](pn-unified-service-desk.md)] バージョンなど、[!INCLUDE[pn_unified_service_desk](pn-unified-service-desk.md)] の使用状況に関する情報が送信されます。 [!INCLUDE[pn_unified_service_desk](pn-unified-service-desk.md)] により、組織のインサイトへのセキュリティで保護された接続を通じて [!INCLUDE[cc_Microsoft](cc-microsoft.md)] に情報が送信され、[!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] Table Storage に格納されます。
  
> [!NOTE]
>  組織のインサイトによって、[!INCLUDE[pn_crm_shortest](pn-crm-shortest.md)] 組織のシステム管理者に、組織の使用状況に関する簡単な概要が提供されます。 システム管理者は、最もアクティブなユーザー、開始中の SDK 要求の数、SDK ユーザーによって表示されている数を確認することができます。
  
 Unified Service Desk の品質向上プログラム機能に関連する [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] コンポーネントおよびサービスの一覧を以下に示します。  
  
> [!NOTE]
>  その他の [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] サービスの詳細については、[Microsoft Azure セキュリティ センター](https://azure.microsoft.com/support/trust-center/)を参照してください。  
  
 [Cloud Services](https://azure.microsoft.com/services/cloud-services/) OrgInsights Data REST API (Web ロール)  
  
 この Web ロールは、組織のインサイトでデータを表示するグラフからの要求を受け入れます。 API によって [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] テーブルからの集計データが読み取られ、それが返されます。  
  
 [Azure Blob Storage](https://azure.microsoft.com/services/storage/blobs/)  
  
 監視エージェント (すべてのスケール グループのコンピューター上で稼働) によって [!INCLUDE[pn_crm_shortest](pn-crm-shortest.md)] 組織の未加工のテレメトリ データが収集され、ボンド形式 (バイナリ形式) で [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] Blob Storage にアップロードされます。  
  
 [Azure Table Storage](https://azure.microsoft.com/services/storage/tables/)  
  
 [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] Blob Storage の未加工のテレメトリ データが集計され、Azure Table Storage に格納されます。クラウド サービスがこれを読み取ります。  
  
 [Azure Active Directory](https://azure.microsoft.com/services/active-directory/)  
  
 組織のインサイトでは [!INCLUDE[pn_azure_active_directory](pn-azure-active-directory.md)] を使用して Web サービスを認証します。  
  
 [Azure Service Bus](https://azure.microsoft.com/services/service-bus/)  
  
 監視エージェントでは、[!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] Blob Storage にデータをアップロードするたびにメッセージが作成されてキューに入れられます。 これらのメッセージは CMA パイプによって取得され、アップロードされたデータが集計されます。