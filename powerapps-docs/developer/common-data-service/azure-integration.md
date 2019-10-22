---
title: Azure の統合 (Common Data Service) | Microsoft Docs
description: <Description>
ms.custom: ''
ms.date: 06/01/2019
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: brandonsimons
ms.author: jdaly
manager: ryjones
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="azure-integration"></a>Azure 統合

Common Data Service は、Azureとの統合に対応しています。 開発者は Common Data Service にプラグインを登録し、実行コンテキストと呼ばれるランタイムメッセージデータを、クラウド内の1つ以上のAzureソリューションに渡すことができます。 これは特に重要です。なぜなら Azure は、プラグインで取得された実行時コンテキストを外部の基幹業務 (LOB) アプリケーションに伝達するためにサポートされている 2 つのソリューションの 1 つだからです。 もう 1 つのソリューションは、サンドボックスに登録されたプラグインから外部のカスタム エンドポイントへのアクセス機能です。

Azure Service Busは Common Data Service ランタイムデータと外部クラウドベースの基幹業務(LOB)アプリケーションの間で、安全かつ信頼性の高い通信チャネルを提供します。 この機能は異なる Common Data Service システムやその他の Common Data Service サーバーを変更されたビジネス データと同期させる場合に特に役立ちます。

## <a name="key-elements-of-the-connection"></a>接続の主な要素  

 Common Data Service とAzure Service Bus 間の接続を実装する主な要素については後述します。 次のセクションの図には、操作中のこれらの要素が表示されます。  
  
### <a name="data-context"></a>データのコンテキスト 

 *データ コンテキスト* には、現在の Common Data Service 操作の一部として処理されるビジネス データが含まれます。 この処理は、ユーザー、ワークフロー、またはアプリケーションが、Dynamics 365 プラットフォームに対して特定の操作を実行するように要求したときに起動したものです。 データのコンテキストは、現在処理中の特定の要求およびエンティティの組合せで実行される、イベント パイプラインに登録されたプラグインまたはカスタム ワークフロー活動に渡されます。 データ コンテキストは、イベント実行パイプラインに沿って渡されるときは <xref:Microsoft.Xrm.Sdk.IPluginExecutionContext> の種類で、サービス ハブに投稿されるときは <xref:Microsoft.Xrm.Sdk.RemoteExecutionContext> です。  
  
 Azure Service Bus に投稿されるメッセージ内に含まれるデータ コンテキストは、既定の .NET バイナリ形式に加え、 XML または JSON 形式である場合があります。 これによりクロスプラットフォームの相互運用が可能となります。ここでは Azure がホストする非 .NET クライアントがサービス バスから Common Data Service データを読み取ることができます。 

> [!IMPORTANT]
> HTTP ペイロード全体のサイズが 192Kb を超えると、次のプロパティが削除されます:
>
> - <xref:Microsoft.Xrm.Sdk.RemoteExecutionContext.ParentContext>
> - <xref:Microsoft.Xrm.Sdk.RemoteExecutionContext.InputParameters>
> - <xref:Microsoft.Xrm.Sdk.RemoteExecutionContext.PreEntityImages>
> - <xref:Microsoft.Xrm.Sdk.RemoteExecutionContext.PostEntityImages>
>
> 一部の操作では、次のプロパティは含まれません。 
>
> - 追加データが削除された後にペイロードのサイズが 192kb を超える場合、追加の `MessageMaxSizeExceeded` プロパティは、システムが送信した [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) に追加されます。 これはデータの一部が切捨てられたことを示します。
> - 追加データが削除された後にペイロードのサイズが 192Kb を超える場合、エラーが発生し、メッセージは送信されません。
  
 前述のテクノロジーの詳細については、次を参照してください。
 - [イベント実行パイプライン](event-framework.md#event-execution-pipeline)
 - [ Microsoft Azure ソリューションに向けたリスナー アプリケーションを記述する](write-listener-application-azure-solution.md)  
  
### <a name="plug-ins"></a>プラグイン

プラグインは、Azure Service Bus へのデータ コンテキストを含むメッセージの投稿を開始するのに使用される 2 つのメソッドのうちの 1 つです。他のメソッドはユーザー定義のワークフロー活動です。 Common Data Service-Azure の接続機能が対応しているプラグインは2種類あります: アウトオブボックス (OOB) と カスタム です。 いずれの場合も、システムのベスト パフォーマンスのため、非同期で実行するようプラグインを登録することをお勧めします。  
  
Azure対応のOOBプラグインは Common Data Service に付属しており、プラグイン登録ツールにて登録することができます。 このプラグインは、 Common Data Service プラットフォームに対して完全信頼で実行されます。 イベント実行パイプラインでプラグイン「ステップ」を登録する必要があります。このステップでは、投稿の通知の実行および処理のためのプラグインをトリガーする、メッセージとエンティティの組合せを識別します。 実行するとき、プラグインは非同期サービスを通知し、サービス エンドポイント通知サービス (<xref:Microsoft.Xrm.Sdk.IServiceEndpointNotificationService>) を介し、現在の要求データ コンテキストを Azure Service Bus に投稿します。  
  
また、“Azure 対応“ の独自のカスタム プラグインを作成することもできます。 カスタム プラグインは、部分信頼でサンドボックス内で実行します。 カスタム プラグインは、サービス エンドポイントの通知を介し、サービス バスに対するデータ コンテキストの投稿を開始することができます。 このサービスを呼び出すコードを追加すると、プラグインは “Azure 対応“になります。 
 
プラブイン全般の詳細については、 [プラグインの記述](write-plug-in.md)を参照してください。 Azure 対応プラグインの詳細については、[Azure 対応のカスタム プラグインの記述](write-custom-azure-aware-plugin.md) を参照してください。  
  
### <a name="custom-workflow-activities"></a>ユーザー定義のワークフロー活動

プラグインと同様に、ユーザー定義のワークフロー活動を記述して、サービス エンドポイント通知サービスを使用し、Azure Service Bus に対する現在の要求メッセージ データの投稿を開始することができます。 詳細: [ワークフロー拡張](workflow/workflow-extensions.md) 
  
### <a name="asynchronous-service"></a>非同期サービス

サービス エンドポイント通知サービスにより通知されると、非同期サービスは、イベント実行パイプラインが現在処理している要求メッセージのデータ コンテキストの、Azure Service Bus に対する投稿を処理します。 各ポストは非同期サービスのシステム ジョブによって実行されます。 ユーザーは、PowerApps Web アプリケーションの**システム ジョブ**ビューを使用して、各システム ジョブのステータスを表示することができます。  
  
非同期サービスの詳細については、「[非同期サービス](asynchronous-service.md)」を参照してください。  
  
### <a name="microsoft-azure-service-bus"></a>Microsoft Azure サービス バス

サービスバスは Common Data Service とAzure サービス バス ソリューション リスナー アプリケーションの間で要求されたメッセージのデータ コンテキストを中継します。 またサービス バスは、投稿した Dynamics 365 データには承認済みのアプリケーションのみがアクセスできるよう、データ セキュリティを提供します。  データ コンテキストをサービス バスに登録する、およびリスナー アプリケーションがそれを読み込むために Common Data Service が行う認証は、Azure Shared Access Signatures(SAS)によって管理されています。  
  
  
 サービス バスの詳細については、[サービス バス](https://azure.microsoft.com/services/service-bus/) を参照してください。 サービス バス認証の詳細については、 [サービス バスの認証および承認](https://azure.microsoft.com/documentation/articles/service-bus-authentication-and-authorization/) を参照してください。  
  
### <a name="microsoft-azure-solution"></a>Microsoft Azure ソリューション

Common Data Service とAzureの接続が機能するためには、Azure Service Bus ソリューションのアカウントに少なくとも1つのソリューションが含まれている必要があり、そのソリューションには1つ以上のサービスエンドポイントが含まれてる必要があります。 リレー エンドポイント契約では、Common Data Service 対応のリスナー アプリケーションは、サービス バスでの Common Data Service の要求をエンドポイントでアクティブにリスニングする必要があります。 キュー エンドポイント契約では、リスナーはアクティブにリスニングする必要はありません。 リスナーは <xref:Microsoft.Xrm.Sdk> アセンブリにリンクすることで Common Data Serviceを認識できるようになり、 <xref:Microsoft.Xrm.Sdk.RemoteExecutionContext> の種別が定義されます。 詳細については次を参照ください: [ Microsoft Azure ソリューションに向けたリスナーを記述する](write-listener-application-azure-solution.md)  
  
Common Data Service は Azure イベント ハブ ソリューションへのエベントデータの送信に対応しています。 イベント ハブの詳細については、[Azure イベント ハブ ソリューションのイベント データとの連携](work-event-data-azure-event-hub-solution.md) を参照してください。  
  
<a name="bkmk_describing"></a>  
 
## <a name="common-data-service-to-service-bus-scenario"></a>Common Data Service からサービスバスへのシナリオ  

ここでは、これまでに説明した接続コンポーネントを実装するシナリオについて説明します。 前提として、SASは Common Data Service を対応する発行者として認識するよう設定がされており、 リスナーが存在するエンドポイントに Common Data Service が送信できるように、ルールが設定されたAzure Service Busソリューションが存在します。  
  
次の図は、シナリオを構成する物理要素を示しています。  
  
![Dynamics 365 Service Bus シナリオ](media/crm-v5s-az.png "Common Data Service Service Bus シナリオ")  
  
この図に示すイベントの順序は次のとおりです。  
  
1. リスナーアプリケーションはAzure Service Busソリューションエンドポイントに登録され、サービスバス上の Common Data Service リモート実行コンテキストのリスニング処理を開始します。  

2. ユーザーが Common Data Service で何らかの操作を行うと、登録済みのOOBプラグインまたはカスタマイズされたAzure対応プラグインが実行されます。 プラグインが、非同期サービス システム ジョブを介して、現在の要求データ コンテキストのサービス バスへのポストを開始します。  
3. Common Data Service によってポストされたクレームが認証されます。 次に、サービス バスが、リモート実行コンテキストをリスナーに渡します。 リスナーはコンテキスト情報を処理し、その情報に対してビジネス関連タスクを実行します。 サービス バスから非同期サービスにポストの成功が通知され、関連するシステム ジョブが完了ステータスに設定されます。  
  
<a name="bkmk_establising"></a>  

## <a name="establish-a-contract-between-common-data-service-and-an-azure-solution"></a>Common Data Service と Azure ソリューションの契約の確立

ソリューション エンドポイントごとに契約を構成して、サービス バスでのこれらのリモート実行コンテキストの "メッセージ" の処理と、そのエンドポイントで使用する必要があるセキュリティを定義します。 サービス バス メッセージは、ここに示す 1 件のサポート契約を使用してエンドポイントで受信されます。  
  
### <a name="queue"></a>キュー 

キュー契約は、クラウドでメッセージ キューを提供します。 キュー契約では、リスナーはエンドポイントでメッセージをアクティブにリスニングする必要はありません。 キューに対しては破壊読み取りと非破壊読み取りがあります。 破壊読み取りでは、キューにあるメッセージが読み取られ、メッセージが削除されます。 非破壊読み取りでは、メッセージがキューから削除されません。  
  
Common Data Service でサポートされる種類のキューは、永久キューと呼ばれます。 永久キューでは、コードで指定することができる、有効期間が長く有限のメッセージがあります。  
  
### <a name="one-way"></a>一方向

一方向契約ではアクティブなリスナーが必要です。 エンドポイントにアクティブなリスナーがないと、サービス バスへのポストが失敗します。 要求を投稿する非同期システム ジョブが最終的に中止され、そのステータスが "失敗" にセットされるまで、Common Data Service は指数関数的に長い期間、投稿を再試行します。  
  
### <a name="two-way"></a>二方向

双方向契約は一方向契約と似ていますが、リスナーからポストを開始したプラグインまたはユーザー定義ワークフロー活動に、文字列値が返される点で異なります。  
  
### <a name="rest"></a>停止

REST 契約は REST エンドポイントでの二方向契約に似ています。  
  
### <a name="topic"></a>トピック

一つ以上のリスナーがトピックをサブスクライブしてトピックからメッセージを受信することができること以外は、キューに似ています。  
  
### <a name="event-hub"></a> イベント ハブ

この契約の種類は Azure イベント ハブ ソリューションに適用されます。  
  
> [!IMPORTANT]
>  これらの契約を使用するには、[Azure SDK](http://www.windowsazure.com/develop/downloads/) v1.7 またはそれ以降を使用して、リスナー アプリケーションを記述する必要があります。  
  
契約の構成では、契約で使用されるセキュリティの種類を指定します。 契約は、Transport Layer Security (TLS) または Secure Sockets Layer (SSL) (https) を使用するトランスポート セキュリティを使用できます。  
  
クレーム認証は、サービス バスに対するセキュリティで保護されたアクセスのために使用されます。 サービス バスへの認証で使用されるクレームは、 Common Data Service 内で生成され、 Common Data Service 構成データベースに指定されている AppFabricIssuer 証明書によって署名されます。  
  
<a name="bkmk_management"></a>

## <a name="manage-run-time-errors"></a>ランタイム エラーの管理  

サービス バスへのポストが試行された後でエラーが発生した場合は、Web アプリケーションの関連するシステム ジョブのステータスを調べて、エラーの詳細を確認します。 サービス バスが停止しているか、リスナーまたはエンドポイントが使用できない場合、 Common Data Service で処理されている現在のメッセージはバスにポストされません。 非同期サービスはメッセージのポスト試行を継続しますが、最初は頻繁に試行されるものの、その後は試行間隔が急激に長くなります。 内部の Common Data Service エラーの場合、メッセージのポストは試行されません。 外部のサービス バスまたはネットワークのエラーの場合、関連するシステム ジョブは「待機」状態になります。