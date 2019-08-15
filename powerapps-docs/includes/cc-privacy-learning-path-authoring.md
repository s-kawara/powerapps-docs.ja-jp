[!INCLUDE[pn_dynamics_crm](pn-dynamics-crm.md)] 組織に対してラーニング パス作成を有効にすると、適切なセキュリティ特権を持つユーザーが作成したラーニング パスのコンテンツ (公開済みまたは下書き) が、[!INCLUDE[pn_Azure_SQL_Database_long](pn-azure-sql-database-long.md)] に保存されます。 さらに、この機能を有効にすると、[!INCLUDE[pn_azure_cloud_services](pn-azure-cloud-services.md)] で、[!INCLUDE[pn_dynamics_crm](pn-dynamics-crm.md)] 組織に関連付けられた以下のデータを取り込むことができます。  
  
-   テナント内の組織の一覧  
  
-   エンド ユーザーの [!INCLUDE[pn_dynamics_crm](pn-dynamics-crm.md)] クライアントおよび適用されるブラウザーや OS の構成  
  
-   エンド ユーザーの使用状況を表すデータ (ラーニング パスで費やした時間や、記録されたクリック数など)  
  
-   集計されたエンド ユーザーのデータ (場所、セキュリティ ロール、ユーザー言語)  
  
-   集計されたエンド ユーザーのデータ (場所、セキュリティ ロール、ユーザー言語)  
  
-   一字一句そのままの、エンド ユーザーからのフィードバック  
  
 管理者は、**システムの設定**ダイアログ ボックスの**全般**タブで、ラーニング パス作成を有効にすること (また、後から無効にすること) ができます。  
  
 ラーニング パス作成機能に関連する [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] コンポーネントとサービスについては、以下のセクションで説明します。  
  
 [!INCLUDE[cc_privacy_note_azure_trust_center](cc-privacy-note-azure-trust-center.md)]  
  
 [Cloud Services](https://azure.microsoft.com/services/cloud-services/)  
  
 **Web サービス**  
  
 Web サービスは、ラーニング パス ランタイムによってクライアントに表示されるコントロールを提供します。 また、ラーニング パス作成に使用される Designer API をサポートします。 コントロールは、このサービスによって [!INCLUDE[pn_Azure_SQL_Database_long](pn-azure-sql-database-long.md)] 上に保存されます。  
  
 **コンパイラ (ワーカー ロール)**  
  
 コンパイラ ロールは、公開グループへのコントロールの公開を管理します。 コンパイラはキューを使用して公開ジョブに関するメッセージを保存します。 結果は [!INCLUDE[pn_Azure_SQL_Database_long](pn-azure-sql-database-long.md)] に保存されます。  
  
 [Azure SQL Database](https://azure.microsoft.com/services/sql-database/)  
  
 ラーニング パスは [!INCLUDE[pn_Azure_SQL_Database_long](pn-azure-sql-database-long.md)] を使用して以下の情報を保存します。  
  
-   ラーニング パスを使って作成されたコントロール。  
  
-   構成に関連したラーニング パス作成。  
  
 [Azure Active Directory](https://azure.microsoft.com/services/active-directory/)  
  
 ラーニング パスは [!INCLUDE[pn_azure_active_directory](pn-azure-active-directory.md)] を使用して Web サービスを認証します。  
  
 [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/)  
  
 ラーニング パスは [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] Traffic Manager を使用して Web サービスの負荷分散を行い、可用性とパフォーマンスを高めます。  
  
 [Azure Storage キュー](https://azure.microsoft.com/services/storage/)  
  
 [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] Storage キューは、Web サービスとコンパイラ ロール間のやり取りの調整に使用されます。  
  
 [Azure Blob Storage](https://azure.microsoft.com/services/storage/)  
  
 ラーニング パスは [!INCLUDE[pn_azure_blob_storage](pn-azure-blob-storage.md)] を使用して静的コンテンツ (クライアント側の [!INCLUDE[pn_JavaScript](pn-javascript.md)]、画像、CSS コンテンツ) を保存します。  
  
 [Azure Content Delivery Network (CDN)](https://azure.microsoft.com/services/cdn/)  
  
 CDN は、クライアント側の静的コンテンツ ([!INCLUDE[pn_JavaScript](pn-javascript.md)]、画像、CSS ファイル) をキャッシュに保存するために使用されます。保存されたコンテンツはグローバル CDN ネットワークから提供されます。