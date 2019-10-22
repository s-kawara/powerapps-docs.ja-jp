---
ms.openlocfilehash: f331670a2fd6b051c91a7fe2bfa607c54c9ab41a
ms.sourcegitcommit: ad203331ee9737e82ef70206ac04eeb72a5f9c7f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/18/2019
ms.locfileid: "67225244"
---
[!INCLUDE[pn-marketing-business-app-module-name](../includes/pn-marketing-business-app-module-name.md)] を有効にした場合、いくつかのマーケティング プロセスを実行するために、[!INCLUDE[pn-microsoftcrm](../includes/pn-microsoftcrm.md)] から特定の [!INCLUDE[pn-azure-shortest](../includes/pn-azure-shortest.md)] サービスへのデータ フローを許可することに同意したものとします。 これらのサービスはまとめて "[!INCLUDE[pn-marketing-app-module](../includes/pn-marketing-app-module.md)] サービス" と呼ばれます。

カスタマー ジャーニーを実行するために、[!INCLUDE[pn-marketing-business-app-module-name](../includes/pn-marketing-business-app-module-name.md)] は、顧客体験、電子メール、送信フォーム、およびマーケティング ページの定義を [!INCLUDE[pn_azure_service_fabric](../includes/pn_azure_service_fabric.md)] で実行されているこれらの [!INCLUDE[pn-marketing-app-module](../includes/pn-marketing-app-module.md)] サービスに送信する必要があります。 さらに、マーケティング ページは、[!INCLUDE[pn-microsoftcrm](../includes/pn-microsoftcrm.md)] に対するポータル機能のお客様のインスタンスに送信されます。

送信される電子メールを個人用に設定するために、[!INCLUDE[pn-marketing-business-app-module-name](../includes/pn-marketing-business-app-module-name.md)] は [!INCLUDE[pn-customer-insights-full](../includes/pn-customer-insights-full.md)] との間の送受信データ フローを有効にする必要があります。 [!INCLUDE[pn-customer-insights-full](../includes/pn-customer-insights-full.md)] サービスの詳細については以下を参照してください。 [!INCLUDE[pn-customer-insights-full](../includes/pn-customer-insights-full.md)] へのデータ フローには、連絡先の同期と [!INCLUDE[pn-customer-insights-full](../includes/pn-customer-insights-full.md)] に対するアカウントが含まれています。 [!INCLUDE[pn-marketing-app-module](../includes/pn-marketing-app-module.md)] サービスは、このデータを使用して電子メールの内容を個人用に設定します。 含まれるデータは、電子メールの定義によってのみ変わります。

リード スコア モデルとマーケティング セグメントを再計算するために、[!INCLUDE[pn-marketing-business-app-module-name](../includes/pn-marketing-business-app-module-name.md)] はリードのスコア モデル定義とセグメント定義を [!INCLUDE[pn-customer-insights-full](../includes/pn-customer-insights-full.md)] に送信し、これらの計算内で [!INCLUDE[pn-customer-insights-full](../includes/pn-customer-insights-full.md)] のプロファイルとやりとりを利用する必要があります。

[!INCLUDE[pn-marketing-app-module](../includes/pn-marketing-app-module.md)] サービスによってキャプチャされた電子メールとインターネットのやりとりについて分析情報を提供するために、収集されたデータは [!INCLUDE[pn-marketing-app-module](../includes/pn-marketing-app-module.md)] サービスから [!INCLUDE[pn-marketing-business-app-module-name](../includes/pn-marketing-business-app-module-name.md)] と [!INCLUDE[pn-customer-insights-full](../includes/pn-customer-insights-full.md)] の両方に流れます。

さらに、[!INCLUDE[pn-marketing-business-app-module-name](../includes/pn-marketing-business-app-module-name.md)] のイベント管理の統合が有効な場合、[!INCLUDE[pn-marketing-business-app-module-name](../includes/pn-marketing-business-app-module-name.md)] はイベントを ([!INCLUDE[pn-crm-online-shortest](../includes/pn-crm-online-shortest.md)] のコネクタを直接介して) [!INCLUDE[pn-customer-insights-full](../includes/pn-customer-insights-full.md)] と、(やりとりとして [!INCLUDE[pn-marketing-app-module](../includes/pn-marketing-app-module.md)] サービスを介して) イベント登録とチェックインに対して同期しています。

[!INCLUDE[pn-customer-insights-full](../includes/pn-customer-insights-full.md)] に関するデータ フローは以下のとおりです。
- 電子メールの個人用設定、リード スコアリング、セグメント化のコンテンツを提供するための、[!INCLUDE[pn-customer-insights-full](../includes/pn-customer-insights-full.md)] の通常の受信コネクタを使用する [!INCLUDE[pn-marketing-business-app-module-name](../includes/pn-marketing-business-app-module-name.md)] から [!INCLUDE[pn-customer-insights-full](../includes/pn-customer-insights-full.md)] へのエンティティ データ (主に連絡先とアカウント、最終的にはリードとイベントにもつながります)
- やりとりと分析情報の識別子を提供するための、[!INCLUDE[pn-marketing-business-app-module-name](../includes/pn-marketing-business-app-module-name.md)] から [!INCLUDE[pn-marketing-app-module](../includes/pn-marketing-app-module.md)] サービス経由の [!INCLUDE[pn-customer-insights-full](../includes/pn-customer-insights-full.md)] へのエンティティ データ (顧客体験、マーケティング電子メール、マーケティング ページ)
- [!INCLUDE[pn-marketing-app-module](../includes/pn-marketing-app-module.md)] サービスから [!INCLUDE[pn-customer-insights-full](../includes/pn-customer-insights-full.md)] へのやりとり (電子メールの追跡、Web サイトの追跡、顧客体験の進行状況)
- [!INCLUDE[pn-marketing-business-app-module-name](../includes/pn-marketing-business-app-module-name.md)] から [!INCLUDE[pn-marketing-app-module](../includes/pn-marketing-app-module.md)] サービス経由の [!INCLUDE[pn-customer-insights-full](../includes/pn-customer-insights-full.md)] へのやりとり (イベントの登録とチェックイン)
- [!INCLUDE[pn-customer-insights-full](../includes/pn-customer-insights-full.md)] から [!INCLUDE[pn-marketing-app-module](../includes/pn-marketing-app-module.md)] サービス経由の [!INCLUDE[pn-marketing-business-app-module-name](../includes/pn-marketing-business-app-module-name.md)] への [!INCLUDE[pn-insights](../includes/pn-insights.md)] (やりとりと KPI) (主に顧客体験と電子メールの送信の進行状況、リード スコアリング結果)
- [!INCLUDE[pn-customer-insights-full](../includes/pn-customer-insights-full.md)] から専用のサンドボックス化された [!INCLUDE[pn-marketing-business-app-module-name](../includes/pn-marketing-business-app-module-name.md)] 形式の UI 要素への直接の [!INCLUDE[pn-customer-insights-full](../includes/pn-customer-insights-full.md)] アプリ (セグメント化とウィジェット)

### <a name="marketing-services"></a>マーケティング サービス

[!INCLUDE[pn-marketing-business-app-module-name](../includes/pn-marketing-business-app-module-name.md)] は以下の [!INCLUDE[pn-azure-shortest](../includes/pn-azure-shortest.md)] サービスを使用します。

- [!INCLUDE[pn-azure-shortest](../includes/pn-azure-shortest.md)] Data Lake Store
- [!INCLUDE[pn-azure-shortest](../includes/pn-azure-shortest.md)] Data Lake Analytics
- [!INCLUDE[pn-azure-key-vault](../includes/pn-azure-key-vault.md)]
- [!INCLUDE[pn_azure_service_fabric](../includes/pn_azure_service_fabric.md)]
- [!INCLUDE[pn-azure-shortest](../includes/pn-azure-shortest.md)] DocumentDB
- [!INCLUDE[pn-microsoft-azure-active-directory](../includes/pn-microsoft-azure-active-directory.md)]
- [!INCLUDE[pn-azure-shortest](../includes/pn-azure-shortest.md)] Storage

> [!NOTE]
> その他の [!INCLUDE[pn-azure-shortest](../includes/pn-azure-shortest.md)] サービス オファリングについては、[!INCLUDE[cc_privacy_note_azure_trust_center](../includes/cc_privacy_note_azure_trust_center.md)] (<https://azure.microsoft.com/support/trust-center/>) に関するページを参照してください。

### [!INCLUDE[pn-customer-insights-full](../includes/pn-customer-insights-full.md)]

[!INCLUDE[pn-marketing-business-app-module-name](../includes/pn-marketing-business-app-module-name.md)] を使用すると、処理対象の顧客データを [!INCLUDE[pn-customer-insights-full](../includes/pn-customer-insights-full.md)] に転送する処理がアクティブになります。 [!INCLUDE[pn-microsoftcrm](../includes/pn-microsoftcrm.md)] のために [!INCLUDE[pn-customer-insights-short](../includes/pn-customer-insights-short.md)] を使用するには、特定のプライバシーに関する法律に準拠する必要があります。 不明な点がある場合は、お客様の組織内の適切な担当者におたずねください。

現段階では、[!INCLUDE[pn-customer-insights-short](../includes/pn-customer-insights-short.md)] はパブリック プレビュー段階であり、[!INCLUDE[pn-marketing-business-app-module-name](../includes/pn-marketing-business-app-module-name.md)] または [!INCLUDE[pn-microsoftcrm](../includes/pn-microsoftcrm.md)] Customer Engagement と同じレベルのプライバシーとセキュリティ コミットメントを提供していません。 [!INCLUDE[pn-customer-insights-short](../includes/pn-customer-insights-short.md)] はネイティブで [!INCLUDE[pn-azure-shortest](../includes/pn-azure-shortest.md)] サービスに基づいて構築され、適用可能な各 [!INCLUDE[pn-azure-shortest](../includes/pn-azure-shortest.md)] サービスのコンプライアンスとセキュリティ標準が適用されます。 詳細については、[!INCLUDE[cc-microsoft](../includes/cc-microsoft.md)] セキュリティ センターを参照してください。[https://azure.microsoft.com/support/trust-center/](https://azure.microsoft.com/support/trust-center/)

[!INCLUDE[pn-customer-insights-short](../includes/pn-customer-insights-short.md)] は以下の [!INCLUDE[pn-azure-shortest](../includes/pn-azure-shortest.md)] サービスを使用します。

- [!INCLUDE[pn-azure-shortest](../includes/pn-azure-shortest.md)] Data Lake Store
- [!INCLUDE[pn-azure-shortest](../includes/pn-azure-shortest.md)] Data Lake Analytics
- [!INCLUDE[pn-azure-shortest](../includes/pn-azure-shortest.md)] HDInsight (Spark、Phoenix、HBase)
- [!INCLUDE[pn-ms-azure-sql-database](../includes/pn-ms-azure-sql-database.md)]
- [!INCLUDE[pn-azure-key-vault](../includes/pn-azure-key-vault.md)]
- [!INCLUDE[pn-azure-shortest](../includes/pn-azure-shortest.md)] Secret Store
- [!INCLUDE[pn-azure-shortest](../includes/pn-azure-shortest.md)] Event Hub
- [!INCLUDE[pn-azure-stream-analytics](../includes/pn-azure-stream-analytics.md)]
- [!INCLUDE[pn-azure-shortest](../includes/pn-azure-shortest.md)] Redis Cache
- [!INCLUDE[pn_azure_service_fabric](../includes/pn_azure_service_fabric.md)]
- [!INCLUDE[pn-microsoft-azure-active-directory](../includes/pn-microsoft-azure-active-directory.md)]
- [!INCLUDE[pn-azure-shortest](../includes/pn-azure-shortest.md)] Monitoring
- [!INCLUDE[pn-azure-shortest](../includes/pn-azure-shortest.md)] Metrics
- [!INCLUDE[pn-azure-shortest](../includes/pn-azure-shortest.md)] Websites
- [!INCLUDE[pn_azure_service_bus](../includes/pn_azure_service_bus.md)]
- [!INCLUDE[pn-azure-shortest](../includes/pn-azure-shortest.md)] Storage
