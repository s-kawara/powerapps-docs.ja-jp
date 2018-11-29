---
title: 'チュートリアル: プラグインの作成と登録 (アプリ用 Common Data Service) | Microsoft Docs'
description: このチュートリアルでは、プラグインの使用方法を説明するシリーズの最初のチュートリアルです。
ms.custom: ''
ms.date: 10/31/2018
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
# <a name="tutorial-write-and-register-a-plug-in"></a>チュートリアル: プラグインを書き込み登録する

このチュートリアルは、プラグインの使用方法を説明するシリーズの最初のチュートリアルです。このチュートリアルは、以下のチュートリアルの前提条件です。

- [チュートリアル: プラグインをデバッグする](tutorial-debug-plug-in.md)
- [チュートリアル: プラグインを更新する](tutorial-update-plug-in.md)

関連する概念と技術的詳細については、以下を参照してください。

- [ビジネス プロセスを拡張するためのプラグインの使用](plug-ins.md)
- [プラグインを記述する](write-plug-in.md)
- [プラグインの登録](register-plug-in.md)
- [プラグインのデバッグ](debug-plug-in.md)

## <a name="goal"></a>目標

取引先企業エンティティの作成メッセージで登録された非同期プラグインを作成します。 プラグインは、取引先企業の作成者に 1 週間後のフォローアップを通知するタスク活動を作成します。

> [!NOTE]
> この目標は、コードを記述せずにワークフローを使用して簡単に達成できます。 プラグインの作成および展開に集中できるように、この単純な例を使用します。

## <a name="prerequisites"></a>前提条件

- アプリ用 Common Data Service 環境の管理者レベルのアクセス
- 取引先企業およびタスク エンティティを含むモデル駆動型のアプリケーション。
    - これらを含むモデル駆動型アプリケーションがない場合は、[モデル駆動型アプリケーションを最初から作成する](../../maker/model-driven-apps/build-first-model-driven-app.md)を参照して、わずか数分で作成する手順を参照してください。
- Visual Studio 2017
- Visual C# プログラミング言語の知識
- プラグイン登録ツールをダウンロードします。
    - プラグイン登録ツールのダウンロードについては、[NuGet からツールをダウンロード](download-tools-nuget.md)を参照してください。 そのトピックには、最新の NuGet ツールをダウンロードするために PowerShell スクリプトを使用するための手順が含まれます。

## <a name="create-a-plug-in-project"></a>プラグイン プロジェクトの作成

プラグインを作成するには Visual Studio を使用する必要があります。 基本的なプラグインを作成する手順に従います。

### <a name="create-a-visual-studio-project-for-the-plug-in"></a>プラグイン用の Visual Studio プロジェクトの作成

1. Visual Studio 2017 を開き、**.NET Framework 4.5.2** を使用して新しい**クラス ライブラリ (.NET Framework)** を開きます。

    ![.NET Framework 4.5.2 を使用して新しいクラス ライブラリ (.NET Framework) を開く](media/tutorial-write-plug-in-create-visual-studio-project.png)

    プロジェクトで使用した名前は、アセンブリの名前になります。 このチュートリアルでは `BasicPlugin` という名前を使用します。
1. **ソリューション エクスプローラー**で、プロジェクトを右クリックしてコンテキスト メニューから **NuGet Packages の管理...**  を選択します。

    ![NuGet パッケージの管理](media/tutorial-write-plug-in-manage-nuget-packages.png)

1. **参照** を選択して、`Microsoft.CrmSdk.CoreAssemblies` を検索し、最新バージョンをインストールします。

    ![Microsoft.CrmSdk.CoreAssemblies NuGet パッケージのインストール](media/tutorial-write-plug-in-install-microsoft.crmsdk.coreassemblies.png)

1. **ライセンスの承認** ダイアログで **同意する** を選択する必要があります。
1. **ソリューション エクスプローラー**で、`Class1.cs` ファイルを右クリックし、コンテキスト メニューで **名前の変更** を選択します。

    ![クラスの名前変更](media/tutorial-write-plug-in-rename-class.png)

1. `Class1.cs` ファイルの名前を `FollowupPlugin.cs` に変更します。
1. プロンプトが表示されたら、Visual Studio はクラスの名前をファイル名と同じ名前に変更できるようにします。

    ![名前の変更の確認ダイアログ](media/tutorial-write-plug-in-rename-class-confirm.png)

### <a name="edit-the-class-file-to-enable-a-plug-in"></a>プラグインを有効にするためにクラス ファイルを編集する

1. 以下の `using` ステートメントを `FollowupPlugin.cs` ファイルの上部に追加します。

    ```csharp
    using System.ServiceModel;  
    using Microsoft.Xrm.Sdk;
    ```

1. クラスを編集することで、<xref:Microsoft.Xrm.Sdk.IPlugin> インターフェイスを実装します。

    > [!NOTE]
    > クラス名の後「`: IPlugin`」と入力するだけの場合、Visual Studio により **Execute** メソッドのスタブの実装が自動推奨されます。

    ```csharp
    public class FollowupPlugin : IPlugin
    {
        public void Execute(IServiceProvider serviceProvider)
        {
            throw new NotImplementedException();
        }
    }
    ```


1. `Execute` メソッドの内容を次のコードに置き換えます。


```csharp
// Obtain the tracing service
ITracingService tracingService =
(ITracingService)serviceProvider.GetService(typeof(ITracingService));

// Obtain the execution context from the service provider.  
IPluginExecutionContext context = (IPluginExecutionContext)
    serviceProvider.GetService(typeof(IPluginExecutionContext));

// The InputParameters collection contains all the data passed in the message request.  
if (context.InputParameters.Contains("Target") &&
    context.InputParameters["Target"] is Entity)
{
    // Obtain the target entity from the input parameters.  
    Entity entity = (Entity)context.InputParameters["Target"];

    // Obtain the organization service reference which you will need for  
    // web service calls.  
    IOrganizationServiceFactory serviceFactory =
        (IOrganizationServiceFactory)serviceProvider.GetService(typeof(IOrganizationServiceFactory));
    IOrganizationService service = serviceFactory.CreateOrganizationService(context.UserId);

    try
    {
        // Plug-in business logic goes here.  
    }

    catch (FaultException<OrganizationServiceFault> ex)
    {
        throw new InvalidPluginExecutionException("An error occurred in FollowUpPlugin.", ex);
    }

    catch (Exception ex)
    {
        tracingService.Trace("FollowUpPlugin: {0}", ex.ToString());
        throw;
    }
}
```

### <a name="about-the-code"></a>コードについて

- <xref:Microsoft.Xrm.Sdk.ITracingService> により、トレース ログへの書き込みが可能になります。  最終キャッチ ブロックで例を確認できます。 詳細: [トレースの使用](debug-plug-in.md#use-tracing)
- <xref:Microsoft.Xrm.Sdk.IPluginExecutionContext> は、プラグインを実行したイベントのコンテキストへのアクセスを提供します。  詳細: [実行コンテキスト](write-plug-in.md#execution-context).
- コードは、コンテキスト <xref:Microsoft.Xrm.Sdk.IExecutionContext.InputParameters> に、このプラグインが登録される <xref:Microsoft.Xrm.Sdk.Messages.CreateRequest> の必要なパラメーターが含まれていることを確認します。 <xref:Microsoft.Xrm.Sdk.Messages.CreateRequest.Target> プロパティが存在する場合、要求に渡された <xref:Microsoft.Xrm.Sdk.Entity> が使用可能になります。
- <xref:Microsoft.Xrm.Sdk.IOrganizationServiceFactory> インターフェイスは、サービスを操作してタスクを作成するために使用するメソッドを提供する <xref:Microsoft.Xrm.Sdk.IOrganizationService> インターフェイスを実装するサービス変数へのアクセスを提供します。


## <a name="add-business-logic"></a>ビジネス ロジックの追加

プラグインは、取引先企業の作成者に 1 週間後のフォローアップを通知するタスク活動を作成します。

try ブロックに次のコードを追加します。 コメント `// Plug-in business logic goes here` を置き換えます。 次の内容に置き換えます。


```csharp
// Create a task activity to follow up with the account customer in 7 days. 
Entity followup = new Entity("task");

followup["subject"] = "Send e-mail to the new customer.";
followup["description"] =
    "Follow up with the customer. Check if there are any new issues that need resolution.";
followup["scheduledstart"] = DateTime.Now.AddDays(7);
followup["scheduledend"] = DateTime.Now.AddDays(7);
followup["category"] = context.PrimaryEntityName;

// Refer to the account in the task activity.
if (context.OutputParameters.Contains("id"))
{
    Guid regardingobjectid = new Guid(context.OutputParameters["id"].ToString());
    string regardingobjectidType = "account";

    followup["regardingobjectid"] =
    new EntityReference(regardingobjectidType, regardingobjectid);
}

// Create the task in Microsoft Dynamics CRM.
tracingService.Trace("FollowupPlugin: Creating the task activity.");
service.Create(followup);
```

### <a name="about-the-code"></a>コードについて

- このコードは、タスクを作成し、作成された取引先企業に関連付けるために、遅延バインドのフォームを使用します。 詳細: [組織サービスを使用したエンティティの作成](org-service/entity-operations-create.md)
- 事前バインド クラスを使用できますが、エンティティのクラスを生成し、アセンブリ プロジェクトと共にそれらのクラスを定義するファイルが含まれている必要があります。 これは、大部分は個人用設定であるので、簡略化するため、これらの手順はこのチュートリアルでは除外されています。 詳細: [組織サービスを使用した遅延バインドと事前バインド プログラミングのクラス](org-service/early-bound-programming.md)
- 作成される取引先企業の <xref:Microsoft.Xrm.Sdk.Entity.Id> は、コンテキスト <xref:Microsoft.Xrm.Sdk.IExecutionContext.OutputParameters> にあり、タスクの `regardingobjectid` 検索属性として設定されます。

## <a name="build-plug-in"></a>プラグインの作成

Visual Studio では、アセンブリを構築するために **F6** キーを押します。 エラーなしでコンパイルされることを確認します。

## <a name="sign-plug-in"></a>プラグインの署名

1. **ソリューション エクスプローラー**で、**BasicPlugin** プロジェクトを右クリックし、コンテキスト メニューで **プロパティ** を選択します。

    ![プロジェクト プロパティを開く](media/tutorial-write-plug-in-project-properties.png)

1. プロジェクト プロパティで、**署名** タブを選択し、**アセンブリに署名する** チェック ボックスを選択します。

    ![アセンブリにサインする](media/tutorial-write-plug-in-sign-assembly.png)

1. **厳密な名前のキーファイルを選択** ドロップダウンで、**<新規…>** を選択します。 
1. **厳密な名前キーを作成** ダイアログで、**キー ファイル名**を入力し、**パスワードでキー ファイルを保護する** チェック ボックスを選択解除します。
1. **OK** をクリックして **厳密な名前キーの作成** ダイアログを閉じます。
1. プロジェクトのプロパティの **ビルド** タブで、**構成** が **デバッグ** に設定されていることを確認します。
1. プラグインを再構築するために **F6** を押します。
1. エクスプローラーを使用して、作成されたプラグインを ` \bin\Debug\BasicPlugin.dll` で検索します。

> [!NOTE]
> 以降のチュートリアルではプラグイン プロファイラーを使用してデバッグするため、**デバッグ**構成を使用してアセンブリをビルドします。   ソリューションと共にプラグインを含めるには、リリース構成を使用してクエリを構築する必要があります。

## <a name="register-plug-in"></a>プラグインの登録

プラグインを登録するには、プラグイン登録ツールが必要

[!INCLUDE [cc-connect-plugin-registration-tool](includes/cc-connect-plugin-registration-tool.md)]

### <a name="register-your-assembly"></a>アセンブリの登録

1. **登録** ドロップダウン リストで **新しいアセンブリ** を選択します。

    ![新しいアセンブリの登録](media/tutorial-write-plug-in-register-new-assembly.png)

1. **新しいアセンブリの登録** ダイアログで、省略記号 (**…**) ボタンを選択し、前の手順で作成したアセンブリを参照します。

    ![[新しいアセンブリの登録] ダイアログ](media/tutorial-write-plug-in-register-new-assembly-dialog.png)

1. **分離モード** が **サンドボックス** であり、アセンブリを格納する **場所** が **データベース** であることを確認します。

    > [!NOTE]
    > **分離モード** および **場所** のそのほかのオプションは、設置型 Dynamics 365 展開に適用されます。

1. **選択したプラグインの登録** をクリックします。
1. **登録プラグイン** 確認ダイアログが表示されます。

    ![登録済みプラグインの確認ダイアログ](media/tutorial-write-plug-in-register-new-assembly-dialog-confirm.png)

1. **OK** をクリックしてダイアログを閉じ、**新しいアセンブリの登録** ダイアログを閉じます。 
1. **(アセンブリ) BasicPlugin** アセンブリが表示されるようになりました。展開すると、**(プラグイン) BasicPlugin.FollowUpPlugin** プラグインが表示されます。

    ![(プラグん) BasicPlugin.FollowUpPlugin プラグイン。](media/tutorial-write-plug-in-basic-followupplugin-plugin.png)


### <a name="register-a-new-step"></a>新しい手順の登録

1. **(プラグイン) BasicPlugin.FollowUpPlugin** を右クリックし、**新しいステップの登録** を選択します。

    ![新しい手順の登録](media/tutorial-write-plug-in-register-new-step.png)

1. **新しい手順の登録** ダイアログで、以下のフィールドを設定します。

    |設定|Value|
    |--|--|
    |メッセージ|作成|
    |主エンティティ|取引先企業|
    |実行のイベント パイプライン ステージ|PostOperation|
    |実行モード|非同期|

    ![新しい手順の登録](media/tutorial-write-plug-in-register-new-step-dialog.png)

1. **新しいステップの登録** をクリックして登録を完了し、**新しいステップの登録** ダイアログを閉じます。
1. 登録されている手順を表示できます。

    ![登録された手順の表示](media/tutorial-write-plug-in-view-registered-step.png)

> [!NOTE]
> この時点で、アセンブリや手順はシステムの**既定のソリューション**の一部です。 この時点で、配布するアンマネージド ソリューションに追加することをお勧めします。 これらのステップは、このチュートリアルには含まれていません。 詳細については、[ソリューションへのアセンブリの追加](register-plug-in.md#add-your-assembly-to-a-solution)と[ソリューションへのステップの追加](register-plug-in.md#add-step-to-solution)を参照してください。

## <a name="test-plug-in"></a>プラグインのテスト

1. モデル駆動型アプリケーションを開き、アカウント エンティティを作成します。
1. すぐに、取引先企業を開き、タスクの作成を確認します。

    ![プラグインによる関連タスク活動を持つ取引先企業エンティティ レコードの作成](media/tutorial-write-plug-in-test-plugin-in-model-app.png)

### <a name="what-if-the-task-wasnt-created"></a>タスクが作成されなかった場合はどうなりますか

これは非同期プラグインであるため、タスクを作成する操作は、取引先企業が作成された後に行われます。 通常、これはすぐに行われますが、行われない場合でも、適用されるのを待っているキューでシステム ジョブを表示できます。 このステップ登録では、ベスト プラクティスの **Delete AsyncOperation if StatusCode = Successful** オプションを使用しました。 これは、システム ジョブが正常に完了するとすぐに、**Delete AsyncOperation if StatusCode = Successful** オプションを選択解除してプラグインを再登録しない限り、システム ジョブ データを表示できなくなることを意味します。

ただし、エラーが発生した場合、エラー メッセージを表示するためにシステム ジョブを表示できます。

## <a name="view-system-jobs"></a>システム ジョブの表示

**Dynamics 365 --カスタム** アプリを使用してシステム ジョブを表示できます。

1. モデル駆動型のアプリケーションで、 

    ![dynamics 365 カスタム アプリの表示](media/dynamics-365-custom-app.png)

1. **Dynamics 365 --カスタム** アプリで、**設定** > **システム** > **システム ジョブ** に移動します。

    ![システム ジョブに移動](media/navigate-system-jobs.png)

1. システム ジョブを表示すると、**エンティティ** でフィルター処理できます。 **取引先企業** を選択します。

    ![foo](media/system-jobs-filter-entity-account.png)

1. ジョブが失敗した場合、**BasicPlugin.FollowupPlugin: アカウントの作成** という名前のレコードが表示されます。

    ![失敗したシステム ジョブ](media/failed-system-job.png)

1. システム ジョブを開いた場合、トレースに書き込まれた情報とエラーについての詳細を表示するために **詳細** セクションを展開できます。

    ![システム ジョブの詳細](media/system-job-failed-plug-in.png)

### <a name="query-system-jobs"></a>システム ジョブの照会

非同期プラグイン失敗したシステム ジョブを返すには、以下の Web API クエリを使用できます

```
GET <your org uri>/api/data/v9.0/asyncoperations?$filter=operationtype eq 1 and statuscode eq 31&$select=name,message
```
詳細: [Web API を使用するクエリ データ](webapi/query-data-web-api.md)


または、次の FetchXml を使用します。

```xml
<fetch top='50' >
  <entity name='asyncoperation' >
    <attribute name='message' />
    <attribute name='name' />
    <filter type='and' >
      <condition attribute='operationtype' operator='eq' value='1' />
      <condition attribute='statuscode' operator='eq' value='31' />
    </filter>
  </entity>
</fetch>
```
詳細: [FetchXML と FetchExpression の使用](org-service/entity-operations-query-data.md)


## <a name="view-trace-logs"></a>トレース ログの表示

サンプル コードは、トレース ログにメッセージを書きました。 以下のステップは、ログを表示する方法について説明します。

既定では、プラグイン トレース ログは無効です。 

> [!TIP]
> コードでこの設定を変更する場合: この設定は、[組織エンティティの PluginTraceLogSetting 属性](reference/entities/organization.md#BKMK_PluginTraceLogSetting)にあります。
> 
> 有効な値:
> 
> |Value|ラベル|
> |--|--|
> |0|オフ|
> |1|Exception|
> |2|すべて|

モデル駆動型アプリケーションで有効にするには、次の手順を実行します。

1. Dynamics 365 - カスタム アプリを開きます。

    ![Dynamics 365 - カスタム アプリを開く](media/tutorial-write-plug-in-open-dynamics365-custom-app.png)

1. **設定** > **システム** > **管理** の順に移動します。

    ![管理に移動](media/tutorial-write-plug-in-navigate-administration.png)

1. **管理** で **システム設定** を選択します。
1. **システム設定** ダイアログの [カスタマイズ] タブで、**プラグイン トレース ログへのログ記録を有効にする** を **すべて** に設定します。

    ![[システム設定] の [カスタマイズ] タブ](media/tutorial-write-plug-in-system-settings-customization-tab.png)

    > [!NOTE]
    > プラグインのテストを終了したらログ記録を無効にする必要があります。または、少なくとも **すべて** ではなく **例外** に設定します。

1. **OK** をクリックして**システムの設定**ダイアログを閉じます。
1. 新しい取引先企業を作成することで、プラグインをテストするための手順を繰り返します。
1. **Dynamics 365 -- カスタム アプリケーション** で、**設定** > **カスタマイズ** > **プラグイン トレース ログ** の順に移動します。
1. 新しいプラグイン トレース ログ レコードが作成されたことがわかります。

    ![プラグイン トレース ログ レコード](media/tutorial-write-plug-in-plug-in-trace-log.png)

1. レコードを開いた場合、トレースで設定した情報が含まれていることが期待されるかもしれませんが、含まれていません。 トレースが発生されたことのみ確認されます。
1. 詳細を表示するには、<xref href="Microsoft.Dynamics.CRM.plugintracelog?text=plugintracelog EntityType" /> と共に以下のクエリを使用し、`typename` プロパティを使用してプラグイン クラスの名前に基づいて `messageblock` プロパティで結果をフィルター処理し、ブラウザーで Web API を使用してこのデータを照会した方が簡単です。

    `GET <your org uri>/api/data/v9.0/plugintracelogs?$select=messageblock&$filter=typename eq 'BasicPlugin.FollowUpPlugin'`

1. Web API クエリで返される以下の内容が表示されることを期待できます。

    ```json
    {
        "@odata.context": "<your org uri>/api/data/v9.0/$metadata#plugintracelogs(messageblock)",
        "value": [{
            "messageblock": "FollowupPlugin: Creating the task activity.",
            "plugintracelogid": "f0c221d1-7f84-4f89-acdb-bbf8f7ce9f6c"
        }]
    }
    ```

## <a name="next-steps"></a>次のステップ

このチュートリアルでは、単純なプラグインを作成して登録しました。 このプラグインをデバッグする手順について知るには、[チュートリアル: プラグインのデバッグ](tutorial-debug-plug-in.md)を実行します。