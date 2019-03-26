---
title: プラグインで ITracingService を使用する | MicrosoftDocs
description: プラグインの問題や動作のデバッグやトラブルシューティングは、豊富で洞察に満ちたログやトレースがなければ複雑となります。
services: ''
suite: powerapps
documentationcenter: na
author: jowells
manager: austinj
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/12/2018
ms.author: jowells
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="use-itracingservice-in-plug-ins"></a>プラグインで ITracingService を使用する

**カテゴリ**: 保守性、サポート

**影響の可能性**: 中程度

<a name='symptoms'></a>

## <a name="symptoms"></a>現象

プラグインの問題や動作のデバッグやトラブルシューティングは、豊富で洞察に満ちたログやトレースがなければ複雑となります。

<a name='guidance'></a>

## <a name="guidance"></a>ガイダンス

<xref:Microsoft.Xrm.Sdk.ITracingService> インタフェースは、コードの失敗やプラグインの予期しない動作の原因を診断するために、ランタイム カスタム情報を記録することで開発者を支援します。 トレース サービスに書き込む前に、まず渡された実行コンテキストからトレース サービス オブジェクトを抽出する必要があります。 その後、[トレース](/dotnet/api/microsoft.xrm.sdk.itracingservice.trace) 呼び出しをカスタム コードに追加するだけです。適切な場合は、そのメソッド呼び出しに関連する診断情報を渡します。

> [!NOTE]
> `ITracingService` インターフェースを使用したトレース ロギングは、プラグインがサンドボックス モードで登録されている場合にのみ機能します。ランタイム データを取得するにはトレース ロギングを有効にする必要があります。 詳細については、[ロギングとトレース](/dynamics365/customer-engagement/developer/debug-plugin#logging-and-tracing) を参照してください。

```csharp
//Extract the tracing service for use in debugging sandboxed plug-ins.
ITracingService tracingService =
    (ITracingService)serviceProvider.GetService(typeof(ITracingService));

// Obtain the execution context from the service provider.
IPluginExecutionContext context = (IPluginExecutionContext)
    serviceProvider.GetService(typeof(IPluginExecutionContext));

// For this sample, execute the plug-in code only while the client is online. 
tracingService.Trace("AdvancedPlugin: Verifying the client is not offline.");
if (context.IsExecutingOffline || context.IsOfflinePlayback)
    return;

// The InputParameters collection contains all the data passed 
// in the message request.
if (context.InputParameters.Contains("Target") &&
    context.InputParameters["Target"] is Entity)
{
    // Obtain the target entity from the Input Parameters.
    tracingService.Trace("AdvancedPlugin: Getting the target entity from Input Parameters.");
    Entity entity = (Entity)context.InputParameters["Target"];

    // Obtain the image entity from the Pre Entity Images.
    tracingService.Trace("AdvancedPlugin: Getting image entity from PreEntityImages.");
    Entity image = (Entity)context.PreEntityImages["Target"];
}
```

<a name='additional'></a>

## <a name="additional-information"></a>追加情報

登録されたカスタム コードはそのシナリオでサポートされている唯一のトラブルシューティング方法であるため、トレースは登録されたカスタム コードのトラブルシューティングに特に役立ちます。 トレースは、サンドボックスで保護された `sandboxed` (部分信頼)、また完全信頼で登録されたユーザー定義コードに対して、同期または非同期の実行時にサポートされます。 トレースは、Microsoft Dynamics 365 for Outlook または他のモバイル クライアントで実行されるユーザー定義コードに対してはサポートされません。

<a name='seealso'></a>

### <a name="see-also"></a>関連項目

[プラグインを記述する](../../write-plug-in.md)  
[トレースおよびログ](../../logging-tracing.md)