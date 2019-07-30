---
ms.openlocfilehash: 1cdcb40245aae9a23ecb6d3392e412f8a60b95ba
ms.sourcegitcommit: ad203331ee9737e82ef70206ac04eeb72a5f9c7f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/18/2019
ms.locfileid: "67212305"
---
[!INCLUDE[pn_microsoftcrm](pn-microsoftcrm.md)] で推奨事項モデルを構築するときに、製品に関する推奨事項機能を有効にすると、構成されているバスケット データ エンティティに基づくトランザクション データの履歴およびそのフィルターが、[!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] に送信され、[!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] で処理され、[!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] Storage に一時的に格納され、最終的に機械学習モデルを構築するために Azure Recommendations API に送信されます。 Azure Recommendations API でモデルが構築されたら、データは [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] Storage から削除されます。 なお、推奨事項モデルの構築には、[!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] に ID (アカウント ID、製品 ID、トランザクション ID) のみが送信されます。

管理者は、製品に関する推奨事項機能を [!INCLUDE[pn_microsoftcrm](pn-microsoftcrm.md)] 組織の **[設定]** &gt; **[管理]** &gt; **[システム設定]** &gt; **[プレビュー]** タブで有効にできます。 推奨事項モデルが構築された場合のみ、データは Azure Recommendations API に送信されます。 システム管理者には、Azure Recommendations API で共有されているデータを削除する、既存のモデルを削除するオプションはありません。 また、システム管理者が Azure Recommendations API への接続を削除して、今後いかなる推奨事項モデルも構築されないようにすることも可能です。

製品に関する推奨事項に関係する [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] のコンポーネントやサービスについては、以下のセクションで説明しています。

[!INCLUDE[cc_privacy_note_azure_trust_center](cc-privacy-note-azure-trust-center.md)]

[Azure Logic Apps](https://azure.microsoft.com/services/app-service/logic/)

これは、推奨事項モデル バージョンを構築するために Recommendations API を使用して製品カタログとトランザクション データを同期する調整されたデータ パイプラインを提供します。 このパイプラインは、Dynamics 365 組織と Recommendations API 間での通信のために、複数の API アプリが使用されたマルチテナント サービスとして実行されます。 Logic Apps は、モデル バージョン ID および [!INCLUDE[pn_dynamics_crm](pn-dynamics-crm.md)] 組織の URL などの最小限のコンテキストで [!INCLUDE[pn_dynamics_crm](pn-dynamics-crm.md)] からトリガーされます。 

[Azure API Apps](https://azure.microsoft.com/services/app-service/api/)

これらは、[!INCLUDE[pn_dynamics_crm](pn-dynamics-crm.md)] 組織からデータを読み取る Web ジョブをトリガーする、推奨モデルを構築するために Recommendations API にデータを送信する Web アプリケーションです。 3 つの API アプリと対応する Web ジョブがあります。1 つは製品データを読み取り、1 つはトランザクション データを読み取り、1 つは推奨事項モデルを構築します。 API アプリは Web ジョブを使用し、バックグラウンドで実際のデータ処理を実行し、[!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] Blob Storage にデータの出力を書き込みます。 データは一時的に [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] Blob Storage に格納されます。 モデルが構築されると、データは最終的に [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] Storage から削除されます。

[Azure テーブル](https://azure.microsoft.com/services/storage/tables/)

[!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] テーブルは、API アプリと Web ジョブ間でモデルのバージョンと組織のコンテンツをやりとりするために使用されます。

[Azure Blob Storage](https://azure.microsoft.com/services/storage/) 

データは一時的に Web ジョブにより [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] Blob Storage に格納され、Logic App パイプラインが実行を終了すると削除されます。

[Azure Recommendations API](https://www.microsoft.com/cognitive-services/en-us/recommendations-api) Azure Recommendations API には、推奨事項モデルを構築するための最小限のデータ製品 ID、トランザクション ID、およびアカウント ID が送信されます。 データは対応するモデル バージョンが存在するまで、Recommendations API サービスに格納されます。
