---
title: ログおよびトレース (アプリ用 Common Data Service) | Microsoft Docs
description: プラグインのデバッグを支援するために、トレース ログを使用してプラグイン実行情報を保存します。
ms.custom: ''
ms.date: 1/28/2019
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: JimDaly
ms.author: pehecke
manager: kvivek
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# トレースおよびログ

 プラグインまたはユーザー定義のワークフロー活動 (カスタム コード) をトラブルシューティングする代替の方法は、[!INCLUDE[pn_Visual_Studio](../../includes/pn-visual-studio.md)] のデバッグと比べると、トレースの使用です。 トレースは、コードの失敗の原因を診断する補助として、実行時のユーザー定義の情報を記録することによって、開発者を支援します。 トレースは、[!INCLUDE[pn_CRM_Online](../../includes/pn-crm-online.md)] に登録されているユーザー定義のコードをトラブルシューティングする場合に特に有効であり、このシナリオでサポートされている唯一のトラブルシューティングの方法です。 トレースは、サンドボックスで保護された (部分信頼)、また完全信頼で登録されたユーザー定義コードに対して、同期または非同期の実行時にサポートされます。 トレースは、[!INCLUDE[pn_microsoft_dynamics_crm_for_outlook](../../includes/pn-microsoft-dynamics-crm-for-outlook.md)] または他のモバイル クライアントで実行されるユーザー定義コードに対してはサポートされません。  
  
 [!INCLUDE[pn_dynamics_crm](../../includes/pn-dynamics-crm.md)] アプリの実行時のトレース情報の記録は、<xref:Microsoft.Xrm.Sdk.ITracingService> という名前のサービスによって提供されます。 ユーザー定義コードによってこのサービスに提供された情報は、次に示す 3 つの異なる場所に記録できます。  

> [!NOTE]
> `ITracingService` インターフェイスを使用するトレース ログは、プラグインがサンドボックス モードに登録されているときにのみ動作します。

- ****トレース ログ****  
  
     **PluginTraceLog** の種類のトレース ログ レコードは、**設定**に移動して、**プラグイン トレース ログ**タイルを選択することによって、Web アプリケーション内に見つけることができます。 このタイルは、割り当てられたセキュリティ ロールでトレース ログのエンティティ レコードにアクセスできる場合にのみ表示されます。 これらのレコードの作成は、次のセクションで説明されるトレースの設定によって制御されます。
  
    > [!NOTE]
    > トレース ログは、特に多数のトレースと例外が生成されたときは、組織の保存領域を占有します。 トレースログは、デバッグとトラブルシューティングの場合にのみオンにして、調査の完了後はオフにする必要があります。  
  
- ****エラー ダイアログ****  
  
     例外をプラットフォームに返す、非同期の登録済みのプラグインまたはユーザー定義のワークフロー活動の結果、ログオンしているユーザーに表示される Web アプリケーションに、エラー ダイアログ ボックスが表示されます。 ユーザーは、ダイアログにある**ログ ファイルのダウンロード**ボタンを選択して、例外とトレース出力を格納しているログを表示することができます。  
  
- ****システム ジョブ****  
  
     例外を返す、非同期の登録済みのプラグインまたはユーザー定義の活動の場合、トレース情報は、Web アプリケーションの**システム ジョブ**フォームの**詳細**領域に表示されます。  
  
<a name="bkmk_trace-settings"></a>   
## トレース ログの有効化  
 この機能をサポートする組織のトレース ログを有効にするには、Web アプリケーションで、**設定** > **管理** > **システムの設定**に移動します。 **カスタマイズ**タブで、**プラグイン トレース ログへのログ記録を有効化**という名前のドロップダウン メニューを見つけて、使用可能なオプションから 1 つを選択します。  
  
|オプション|内容|  
|------------|-----------------|  
|オフ​​|トレース ログへの書き込みは無効です。 **PluginTraceLog** レコードが作成されません。 ただし、ログが書き込まれていない場合でも、ユーザー定義コードはそれでも <xref:Microsoft.Xrm.Sdk.ITracingService.Trace(System.String,System.Object[])> メソッドを呼び出すことができます。|  
|例外|ユーザー定義コードから例外がプラットフォームに渡されると、トレース情報がログに書き込まれます。|  
|すべて|コードの完了時に、またはユーザー定義コードから例外がプラットフォームに渡されたときに、トレース情報がログに書き込まれます。|  
  
 トレース ログの設定が**例外**に設定されている場合、ユーザー定義コードが例外をプラットフォームに返したとき、トレース ログのレコードが作成され、トレース情報はもう一つの場所にも書き込まれます。 同期して実行されるユーザー定義コードの場合は、情報はエラー ダイアログ ボックスでユーザーに表示されます。それ以外の、非同期のコードの場合は、情報は関連するシステム ジョブに書き込まれます。  
  
 既定では、システム管理者およびシステム カスタマイザのロールには、トレース ログの設定を変更するために必要な特権が備わっています。トレース ログの設定は <xref:Microsoft.Xrm.Sdk.Deployment.TraceSettings> エンティティ レコードに格納されています。 トレース設定には組織のスコープがあります。  
  
## トレース サービスへの書き込み  
 トレース サービスに書き込む前に、最初に、渡された実行コンテキストからトレース サービス オブジェクトを取得する必要があります。 その後、ユーザー定義コードに、<xref:Microsoft.Xrm.Sdk.ITracingService.Trace(System.String,System.Object[])> 呼び出しを追加するだけす。このメソッドの呼び出しで関連する診断情報が渡されます。  

 サンプル [プラグインの操作](https://code.msdn.microsoft.com/Sample-Create-a-basic-plug-64d86ade) をダウンロードします。
  
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
     tracingService.Trace
         ("AdvancedPlugin: Getting the target entity from Input Parameters.");
     Entity entity = (Entity)context.InputParameters["Target"];

     // Obtain the image entity from the Pre Entity Images.
     tracingService.Trace
         ("AdvancedPlugin: Getting image entity from PreEntityImages.");
     Entity image = (Entity)context.PreEntityImages["Target"];
```

  
 次に、プラグインまたはユーザー定義ワークフロー活動を作成して展開します。 組織によってサポートされ、有効になっていて、前のセクションで説明したとおりに、Web ダイアログまたはシステム ジョブでユーザーにも利用できるようになっている場合、ユーザー定義コードの実行中に、**Trace** メソッドを呼び出しで提供された情報は、<xref:Microsoft.Xrm.Sdk.ITracingService> によってトレース ログのエンティティ レコードに書き込まれます。 トレース ログに書き込まれるトレース情報は、トレース設定で構成されます。 詳細については、[トレース ログを有効にする](#bkmk_trace-settings) を参照してください。  
  
> [!NOTE]
> ユーザー定義コードがデータベース トランザクション内で実行され、トランザクションのロールバックを引き起こす例外が発生した場合、コードによるすべてのエンティティ データの変更は取り消されます。 ただし、**PluginTraceLog** レコードは、ロールバックが完了しても残ります。  
  
## トレース サービスに関する追加情報

 <xref:Microsoft.Xrm.Sdk.ITracingService> は提供された情報を **Trace** メソッドを使用して 1 つにまとめます。 ユーザー定義コードの実行が正常に完了した後、または例外がスローされた後、情報は新しい **PluginTraceLog** レコードに書き込まれます。  
  
 PluginTraceLog レコードには有効期限があります。 一括削除ジョブがバックグラウンドで 1 日に 1 回実行されて、作成から 24 時間経過したレコードを削除します。 このジョブは必要に応じて無効にすることができます。 

## コミュニティ ツール

 ### プラグイン追跡ビューア

**プラグイン追跡ビューア**は [!INCLUDE[pn_dynamics_crm](../../includes/pn-dynamics-crm.md)] アプリ用に XrmToolbox コミュニティが開発したツールです。 コミュニティ開発ツールのトピック、[開発者ツール](developer-tools.md) を参照してください。

> [!NOTE]
> コミュニティ ツールは [!include[pn_microsoft_dynamics](../../includes/pn-microsoft-dynamics.md)] アプリの製品ではなく、コミュニティ ツールに対するサポートは提供しません。 このツールに関するご質問は、その発行元にお問い合わせください。 詳細: [XrmToolBox](https://www.xrmtoolbox.com)。  

### 関連項目

[[プラグイン](plug-ins.md)](plug-ins.md)  
[[プラグインのデバッグ](debug-plug-in.md#use-tracing)](debug-plug-in.md#use-tracing)  
[[トレース ログの表示](tutorial-write-plug-in.md#view-trace-logs)](tutorial-write-plug-in.md#view-trace-logs)  
[[トレース サービスの使用](write-plug-in.md#use-the-tracing-service)](write-plug-in.md#use-the-tracing-service)  
[[PluginTraceLog エンティティ](reference/entities/plugintracelog.md)](reference/entities/plugintracelog.md)