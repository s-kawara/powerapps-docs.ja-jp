---
ms.openlocfilehash: 3fb3961dc88033a44c60c4b6f09124c7c38a11bf
ms.sourcegitcommit: ad203331ee9737e82ef70206ac04eeb72a5f9c7f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/18/2019
ms.locfileid: "67212782"
---
Dynamics 365 のお客様の声を有効にした場合、Dynamics 365 から調査を発行すると、調査の定義が Azure に送信され、Azure Storage に格納されます。 (電子メールで送信された調査への招待リンクを回答者が開き) 調査を送信すると、調査の回答は一時的に Azure Service Bus に格納され、その後 Dynamics 365 によって取得され格納されます。 回答が Dynamics 365 に格納されると、それらは Azure から削除されます。  
  
 なお、回答者の調査のレンダリング時に、調査に (質問や回答などの調査要素に) Dynamics 365 の顧客名、製品名、サポート案件番号などのデータを含めることができます。 調査の招待リンクが生成されると、この Dynamics 365 データは Dynamics 365 から送信され、調査の招待リンク内で使用されている ID と引き換えで Azure SQL Database に格納されます。 この識別子は、調査の招待リンクを使用して調査が開かれた後に、調査の Dynamics 365 データを表示するために使用されます。 回答者へメールを介して送信される調査リンクの ID は、回答者のメール システムに格納されます。  
  
 Dynamics 365 のお客様の声の機能は、管理者がそれを Dynamics 365 組織のソリューションにインストールすることによって有効にすることができます。 また、Dynamics 365 組織から管理者がこの機能をアンインストールすることにより、この機能を後で無効にすることができます。  
  
 Dynamics 365 のお客様の声機能と関係する Azure のコンポーネントやサービスについては、以下のセクションで詳細に説明しています。  
  
 メモ:その他の Azure サービスオファリングの詳細については、Microsoft Azure[https://azure.microsoft.com/support/trust-center/](https://azure.microsoft.com/support/trust-center/)Trust Center () を参照してください。  
  
 **Cloud Services** ([https://azure.microsoft.com/services/cloud-services/](https://azure.microsoft.com/services/cloud-services/))  
  
 **デザイナー サービス (Web ロール)**  
  
 これは、Dynamics 365 組織とマルチテナント型 Dynamics 365 のお客様の声の Azure コンポーネント間の通信のために複数の Web サービスを提供します。  たとえば、調査は Azure Blob Storage に発行され格納されます。  調査の回答は、Azure Service Bus のキューから取得され、Dynamics 365 組織内で保持されるよう返されます。  すべての要求は Azure Active Directory に対して認証されます。  
  
 **調査ランタイム (Web ロール)**  
  
 これは、回答者に調査を提供する Web アプリケーションです。  送信された調査の回答は、Dynamics 365 の非同期サービスによって処理され取得される前に、Azure Service Bus キューに一時的に格納されます。  
  
 **応答処理 (Worker ロール)**  
  
 この worker ロールは、完了した生の調査を、Dynamics 365 で作成できる有効な調査回答に処理します。  
  
 **プッシュプロセッサ (Worker ロール)**  このワーカーロールは、有効なアンケートの応答を処理し、Dynamics 365 エンティティレコードとして更新します。 
 
 **Azure Key Vault** ([https://azure.microsoft.com/services/key-vault/](https://azure.microsoft.com/services/key-vault/))  
  
 構成データは、いずれのクラウド サービスでも Azure Key Vault に格納されます。  組織、テナント データは SQL Azure に格納されます。  
  
 **Azure SQL Database** ([https://azure.microsoft.com/services/sql-database/](https://azure.microsoft.com/services/sql-database/))  
  
 Dynamics 365 のお客様の声では、SQL Azure を使用して次を格納します。  
  
-   パイプされたデータ  
  
-   調査のメタデータ  
  
-   組織 (テナント) データ  
  
 **Azure Blob Storage** ([https://azure.microsoft.com/services/storage/](https://azure.microsoft.com/services/storage/))  
  
 調査の定義と部分的に完了している (保存されている) 回答は、Azure Blob Storage に格納されます。  
  
 **Azure Content Delivery Network (CDN)** ([https://azure.microsoft.com/services/cdn/](https://azure.microsoft.com/services/cdn/))  
  
 Dynamics 365 のお客様の声ソリューションでは、(お客様のロゴなどのアップロードされた画像などの) 画像、JavaScript および CSS などの調査ランタイムに調査の静的なコンテンツを処理させるために、Azure Content Delivery Network を使用します。  
  
 **Azure Active Directory** ([https://azure.microsoft.com/services/active-directory/](https://azure.microsoft.com/services/active-directory/))  
  
 Dynamics 365 のお客様の声ソリューションでは、Web サービスの認証に Azure Active Directory サービスを使用します。  
  
 **Azure Service Bus** ([https://azure.microsoft.com/services/service-bus/](https://azure.microsoft.com/services/service-bus/))  
  
 調査の表示および送信時に作成されたメッセージは、Azure の worker ロールが調査の回答を組織の Dynamics 365 インスタンスにプッシュして、それが Dynamics 365 エンティティ レコードに保存されるまで、組織 (テナント) の Azure Service Bus キューに一時的に保存されます。
