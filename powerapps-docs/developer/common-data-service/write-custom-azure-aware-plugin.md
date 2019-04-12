---
title: Azure 対応のカスタム プラグインの記述 (Common Data Service) | Microsoft Docs
description: サンプルでは、Azure サービス プロバイダーを取得し、IExecutionContext) を呼び出すことでサービス バスへの実行コンテキストのポストを開始するコードを追加する方法を示します。
keywords: ''
ms.date: 10/31/2018
ms.service:
  - powerapps
ms.custom:
  - ''
ms.topic: article
ms.assetid: 93d0442e-5fc9-c43c-c8c1-a433687f3d0a
author: brandonsimons
ms.author: jdaly
manager: ryjones
ms.reviewer: null
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---

# <a name="write-a-custom-azure-aware-plug-in"></a>Azure 対応のカスタム プラグインの記述

<!-- https://docs.microsoft.com/dynamics365/customer-engagement/developer/write-custom-azure-aware-plugin -->

Azure を操作するプラグインの記述は他のいずれかの Dynamics 365 Common Data Service プラグインの記述と似ています。 ただし、目的の Web サービス メソッドの呼び出しに加えて、プラグインには、実行コンテキストの Azure Service Bus へのポストを開始するコードを含める必要があります。  
  
<a name="bkmk_design"></a>

## <a name="plug-in-design-considerations"></a>プラグインの設計に関する考慮事項  
同期して実行するプラグインでは、リスナー アプリケーションなどの外部サービスから情報を取得するために Azure にメッセージを送信するようにプラグインを設計することをお勧めします。 データ文字列をプラグインに返すことができる Azure Service Bus エンドポイントでの二方向または REST 契約を使用します。  
  
同期プラグインで Azure Service Bus を使用して外部サービスのデータを更新することはお勧めしません。 外部サービスが利用できない場合や更新するデータが大量にある場合、問題が起こる可能性があります。 同期プラグインは、高速実行し、長時間の操作を実行する間はログインしている組織のすべてのユーザーを保持しないようにします。 また、プラグインが起動する現在のコア操作のロールバックが発生すると、プラグインで行われたデータの変更は取り消されます。 これにより、Dynamics 365 と外部のサービスが非同期状態になることがあります。  
  
同期登録されたプラグインで実行コンテキストを Azure Service Bus に投稿することが可能であることに注意してください。  
  
<a name="bkmk_writing"></a>
  
## <a name="write-the-plug-in-code"></a>プラグインのコードを記述する 
 
次のプラグイン例では、Azure サービス プロバイダーを取得し、<xref:Microsoft.Xrm.Sdk.IServiceEndpointNotificationService.Execute(Microsoft.Xrm.Sdk.EntityReference,Microsoft.Xrm.Sdk.IExecutionContext)> を呼び出すことでサービスへの実行コンテキストのポストを開始するコードが追加されています。 プラグインはサンドボックスで実行する必要があるため、プラグインのデバッグを容易にするトレース コードが追加されています。  

> [!NOTE]
> このコードでコンストラクターに渡された `serviceEndpointId` は、[チュートリアル: Common Data Service との統合のための Azure (SAS) の構成](walkthrough-configure-azure-sas-integration.md)で説明されたサービス エンドポイントの作成から取得したものです。
>
> ユーザーのブラウザーと *`[organization Uri]`*`/api/data/v9.0/serviceendpoints?$select=name,description,serviceendpointid` のようなクエリを使用する Web API に対して `GET` 要求を使用することにより、ユーザーの環境で使用可能なサービス エンドポイントをクエリすることができます。
  
```csharp
using System;
using System.Diagnostics;
using System.Threading;
using System.Runtime.Serialization;

using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Description;

using Microsoft.Xrm.Sdk;

namespace Microsoft.Crm.Sdk.Samples
{
    /// <summary>
    /// A custom plug-in that can post the execution context of the current message to the Windows
    /// Azure Service Bus. The plug-in also demonstrates tracing which assist with
    /// debugging for plug-ins that are registered in the sandbox.
    /// </summary>
    /// <remarks>This sample requires that a service endpoint be created first, and its ID passed
    /// to the plug-in constructor through the unsecure configuration parameter when the plug-in
    /// step is registered.</remarks>
    public sealed class SandboxPlugin : IPlugin
    {
        private Guid serviceEndpointId; 

        /// <summary>
        /// Constructor.
        /// </summary>
        public SandboxPlugin(string config)
        {
            if (String.IsNullOrEmpty(config) || !Guid.TryParse(config, out serviceEndpointId))
            {
                throw new InvalidPluginExecutionException("Service endpoint ID should be passed as config.");
            }
        }

        public void Execute(IServiceProvider serviceProvider)
        {
            // Retrieve the execution context.
            IPluginExecutionContext context = (IPluginExecutionContext)serviceProvider.GetService(typeof(IPluginExecutionContext));

            // Extract the tracing service.
            ITracingService tracingService = (ITracingService)serviceProvider.GetService(typeof(ITracingService));
            if (tracingService == null)
                throw new InvalidPluginExecutionException("Failed to retrieve the tracing service.");

            IServiceEndpointNotificationService cloudService = (IServiceEndpointNotificationService)serviceProvider.GetService(typeof(IServiceEndpointNotificationService));
            if (cloudService == null)
                throw new InvalidPluginExecutionException("Failed to retrieve the service bus service.");

            try
            {
                tracingService.Trace("Posting the execution context.");
                string response = cloudService.Execute(new EntityReference("serviceendpoint", serviceEndpointId), context);
                if (!String.IsNullOrEmpty(response))
                {
                    tracingService.Trace("Response = {0}", response);
                }
                tracingService.Trace("Done.");
            }
            catch (Exception e)
            {
                tracingService.Trace("Exception: {0}", e.ToString());
                throw;
            }
        }
    }
}
```  
  
プラグイン コードで、ポストを開始する前にコンテキストで書き込み可能データを更新できます。 たとえば、コンテキスト内の共有変数にキー/値のペアを追加できます。 
  
<a name="bkmk_registration"></a>

## <a name="plug-in-registration"></a>プラグイン登録

Azure 対応のカスタム プラグインの登録時には、いくつかの制限があります。 プラグインは、サンドボックスで実行するよう登録する必要があります。 このため、プラグインは、<xref:Microsoft.Xrm.Sdk.IOrganizationService> メソッド、Azure ソリューション メソッドの呼び出し、または Web クライアントを使用した Network へのアクセスに制限されます。 ローカル ファイル システムへのアクセスなど、他の外部アクセスは許可されません。  
  
非同期モードで実行するよう登録されたプラグインの場合、他の非同期プラグインとの比較でプラグイン実行の順序が保証されないことも意味します。 また、非同期プラグインは常に Dynamics 365 コア操作の後に実行されます。  
  
<a name="bkmk_failure"></a>
 
## <a name="handle-a-failed-service-bus-post"></a>サービス バス ポストの失敗の処理

失敗したサービス バス送信での所定の動作は、プラグインが同期実行と非同期実行のどちらで登録されているかによって異なります。 非同期プラグインでは、実際に実行コンテキストをサービス バスに投稿するシステム ジョブが投稿を再試行します。 同期に登録されたプラグインの場合、例外が返されます。 詳細 [ランタイム エラーの管理と通知](azure-integration.md)  
  
> [!IMPORTANT]
>  非同期として登録されたプラグインの場合のみ、Azure Service Bus に投稿された非同期ジョブが投稿失敗後に再試行されると、プラグイン ロジック全体が再び実行されます。 このため、コンテキストの変更とサービス バスへの投稿以外に、ユーザー定義の Azure 対応プラグインにほかのロジックを追加しないでください。  
  
非同期に実行するように登録されたプラグインの場合、サービス バス経由で送信されたメッセージの本文に含まれる <xref:Microsoft.Xrm.Sdk.RemoteExecutionContext> は <xref:Microsoft.Xrm.Sdk.RemoteExecutionContext.OperationId> のプロパティと <xref:Microsoft.Xrm.Sdk.RemoteExecutionContext.OperationCreatedOn> プロパティを含みます。 これらのプロパティは、関連するシステム ジョブ (`AsyncOperation`) の `AsyncOperationId` と `CreatedOn` 属性が作成したデータと同じデータが含まれます。 Azure Service Bus ポストを再試行する必要がある場合、このような追加のプロパティにより順序付けと重複データ検出が容易に行われます。  
  
### <a name="see-also"></a>関連項目

[Dynamics 365 の Azure 拡張機能](azure-integration.md)<br />
[Microsoft Azure サービス バスを介した Dynamics 365 データの送信](work-data-azure-solution.md)<br />
[プラグインの記述](write-plug-in.md)<br />
[イベント実行パイプライン](event-framework.md)<br />
[プラグインの登録および展開](register-plug-in.md)
