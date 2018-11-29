---
title: プラグインを記述する (アプリ用 Common Data Service) | Microsoft Docs
description: プラグインを記述する場合に必要な概念と技術的詳細について説明します。
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
# <a name="write-a-plug-in"></a>プラグインを記述する

書き込み、登録、およびプラグインをデバッグするプロセスは次のとおりです:

1. **Visual Studio に .NET Framework クラス ライブラリ プロジェクトを作成します。**
1. **`Microsoft.CrmSdk.CoreAssemblies` NuGet パッケージをプロジェクトに追加します。**
1. **ステップとして登録されるクラスの <xref:Microsoft.Xrm.Sdk.IPlugin> インターフェイスを実装します。**
1. **インターフェイスに必要な <xref:Microsoft.Xrm.Sdk.IPlugin.Execute*> メソッドにコードを追加する**
    1. **必要なサービスへの参照を取得する**
    1. **ビジネス ロジックの追加**
1. **アセンブリにサインし、ビルドする**
1. アセンブリをテストする
    1. テスト環境でアセンブリを登録する
    1. アンマネージド ソリューションに、登録されたアセンブリとステップを追加する
    1. アセンブリの動作をテストする
    1. 想定されたトレース ログが書き込まれたことを確認する
    1. 必要に応じてアセンブリをデバッグする

このトピックの内容は上記**太字**のステップについて説明し、次のチュートリアルをサポートしています。

- [チュートリアル: プラグインを書き込み登録する](tutorial-write-plug-in.md)
- [チュートリアル: プラグインをデバッグする](tutorial-debug-plug-in.md)
- [チュートリアル: プラグインを更新する](tutorial-update-plug-in.md)

## <a name="assembly-constraints"></a>アセンブリの制約

作成時には、アセンブリの次の制約に留意してください。

### <a name="optimize-assembly-development"></a>アセンブリ開発を最適化する

アセンブリには複数のプラグイン クラス (または種類) を含める必要があるが、16 MB 程度にすることができます。 サイズを 16 MB 未満にする限り、プラグインとワークフロー アセンブリを単一のアセンブリに統合することをお勧めします。 詳細: [アセンブリ開発を最適化する](/dynamics365/customer-engagement/guidance/server/optimize-assembly-development)

### <a name="assemblies-must-be-signed"></a>アセンブリには署名が必要である

すべてのアセンブリは登録できるようにするには、サインインする必要があります。 これは、プロジェクトの Visual Studio 署名タブを使用するか、または [Sn.exe (Strong Name ツール) ](/dotnet/framework/tools/sn-exe-strong-name-tool) を使用して実行できます。

### <a name="do-not-depend-on-net-assemblies-that-interact-with-low-level-windows-apis"></a>下位の Windows API と対話する .NET アセンブリに依存していでください

プラグインには、それぞれの dll 内にすべての必要なロジックが含まれている必要があります。  プラグインはいくつかのコア .Net アセンブリを参照する場合があります。 とはいえ、グラフィックス デザイン インターフェイスなどの下位の Windows API とやり取りする .Net アセンブリへの依存関係はサポートされていません。

## <a name="iplugin-interface"></a>IPlugin インターフェイス

プラグインは、Visual Studio の .NET Framework 4.5.2 を使用し、.NET Framework クラス ライブラリ プロジェクトを使用して作成されたアセンブリ内のクラスです。 ステップとして登録されるプロジェクトの各クラスは、<xref:Microsoft.Xrm.Sdk.IPlugin> メソッドが必要な <xref:Microsoft.Xrm.Sdk.IPlugin.Execute*> インターフェイスを実装する必要があります。

> [!IMPORTANT]
> `IPlugin` の実装時には、クラスは*ステートレス*である必要があります。 これは、プラットフォームがクラス インスタンスをキャッシュし、パフォーマンス上の理由から再利用するためです。 これについて考える簡単な方法は、クラスにプロパティまたはメソッドを追加するべきではなく、すべてのものは `Execute` メソッド内に含める必要があるということです。 これには、いくつかの例外があります。 たとえば、定数を表すプロパティを持つことができる場合には、`Execute` メソッドから呼び出される関数を表すメソッドを持つことができます。 重要なことは、クラスのプロパティとして、サービス インスタンスやコンテキスト データを格納しないことです。 これらはそれぞれの呼び出しで変わり、そのデータがキャッシュされたり、それ以降の呼び出しに適用されないようにします。  詳細: [IPlugin の実装をステートレスとして開発する](/dynamics365/customer-engagement/guidance/server/develop-iplugin-implementations-stateless)

<xref:Microsoft.Xrm.Sdk.IPlugin.Execute*> メソッドは、単一の <xref:System.IServiceProvider>パラメーターを受け取ります。 `IServiceProvider` には、単一のメソッド: <xref:System.IServiceProvider.GetService*> があります。 コードで使用可能な複数の異なる種類のサービスを取得するには、このメソッドを使用します。 詳細: [コードで使用可能なサービス](#services-you-can-use-in-your-code)

## <a name="pass-configuration-data-to-your-plug-in"></a>プラグインへの構成データの引き渡し

プラグインを登録するとき、構成データを渡す機能があります。 構成データによって、登録されたプラグインの特定のインスタンスがどのように実行されるかを定義できます。 この情報は、クラスのコンストラクターのパラメーターに文字列データとして渡されます。 2 つのパラメーター: `unsecure` と `secure` があります。
最初の `unsecure` パラメーターはユーザーに表示できでも構わないデータに使用します。 機密データには 2 番目の `secure` パラメーターを使用します。 

次のコードは、`SamplePlugin` という名前のプラグイン クラスに対する可能な 3 つの署名を示しています。

```csharp
public SamplePlugin()  
public SamplePlugin(string unsecure)  
public SamplePlugin(string unsecure, string secure)
```
セキュリティで保護された構成データは、システム管理者のみが読み取り特権がある別のエンティティに格納されます。 詳細: [構成データの設定](register-plug-in.md#set-configuration-data)

## <a name="services-you-can-use-in-your-code"></a>コードで使用可能なサービス

プラグイン内で必要な事柄:
 
- プラグインが処理するために登録された場合、発生する事柄に関するコンテキスト情報にアクセスします。 これは*実行コンテキスト*と呼ばれます。
- データをクエリするためのコードの記述、エンティティ レコードに関する作業、操作を行うためのメッセージの使用を行えるように組織の Web サービスにアクセスします。
- コードをどのように実行しているかを評価できるように、メッセージをトレース サービス に記述します。

<xref:System.IServiceProvider>.<xref:System.IServiceProvider.GetService*> メソッドは、必要に応じてこれらのサービスにアクセスする方法を提供します。 サービスのインスタンスを取得するには、サービスの種類を渡す `GetService` メソッドを呼び出します。

> [!NOTE]
> Azure Service Bus 統合を使用してプラグインを記述する場合、<xref:Microsoft.Xrm.Sdk.IServiceEndpointNotificationService> インターフェイスを実装する通知サービスを使用しますが、これはここでは説明されません。 詳細: [Azure 統合](azure-integration.md)

## <a name="execution-context"></a>実行コンテキスト

次のコードを使用して、<xref:Microsoft.Xrm.Sdk.IPluginExecutionContext> インターフェイスを実装する変数を取得できます。

```csharp
// Obtain the execution context from the service provider.  
IPluginExecutionContext context = (IPluginExecutionContext)
    serviceProvider.GetService(typeof(IPluginExecutionContext));
```

この <xref:Microsoft.Xrm.Sdk.IPluginExecutionContext> は、プラグインが登録されている <xref:Microsoft.Xrm.Sdk.IPluginExecutionContext.Stage> に関する情報と、現在の操作をトリガーさせた別のプラグイン内の操作に関する情報を提供する <xref:Microsoft.Xrm.Sdk.IPluginExecutionContext.ParentContext> に関する情報を提供します。

ただし、利用可能な残りの情報は、このクラスが実装する <xref:Microsoft.Xrm.Sdk.IExecutionContext> インターフェイスで提供されます。 このクラスのすべてのプロパティは、コードにアクセスするために必要となる場合のある有用な情報を提供しますが、最も重要な 2 つは <xref:Microsoft.Xrm.Sdk.IExecutionContext.InputParameters> および <xref:Microsoft.Xrm.Sdk.IExecutionContext.OutputParameters> プロパティです。 

よく使用する他のプロパティは、<xref:Microsoft.Xrm.Sdk.IExecutionContext.SharedVariables>、<xref:Microsoft.Xrm.Sdk.IExecutionContext.PreEntityImages>、および <xref:Microsoft.Xrm.Sdk.IExecutionContext.PostEntityImages> です。

> [!TIP]
> 実行コンテキストに渡されたデータを視覚化する良い方法は、プラグイン登録ツールの一部として使用できるプラグイン プロファイラー ソリューションをインストールすることです。 プロファイラーは、コンテキスト情報のほか、デバッグできるようにローカルでイベントを再現できる情報も取得します。 プラグイン登録ツール内で、ワークフローを開始したイベントの全データを含む xml ドキュメントをダウンロードできます。 詳細: [プラグイン プロファイル データの表示](debug-plug-in.md#view-plug-in-profile-data)

### <a name="work-with-parametercollections"></a>ParameterCollections に関する作業

実行コンテキストのすべてのプロパティは読み取り専用になっています。 しかし `InputParameters`、`OutputParameters`、および `SharedVariables` は、<xref:Microsoft.Xrm.Sdk.ParameterCollection> 値です。 プラグインが登録されているイベント実行パイプラインのステージに応じて、運用動作を変更するためにこれらのコレクションの項目の値を操作することができます。

<xref:Microsoft.Xrm.Sdk.ParameterCollection> 値は <xref:System.Collections.Generic.KeyValuePair%602> 構造として定義されます。 プロパティにアクセスするために、メッセージによって公開されるプロパティの名前について知る必要があります。 たとえば、<xref:Microsoft.Xrm.Sdk.Messages.CreateRequest> の一部として渡す <xref:Microsoft.Xrm.Sdk.Entity> プロパティにアクセスするには、そのプロパティの名前が `Target` であることを確認する必要があります。 次に、このようなコードを使用して、この値にアクセスできます:

```csharp
var entity = (Entity)context.InputParameters["Target"];
```
SDK アセンブリで定義されているメッセージの名前を理解するには、<xref:Microsoft.Xrm.Sdk.Messages> と <xref:Microsoft.Crm.Sdk.Messages> のドキュメントを使用します。 ユーザー定義アクションについては、システムで定義されるパラメーターの名前を参照してください。

### <a name="inputparameters"></a>InputParameters

`InputParameters` は、<xref:Microsoft.Xrm.Sdk.OrganizationRequest>.<xref:Microsoft.Xrm.Sdk.OrganizationRequest.Parameters> の値を表します Web サービスから入力する操作を表すプロパティ。

[メッセージを組織サービスと共に使用する](org-service/use-messages.md) で説明されているように、システムで発生するすべての操作は最終的に、<xref:Microsoft.Xrm.Sdk.IOrganizationService>.<xref:Microsoft.Xrm.Sdk.IOrganizationService.Execute*> よって処理されている `OrganizationRequest` クラスのインスタンスです。  メソッド。

[イベント フレームワーク](event-framework.md) で説明されているように、操作が一連のステージに移動し、データがデータベースに記述される前に実行するステージでプラグインを登録できます。 **PreValidation**および **PreOperation**ステージ内で、データ操作の予測結果をコントロールできるように `InputParameters` の値を確認して変更できます。

`InputParameters` コレクションの値が許容できない条件を表す場合、操作を取り消して同期プラグインを持つユーザーにエラーを表示する <xref:Microsoft.Xrm.Sdk.InvalidPluginExecutionException> (好適には**PreValidation**ステージで) をスローするか、またはプラグインが非同期の場合には、エラーをログ記録することができます。 詳細: [操作のキャンセル](#cancelling-an-operation)

### <a name="outputparameters"></a>OutputParameters

`OutputParameters` は、<xref:Microsoft.Xrm.Sdk.OrganizationResponse>.<xref:Microsoft.Xrm.Sdk.OrganizationResponse.Results> の値を表します 操作の戻り値を表すプロパティ。 `OutputParameters` はデータベースのトランザクション後まで設定されないので、**PostOperation**ステージに登録されたプラグインに対してのみ使用できます。 操作により戻った値を変更する場合、`OutputParameters` 内で変更できます。

### <a name="shared-variables"></a>共有変数

<xref:Microsoft.Xrm.Sdk.IExecutionContext.SharedVariables> プロパティは、プラグインから実行パイプラインの後の発生するステップに渡すことができるデータを含めることを可能にします。 これは <xref:Microsoft.Xrm.Sdk.ParameterCollection> 値なので、プラグインはプロパティを追加、読み取り、または変更して後続のステップでデータを共有できます。

次の例は、`PrimaryContact` 値を、**PreOperation** ステップから**PostOperation**ステップまで登録されたプラグインからどのように渡すことができるかを示しています。

```csharp
public class PreOperation : IPlugin
{
    public void Execute(IServiceProvider serviceProvider)
    {
        // Obtain the execution context from the service provider.
        Microsoft.Xrm.Sdk.IPluginExecutionContext context = (Microsoft.Xrm.Sdk.IPluginExecutionContext)
            serviceProvider.GetService(typeof(Microsoft.Xrm.Sdk.IPluginExecutionContext));

        // Create or retrieve some data that will be needed by the post event
        // plug-in. You could run a query, create an entity, or perform a calculation.
        //In this sample, the data to be passed to the post plug-in is
        // represented by a GUID.
        Guid contact = new Guid("{74882D5C-381A-4863-A5B9-B8604615C2D0}");

        // Pass the data to the post event plug-in in an execution context shared
        // variable named PrimaryContact.
        context.SharedVariables.Add("PrimaryContact", (Object)contact.ToString());
    }
}

public class PostOperation : IPlugin
{
    public void Execute(IServiceProvider serviceProvider)
    {
        // Obtain the execution context from the service provider.
        Microsoft.Xrm.Sdk.IPluginExecutionContext context = (Microsoft.Xrm.Sdk.IPluginExecutionContext)
            serviceProvider.GetService(typeof(Microsoft.Xrm.Sdk.IPluginExecutionContext));

        // Obtain the contact from the execution context shared variables.
        if (context.SharedVariables.Contains("PrimaryContact"))
        {
            Guid contact =
                new Guid((string)context.SharedVariables["PrimaryContact"]);

            // Do something with the contact.
        }
    }
}
```


### <a name="entity-images"></a>エンティティ イメージ

エンティティをパラメータの 1 つとして含むプラグインのステップを登録すると、<xref:Microsoft.Xrm.Sdk.IExecutionContext.PreEntityImages> および/または <xref:Microsoft.Xrm.Sdk.IExecutionContext.PostEntityImages> プロパティを使用してエンティティ データのコピーを*スナップショット*またはイメージとして含めるように指定するオプションがあります。

このデータは、イベント パイプラインを介して渡されるエンティティ データの比較ポイントを提供します。 これらのイメージを使用すると、プラグインにコードを含めて属性値を比較するだけのエンティティを取得するよりもはるかに優れたパフォーマンスが得られます。

エンティティ イメージを定義するには、固有イメージにアクセスするために使用できるエンティティ エイリアス値を指定します。 たとえば、プレ エンティティ イメージをエイリアス「`a`」で定義する場合、次のコードを使用して、`name` 属性値にアクセスすることができます。

```csharp
var oldAccountName = (string)context.PreEntityImages["a"]["name"];
```

詳細: [エンティティ イメージの定義](register-plug-in.md#define-entity-images)

## <a name="organization-service"></a>組織のサービス

プラグイン内でデータに関する作業をするには、組織サービスを使用します。 Web API は使用しないでください。 プラグインは .NET SDK アセンブリの使用に最適化されています。

<xref:Microsoft.Xrm.Sdk.IOrganizationService> インターフェイスを実装する `svc` 変数にアクセスするには、次のコードを使用します。


```csharp
// Obtain the organization service reference which you will need for  
// web service calls.  
IOrganizationServiceFactory serviceFactory =
    (IOrganizationServiceFactory)serviceProvider.GetService(typeof(IOrganizationServiceFactory));
IOrganizationService svc = serviceFactory.CreateOrganizationService(context.UserId);
```
<xref:Microsoft.Xrm.Sdk.IOrganizationServiceFactory>.<xref:Microsoft.Xrm.Sdk.IOrganizationServiceFactory.CreateOrganizationService(System.Nullable{System.Guid})> とともに使用される `context.UserId` 変数 <xref:Microsoft.Xrm.Sdk.IExecutionContext.UserId> プロパティは実行コンテキストから取得されますので、この呼び出しが行われるのは、実行コンテキストにアクセスした後です。

詳細:
 - [エンティティ操作](org-service/entity-operations.md)
 - [データのクエリ](org-service/entity-operations-query-data.md)
 - [エンティティの作成](org-service/entity-operations-create.md)
 - [エンティティの取得](org-service/entity-operations-retrieve.md)
 - [エンティティの更新と削除](org-service/entity-operations-update-delete.md)
 - [エンティティの関連付けと関連付け解除](org-service/entity-operations-associate-disassociate.md)
 - [メッセージの使用](org-service/use-messages.md)
 - [遅延バインド および事前バインド プログラミング](org-service/early-bound-programming.md)

プラグイン内で事前バインド型を使用できます。 生成された型ファイルのみをプロジェクトに含めます。 実行コンテキストの入力パラメータによって提供されるすべてのエンティティの種類は遅延バインド型であることに留意する必要があります。 事前バインド型にそれらを変換する必要があります。 たとえば、`Target` パラメーターが取引先企業エンティティを表すことを確認する場合、以下を実行できます。

```csharp
Account acct = context.InputParameters["Target"].ToEntity<Account>();
``` 
ただし、事前バインド型を使用して値を設定しないようにする必要があります。 これを実行しないようにしてください:

```csharp
context.InputParameters["Target"] = new Account() { Name = "MyAccount" }; // WRONG: Do not do this. 
```
これは、<xref:System.Runtime.Serialization.SerializationException> が発生する原因になります。

## <a name="impersonation"></a>偽装

プラグインのコードが異なるユーザーのコンテキストで実行することが必要な場合があります。

プラグインの偽装を適用する 2 つの方法があります: 登録または実行。

### <a name="at-plug-in-registration"></a>プラグイン登録で

プラグイン ステップを登録する場合、**ユーザーのコンテキストで実行**オプションから選択して、コードの実行時に使用するユーザー アカウントを指定できます。 既定では、これは**呼び出し元ユーザー**を使用して設定され、これはアクションを開始したユーザー アカウントです。 このデフォルト オプションが適用される場合、[SdkMessageProcessingStep.ImpersonatingUserId](reference/entities/sdkmessageprocessingstep.md#BKMK_ImpersonatingUserId) は null または <xref:System.Guid.Empty> に設定されます。

詳細: [プラグイン ステップの登録](register-plug-in.md#register-plug-in-step)

### <a name="during-plug-in-execution"></a>プラグイン実行の間

<xref:Microsoft.Xrm.Sdk.IOrganizationServiceFactory>.<xref:Microsoft.Xrm.Sdk.IOrganizationServiceFactory.CreateOrganizationService(System.Nullable{System.Guid})> を設定することによって、実行時に、登録時に指定した設定を上書きできます `userId`パラメーター。

これはに通常、<xref:Microsoft.Xrm.Sdk.IExecutionContext>.<xref:Microsoft.Xrm.Sdk.IExecutionContext.UserId> に設定されます プラグイン ステップ登録によって定義されたユーザー アカウントを適用する値。

```csharp
(IOrganizationServiceFactory)serviceProvider.GetService(typeof(IOrganizationServiceFactory));
    IOrganizationService service = serviceFactory.CreateOrganizationService(context.UserId);
```

ステップ登録を上書きする場合は、<xref:Microsoft.Xrm.Sdk.IExecutionContext>.<xref:Microsoft.Xrm.Sdk.IExecutionContext.InitiatingUserId> の値を渡すことができます プラグインが実行されたアクションを開始したユーザー アカウントを使用するサービスを所持すること。

さらに、任意の有効なユーザー アカウントから [SystemUser.SystemUserId](reference/entities/systemuser.md#BKMK_SystemUserId) を提供することもできます。 これは、そのユーザーがプラグインで操作を実行するアクセス許可を持つそのユーザーである限り、機能します。

## <a name="use-the-tracing-service"></a>トレース サービスの使用

プラグインを実行した場合に発生することを把握するためにログを確認できるよう、トレース サービスを使用して [PluginTraceLog エンティティ](reference/entities/plugintracelog.md) にメッセージを記述します。

トレース ログに記述するには、トレース サービスのインスタンスを取得する必要があります。 次のコードは、<xref:System.IServiceProvider>.<xref:System.IServiceProvider.GetService*> を使用してトレース サービスのインスタンスを取得する方法を示しています  メソッド。


```csharp
// Obtain the tracing service
ITracingService tracingService =
(ITracingService)serviceProvider.GetService(typeof(ITracingService));
```

トレースに記述するには、<xref:Microsoft.Xrm.Sdk.ITracingService>.<xref:Microsoft.Xrm.Sdk.ITracingService.Trace*> を使用します。  メソッド。

```csharp
tracingService.Trace("Write {0} {1}.", "your", "message");
```

詳細: [トレースの使用](debug-plug-in.md#use-tracing)。



## <a name="cancelling-an-operation"></a>操作のキャンセル

例外をスローすることで、コードで操作を取り消すことができます。 いずれかの処理されない例外で操作は取り消されるので、スローされる例外を管理するためにコーディング プラクティスを適用し、操作を取り消しを許可するかどうかを決定することが重要です。

ビジネス ロジックが操作を取り消す必要があることを指示する場合、<xref:Microsoft.Xrm.Sdk.InvalidPluginExecutionException> 例外をスローし、操作が表示取り消された理由を説明するメッセージを提供する必要があります。

同期プラグイン内で <xref:Microsoft.Xrm.Sdk.InvalidPluginExecutionException> 例外をスローすると、メッセージを含むエラー ダイアログがユーザーに表示されます。 メッセージを提供しない場合、一般的なエラー ダイアログがユーザーに表示されます。 例外のいずれか他の種類がスローされる場合、ユーザーには一般的なメッセージを含むエラー ダイアログが表示され、例外のメッセージとスタック トレースが [PluginTraceLog エンティティ](reference/entities/plugintracelog.md) に記述されます。

理想的なのは、**PreValidation** ステージで登録された同期プラグインを使用してのみ操作をキャンセルすることです。 このステージは*通常*、データベース トランザクションの外部で実行されます。 トランザクションに達する前に操作を取り消すことは、キャンセルされた操作がロールバックされる必要があるため、非常に推奨されています。 操作をロールバックすることには重要なリソースが必要で、システムのパフォーマンスに影響します。 **PreOperation**および **PostOperation**ステージの操作は常に、データベース トランザクション内にあります。

**PreValidation**ステージは、別の操作のロジックで開始される場合、トランザクション内になる場合もあります。 たとえば、取引先企業の作成の**PreOperation**ステージのタスク エンティティ レコードを作成する場合、タスクの作成はイベント実行パイプラインを通って渡され、**PreValidation**ステージ内で発生しますが、取引先企業のエンティティ レコードを作成するトランザクションの一部です。 <xref:Microsoft.Xrm.Sdk.IExecutionContext>.<xref:Microsoft.Xrm.Sdk.IExecutionContext.IsInTransaction> の値で操作がトランザクション内にあるかどうかを判断できます。 プロパティに設定します。

## <a name="performance-considerations"></a>パフォーマンスに関する考慮事項

プラグインに関するビジネス ロジックを追加するときには、パフォーマンス全体に及ぶ影響を十分に認識する必要があります。 プラグインのビジネス ロジックは完了するまで、2 秒以内である必要があります。

### <a name="time-and-resource-constraints"></a>時間とリソースの制約

メッセージ操作が完了するまでには、2 分という時間制限があります。 拡張機能で使用できる CPU およびメモリ リソースの容量にも制限があります。 制限を超えた場合、例外がスローされ、操作はキャンセルされます。

時間制限を超えた場合、<xref:System.TimeoutException> がスローされます。 いずれかのカスタム拡張が CPU、メモリ、またはハンドルの制限のしきい値を超過するか、何らかの理由で反応しなくなった場合、そのプロセスはプラットフォームによって強制終了されます。 その時点で、そのプロセスで実行中のすべての拡張機能は例外により失敗します。 ただし、拡張機能の次回の実行時には、拡張機能は正常に動作します。

### <a name="monitor-performance"></a>パフォーマンスの監視

プラグインおよびカスタム ワークフローの拡張機能に関するランタイム情報は取得され、[PluginTypeStatistic エンティティ](reference/entities/plugintypestatistic.md) に格納されます。 これらのレコードは、カスタム コードの実行後、30 分から 1 時間以内にデータが取り込まれます。 このエンティティは、次のデータ ポイントを提供します。

|**属性**|**説明**|
|--|--|
|AverageExecuteTimeInMilliseconds|プラグインの種類の平均実行時間 (ミリ秒) です。 |
|CrashContributionPercent|クラッシュの原因となったプラグインの種類の割合です。 |
|CrashCount|プラグインの種類がクラッシュした回数です。 |
|CrashPercent|プラグインの種類のクラッシュ率です。 |
|ExecuteCount|プラグインの種類が実行された回数です。 |
|FailureCount |プラグインの種類が失敗した回数です。 |
|FailurePercent|プラグインの種類の失敗率です。 |
|PluginTypeIdName|プラグインの種類の統計を最後に修正したユーザーを表す一意識別子です。 |
|TerminateCpuContributionPercent |プラグインの種類が CPU の過剰使用によるワーカー プロセスの終了に影響を与えた割合です。 |
|TerminateHandlesContributionPercent |プラグインの種類がハンドルの過剰使用によるワーカー プロセスの終了に影響を与えた割合です。 |
|TerminateMemoryContributionPercent|プラグインの種類がメモリの過剰使用によるワーカー プロセスの終了に影響を与えた割合です。 |
|TerminateOtherContributionPercent|プラグインの種類が不明な理由によるワーカー プロセスの終了に影響を与えた割合です。 |

このデータは、有用な他の多くのレポートとともに、[組織のインサイト プラグイン ダッシュボード](/dynamics365/customer-engagement/admin/use-organization-insights-solution-view-instance-metrics#plug-ins)使用して参照することでも入手可能です。


## <a name="next-steps"></a>次のステップ

[プラグインの登録](register-plug-in.md)<br />
[プラグインのデバッグ](debug-plug-in.md)

### <a name="see-also"></a>関連項目

[ビジネス プロセスを拡張するためのプラグインを記述する](plug-ins.md)<br />
[チュートリアル: プラグインを書き込み登録する](tutorial-write-plug-in.md)<br />
[チュートリアル: プラグインをデバッグする](tutorial-debug-plug-in.md)<br />
[チュートリアル: プラグインを更新する](tutorial-update-plug-in.md)<br />
