---
ms.openlocfilehash: 509ad3f5b1b94378b2c6fd7661510b7aef0e3a23
ms.sourcegitcommit: 4042388fa5e7ef50bc59f9e35df330613fea29ae
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61574929"
---
[!INCLUDE[pn_dynamics_crm](pn-dynamics-crm.md)] 組織のラーニング パスの作成を有効にすると、(適切なセキュリティ特権を持つ) ユーザーが作成したラーニング パス コンテンツ (公開済みまたは下書き) が [!INCLUDE[pn_Azure_SQL_Database_long](pn-azure-sql-database-long.md)] に格納されます。 さらに、この機能を有効にすると、[!INCLUDE[pn_azure_cloud_services](pn-azure-cloud-services.md)] から [!INCLUDE[pn_dynamics_crm](pn-dynamics-crm.md)] 組織に関連付けられた以下のデータを取得できます。  
  
-   テナント内の組織の一覧  
  
-   エンド ユーザーの [!INCLUDE[pn_dynamics_crm](pn-dynamics-crm.md)] クライアントと該当するブラウザー/OS の構成  
  
-   ラーニング パスに費やされた時間や記録されたクリック数など、エンド ユーザーの使用状況データ  
  
-   集計されたエンドユーザー データ - 場所、セキュリティ ロール、ユーザー言語  
  
-   集計されたエンドユーザー データ - 場所、セキュリティ ロール、ユーザー言語  
  
-   エンド ユーザーからの逐語的なフィードバック  
  
 管理者は、**[システム設定]** ダイアログ ボックスの **[全般]** タブの設定を使用して、[ラーニング パスの作成] を有効にすることができます (また、後で無効にすることができます)。  
  
 ラーニング パスの作成機能と関係する [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] のコンポーネントやサービスについては、以下のセクションで詳しく説明します。  
  
 [!INCLUDE[cc_privacy_note_azure_trust_center](cc-privacy-note-azure-trust-center.md)]  
  
 [Cloud Services](https://azure.microsoft.com/en-us/services/cloud-services/)  
  
 **Web サービス**  
  
 Web サービスは、ラーニング パス ランタイムによってクライアント上にレンダリングされるコントロールを提供します。 Web サービスは、ラーニング パスの作成で使用される Designer API もサポートしています。 コントロールはサービスによって [!INCLUDE[pn_Azure_SQL_Database_long](pn-azure-sql-database-long.md)] に格納されます。  
  
 **コンパイラ (worker ロール)**  
  
 コンパイラ ロールは、公開グループに対するコントロールの公開を管理します。 コンパイラは、キューを使用して、公開ジョブに関するメッセージを格納します。 結果は [!INCLUDE[pn_Azure_SQL_Database_long](pn-azure-sql-database-long.md)] に格納されます。  
  
 [Azure SQL Database](https://azure.microsoft.com/en-us/services/sql-database/)  
  
 ラーニング パスは以下の格納に [!INCLUDE[pn_Azure_SQL_Database_long](pn-azure-sql-database-long.md)] を使用します。  
  
-   ラーニング パスを使用して作成されるコントロール。  
  
-   構成に関連するラーニング パスの作成。  
  
 [Azure Active Directory](https://azure.microsoft.com/en-us/services/active-directory/)  
  
 ラーニング パスは、Web サービスの認証に [!INCLUDE[pn_azure_active_directory](pn-azure-active-directory.md)] を使用します。  
  
 [Azure Traffic Manager](https://azure.microsoft.com/en-us/services/traffic-manager/)  
  
 ラーニング パスは、可用性とパフォーマンスの目的で Web サービスの負荷を分散するために [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] Traffic Manager を使用します。  
  
 [Azure Storage キュー](https://azure.microsoft.com/en-us/services/storage/)  
  
 [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] Storage キューは、Web サービスとコンパイラ ロール間の通信を調整するために使用されます。  
  
 [Azure Blob Storage](https://azure.microsoft.com/en-us/services/storage/)  
  
 ラーニング パスは、静的コンテンツ (クライアント側の [!INCLUDE[pn_JavaScript](pn-javascript.md)]、画像、CSS コンテンツ) を格納するために [!INCLUDE[pn_azure_blob_storage](pn-azure-blob-storage.md)] を使用します。  
  
 [Azure Content Delivery Network (CDN)](https://azure.microsoft.com/en-us/services/cdn/)  
  
 CDN は、クライアント側の静的コンテンツ ([!INCLUDE[pn_JavaScript](pn-javascript.md)]、画像、CSS ファイル) をキャッシュして、グローバル CDN ネットワークから配信するために使用されます。