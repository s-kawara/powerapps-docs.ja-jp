---
ms.openlocfilehash: 80997689e9d4ebca8eb4809cc3e94dab549482b5
ms.sourcegitcommit: 4042388fa5e7ef50bc59f9e35df330613fea29ae
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61577553"
---
テキスト分析機能を有効にすることで、[!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] Cognitive Services の Text Analytics API を活用する [!INCLUDE[pn_dynamics_crm](pn-dynamics-crm.md)] 内の依存機能を有効にして高度な分析情報を利用できます。 このような依存機能は次のとおりです。  
  
-   ナレッジの提案  
  
-   ケース トピック分析  
  
-   類似したケースの提案  
  
 管理者は、[!INCLUDE[pn_microsoftcrm](pn-microsoftcrm.md)] 組織の **[設定]** > **[管理]** > **[システム設定]** > **[プレビュー]** タブでテキスト分析機能を有効にできます。  
  
 テキスト分析機能を有効にすると、[!INCLUDE[pn_microsoftcrm](pn-microsoftcrm.md)] 内でテキスト分析ベースのナレッジの提案を設定した場合に、ケースとその関連エンティティのデータが [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] Text Analytics API に送信されてキーワードやフレーズが抽出されます。 [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] Text Analytics API を使用してデータが格納されることはありません。 ナレッジ記事構成で構成済みのフィールドのみが [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] Text Analytics API に送信され、用語が抽出されます。 管理者またはカスタマイザーは、ナレッジ記事構成を非アクティブ化して、[!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] Text Analytics API に対する API 呼び出しを停止させることができます。 また、カスタマイザーは、ケース エンティティ フォーム構成でフィールド ベースの提案に戻すことで、テキスト分析ベースの提案の使用をやめることもできます。  
  
 テキスト分析機能を有効にすると、[!INCLUDE[pn_microsoftcrm](pn-microsoftcrm.md)] 内でケース トピック分析を設定した場合に、ケースとその関連エンティティのデータが [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] Text Analytics API に送信されてトピックが決定されます。 [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] Text Analytics API を使用してデータが格納されることはありません。 トピック モデル構成で構成済みのフィールドのみが [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] Text Analytics API に送信され、トピックが抽出されます。 管理者またはカスタマイザーは、トピック モデルを非アクティブ化して、[!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] Text Analytics API の呼び出しを停止させることができます。  
  
 テキスト分析機能を有効にすると、[!INCLUDE[pn_microsoftcrm](pn-microsoftcrm.md)] 内で類似したケース提案を設定するときに、類似ルールで高度なテキスト分析オプションが有効になっている場合、ケースとその関連エンティティのデータが [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] Text Analytics API に送信されてキーワードとフレーズが抽出されます。 類似ルール内で構成されているテキスト フィールドのみが [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] Text Analytics API に送信されます。 [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] Text Analytics API を使用してデータが格納されることはありません。 管理者またはカスタマイザーは、類似ルールを非アクティブ化して、[!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] Text Analytics API の呼び出しを停止させることができます。  
  
 テキスト分析ベースの機能に関係する [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] のコンポーネントやサービスについては、以下のセクションで説明します。  
  
 [!INCLUDE[cc_privacy_note_azure_trust_center](cc-privacy-note-azure-trust-center.md)]  
  
 [Azure API Apps](https://azure.microsoft.com/services/app-service/api/)  
  
 [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] API アプリでは、[!INCLUDE[pn_dynamics_crm](pn-dynamics-crm.md)] 組織からデータを読み取り、Text Analytics API にデータを送信してトピック分析を行う、Web ジョブがトリガーされます。 [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] API アプリは Web ジョブを使用し、バックグラウンドで実際のデータ処理を実行し、[!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] Blob Storage にデータの出力を書き込みます。 データは一時的に [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] Blob Storage に格納されます。 トピックが決定されると、データは最終的に [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] Storage から削除されます。  
  
 [Azure Scheduler](https://azure.microsoft.com/services/storage/)  
  
 [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] Scheduler は、スケジュールに基づいて Web ジョブをトリガーし、トピック分析を実行するために使用されます。 スケジューラと共有されるものは、トピック モデルのビルド スケジュールのみです。  
  
 [Azure テーブル](https://azure.microsoft.com/services/storage/)  
  
 [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] テーブルは、[!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] API アプリと Web ジョブ間でモデルのバージョンと組織のコンテンツをやりとりするために使用されます。  
  
 [Azure Blob Storage](https://azure.microsoft.com/services/storage/)  
  
 Web ジョブによってデータは一時的に [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] Blob Storage に格納され、Logic App パイプラインの実行が終了すると削除されます。  
  
 [Azure Text Analytics API](https://www.microsoft.com/cognitive-services/en-us/text-analytics-api)  
  
 アクティブなナレッジ検索フィールド、トピック モデル構成、または類似ルール構成で構成されているフィールドに基づいたデータが、[!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] Text Analytics API に送信されます。 たとえば、タイトルや説明、さらに関連メモやアクティビティの説明フィールドなどのケース エンティティ フィールドは、ナレッジ検索フィールドの構成で構成されます。  
  
 [!INCLUDE[pn_dynamics_crm](pn-dynamics-crm.md)] 関連性検索  
  
 管理者が関連性検索を有効にしている場合は、これを使用してケースの類似するレコードを検索できます。 類似ルール内で使用されるテキストの一致フィールドと完全一致フィールドが使用されて、関連性検索の API が呼び出されます。 データ処理について詳しくは、[!INCLUDE[pn_dynamics_crm](pn-dynamics-crm.md)] 関連性検索の技術コンテンツをご覧ください。