静的 HTML であるラーニング パス機能を有効にすると、イメージやスクリプトを [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] コンテンツ配信ネットワーク (CDN) に保存できます。 また、表示されたすべての動的コンテンツは [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] Redis Cache に保存され、[!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] SQL データベースからの事前キャッシュに使用されます。  
  
 管理者は、[!INCLUDE[pn_microsoftcrm](pn-microsoftcrm.md)] 組織の [ガイド付きヘルプを有効にする] の設定を使用して、[!INCLUDE[pn_crm_online_shortest](pn-crm-online-shortest.md)] インスタンス内でのラーニング パス機能の使用を有効または無効にできます。  
  
 ラーニング パス機能に関連する [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] コンポーネントとサービスについては、以下のセクションで説明します。  
  
> [!NOTE]
>  その他の Azure サービス内容については、[Microsoft Azure セキュリティ センター](https://azure.microsoft.com/support/trust-center/) を参照してください。  
  
 [Cloud Services](https://azure.microsoft.com/services/cloud-services/)  
  
 **ラーニング パスのランタイム (Web ロール)**  
  
 これは、ユーザーにコンテンツを提供する アプリケーションです。  
  
 **ラーニング パス サービス (ワーカー ロール)**  
  
 ワーカー ロールは、[!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] SQL データベースからのデータを処理し、[!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] Redis Cache にキャッシュします。  
  
 [Azure SQL Database](https://azure.microsoft.com/services/sql-database/)  
  
 ラーニング パスは SQL データベースを使用して以下を保存します。  
  
-   内容  
  
-   コンテンツ メタデータ  
  
-   システム メタデータ  
  
 [Azure Blob Storage](https://azure.microsoft.com/services/storage/)  
  
 HTML、イメージ、[!INCLUDE[pn_JavaScript](pn-javascript.md)]、および CSS は、すべて [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] BLOB ストレージに保存されます。  
  
 [Azure Content Delivery Network (CDN)](https://azure.microsoft.com/services/cdn/)  
  
 ラーニング パスは [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] Content Delivery Network を使って HTML、イメージ、[!INCLUDE[pn_JavaScript](pn-javascript.md)]、CSS などの静的コンテンツを調査ランタイムに送ります。  
  
 [Azure Active Directory](https://azure.microsoft.com/services/active-directory/)  
  
 ラーニング パスは [!INCLUDE[pn_azure_active_directory](pn-azure-active-directory.md)] サービスを使用してデザイナー専用の Web サービスを認証します。 現在、デザイナーは顧客およびパートナーには公開されていません。 そのため、認証は [!INCLUDE[cc_Microsoft](cc-microsoft.md)] ドメイン内でのみ行われます。  
  
 [Azure Redis Cache](https://azure.microsoft.com/services/cache/)  
  
 ラーニング パスは [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] Redis Cache を使用して、ユーザーに提供する動的コンテンツをキャッシュします。  
  
 [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/)  
  
 ラーニング パスは Traffic Manager を使用して [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] または外部のサービス拠点とサービスを監視し、エラーが発生した場合にユーザーを自動的に新しい場所に誘導することにより、重要なアプリケーションの可用性を高めます。  
  
 [Azure Resource Manager](https://azure.microsoft.com/features/resource-manager/)  
  
 ラーニング パスは [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] リソース マネージャーを使用して CDN、Redis Cache、SQL データベース、クラウド サービスをリソース グループとして展開し、整合した状態を保って、繰り返し展開できるようにします。