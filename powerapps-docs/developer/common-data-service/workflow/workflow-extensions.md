---
title: ワークフローの拡張機能 (Common Data Service) | Microsoft Docs
description: ワークフローのデザイナー内で使用可能なオプションを拡張できます。 これらの拡張機能は、CodeActivity クラスを拡張するクラスを含むアセンブリを追加することによって追加されます。 これらの拡張機能は一般的に、ワークフロー アセンブリまたはワークフロー活動と呼ばれます。
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: JimDaly
ms.author: jdaly
manager: ryjones
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="workflow-extensions"></a>ワークフローの拡張機能

Common Data Service で使用するワークフローのデザイナー内で使用可能なオプションを拡張できます。 これらの拡張機能は、[CodeActivity](/dotnet/api/system.activities.codeactivity) クラスを拡張するクラスを含むアセンブリを追加することによって追加されます。 これらの拡張機能は一般的に、ワークフロー アセンブリまたはワークフロー活動と呼ばれます。

ワークフロー、カスタム アクション、およびダイアログで使用されるデザイナー内のこれらカスタム拡張機能を使用できます。

> [!IMPORTANT]
> 可能な限り、ビジネスロジックを定義するいくつかの宣言型オプションの 1 つを適用することを最初に検討する必要があります。 詳細: [Common Data Service でビジネス ロジックの適用](../../../maker/common-data-service/cds-processes.md)<br/><br/>
> 宣言型プロセスが要件を満たさない場合、ワークフローの拡張機能を使用します。

## <a name="when-to-create-a-workflow-extension"></a>ワークフローの拡張機能を作成するとき

ユーザーが既定のプロセス活動を使用して必要な機能を見出せない場合、ワークフロー、ダイアログ、およびアクションのプロセスを作成するために使用するエディターで使用できるように、カスタム活動を追加できます。

既定では、これらのプロセスには、次の表に示すとおりに実行できる活動の共通セットが含まれます。

|活動|ワークフロー|目的|[ダイアログ]|
|--|--|--|--|
|データのクエリ|||X|
|[値の割り当て]||X|X|
|[レコードの作成]|X|X|X|
|[レコードの更新]|X|X|X|
|レコードの割り当て|X|X|X|
|電子メールの送信|X|X|X|
|子ワークフローの開始|X|X|X|
|アクションの実行|X|X||
|子ダイアログのリンク|||X|
|[状態の変更]|X|X|X|
|ワークフローの停止|X|X||
|ダイアログの停止|||X|

いずれかのユーザー定義アクションを実行するために**アクションの実行**活動を使用するか、または**コマンド アクション**と呼ばれる次のシステムメッセージを使用できます。

||||
|--|--|--|
|AddToQueue|AddUserToRecordTeam|RemoveUserFromRecordTeam|
|SetProcess|SetWordTemplate||

Dynamics 365 Customer Engagement の営業またはサービス ソリューションがある場合、ソリューションに応じて他のコマンド アクションを見つけることができます。

||||
|--|--|--|
|ApplyRoutingRule|CalculateActualValue|CloseOpportunity|
|GetQuoteProductsFromOpportunity|GetSalesOrderProductsFromOpportunity|LockInvoicePricing|
|LockSalesOrderPricing|QualifyLead|RemoveUserFromRecordTeam|
|ResolveIncident|ResolveQuote|Revise|
|UnlockInvoicePricing|UnlockSalesOrderPricing|

詳細: 

- [ワークフロー ステージとステップの構成](/flow/configure-workflow-steps)
- [ガイド付きプロセス用 Common Data Service ダイアログの使用](/flow/use-cds-for-apps-dialogs)
- [ユーザー定義アクションの作成](/flow/create-actions)



## <a name="technology-used"></a>使用するテクノロジ

プロセスでは Windows Workflow Foundation を使用するので、Web アプリケーションのエディター内に表示され、プロセス実行時には起動するユーザー定義活動を定義する [.NET Framework アクティビティ ライブラリ](/dotnet/framework/windows-workflow-foundation/net-framework-4-5-built-in-activity-library) を使用して構築されるアセンブリを登録できます。

ユーザー定義ワークフロー活動では、 抽象 [CodeActivity クラス](/dotnet/api/system.activities.codeactivity?view=netframework-4.6.2) から派生した 1 つ以上のクラスを含む .NET Framework アセンブリの作成が必要です。 このクラスは、活動実行時に Common Data Service プラットフォームにより呼び出される [Execute(CodeActivityContext) メソッド](/dotnet/api/system.activities.codeactivity.execute?view=netframework-4.6.2) を提供します。 アセンブリの各クラスは特定の活動を定義します。

ワークフロー活動でも、プロセス デザイナーに表示され、ユーザーがデータをワークフロー活動に渡して、処理済み出力を受け取ることができる入力および出力パラメーターを定義できます。 クラスを記述する際、これらのパラメーターのプロパティの追加して、[.NET 属性](/dotnet/standard/attributes/index) で注釈を付けて、Common Data Service がデザイナーのいずれかのパラメーターでカスタム ワークフロー活動を公開するために使用するメタデータを提供します。

## <a name="visual-studio-requirements"></a>Visual Studio の要件

ユーザー定義ワークフロー活動を作成するには、**.NET デスクトップ開発**ワークロードで Visual Studio 、および **Windows Workflow Foundation**の個々のコンポーネントをインストールする必要があります。

無料の Visual Studio 2017 Community Edition または Professional および Enterprise Editionを使用できます。

インストールを確認するか、またはこのコンポーネントを追加するには:

1. Visual Studio 2017 を開きます
1. **ツール** > **ツールと機能の取得…** を選択します   これによって Visual Studio インストーラが開きます
1. **ワークロード**タブで、**.NET デスクトップ開発**ワークロードが選択されていることを確認します。
    ![必須の Visual Studio ワークロード](media/visual-studio-workloads-workflow-extensions.png)
1. **個々のコンポーネント**を選択し、**開発活動**セクションにスクロールします。
    ![必須の Visual Studio の個々のコンポーネント](media/visual-studio-individual-components-workflow-extensions.png)
1. **Windows Workflow Foundation**が選択されていない場合には、それを選択します。 **Windows Communication Foundation** コンポーネントも含まれます。
1. 新しいワークロードまたはコンポーネントを追加した場合は、Visual Studio インストーラがそれをインストールできるように **変更**をクリックします。 それ以外の場合は、Visual Studio インストーラを閉じます。

詳細: [Visual Studio 2017 のインストール](/visualstudio/install/install-visual-studio)

## <a name="create-a-custom-workflow-activity-assembly"></a>ユーザー定義ワークフロー活動の作成

これらは、Visual Studio を使用してユーザー設定ワークフロー活動を作成するために使用される一般的な方法です。 完全な手順ごとの例については、[チュートリアル: ワークフロー拡張の作成](tutorial-create-workflow-extension.md) を参照してください。

1. ターゲット フレームワークとして .NET Framework 4.6.2 を使用してワークフロー活動ライブラリ プロジェクトを作成します。
1. プロジェクトで生成された Activity1.xaml ファイルを削除します。
1. [Microsoft.CrmSdk.Workflow](https://www.nuget.org/packages/Microsoft.CrmSdk.Workflow/) NuGet パッケージをインストールします。

    このパッケージには、[Microsoft.CrmSdk.CoreAssemblies](https://www.nuget.org/packages/Microsoft.CrmSdk.CoreAssemblies/) パッケージが含まれています。

1. (オプション) 事前バインド エンティティ クラスを使用する場合には、それらをプロジェクトに含めます。

    詳細: 

    - [組織サービスを使用して遅延バインドと事前バインドのプログラミング クラス](../org-service/early-bound-programming.md)
    - [組織サービスの事前バインド クラスを生成する](../org-service/generate-early-bound-classes.md) 

1. パブリック クラスを追加します。 クラスの名前は、活動により実行されるアクションに対応する必要があります。
1. 次の using ディレクティブを追加する

    ```csharp
    using System.Activities;
    using Microsoft.Xrm.Sdk;
    using Microsoft.Xrm.Sdk.Workflow;
    ```

1. いずれかの入力または出力パラメーターを表すためにプロパティをクラスの追加し、これらのプロパティをワークフロー プロセス デザイナーに公開するために必要なメタデータを提供するため [.NET 属性](/dotnet/standard/attributes/index) を使用します。

    詳細: [パラメーターの追加](#add-parameters)

1. クラスが [CodeActivity クラス](/dotnet/api/system.activities.codeactivity?view=netframework-4.6.2) から派生し、活動が行う操作を含む [Execute(CodeActivityContext) メソッド](/dotnet/api/system.activities.codeactivity.execute?view=netframework-4.6.2) を実施するようにします。

    詳細: [Execute メソッドにコードを追加する](#add-your-code-to-the-execute-method)

1. アセンブリにサインする
1. アセンブリを構築します。
1. アセンブリをプラグイン登録ツールを使用して登録し、Dyn365CE プロセス デザイナーに表示されるテキストを定義する名前とWorkflowActivityGroupName プロパティを設定します。

    詳細: [アセンブリの登録](#register-your-assembly)

1. ワークフロー活動を、ワークフロー、ダイアログ、またはアクション プロセス内から呼び出すことでテストします。
1. (推奨) ソリューションにワークフロー活動を追加します。

## <a name="add-parameters"></a>パラメータを追加する

クラスのパラメーターを定義するとき、[InArgument<T>](/dotnet/api/system.activities.inargument-1)、[OutArgument<T>](/dotnet/api/system.activities.outargument-1)、または[InOutArgument<T>](/dotnet/api/system.activities.inoutargument-1)の種類として定義する必要があります。 これらの種類は、パラメーターを取得または設定するために共通の [引数クラス](/dotnet/api/system.activities.argument) から継承したメソッドを提供します。 コードは Execute メソッドでこれらのメソッドを使用します。 詳細: [Execute メソッドにコードを追加する](#add-your-code-to-the-execute-method)

ユーザー定義ワークフロー活動が入力または出力パラメーターを使用する場合、定義するパブリック クラスのプロパティに適した .NET 属性を追加する必要があります。 このデータはプロセス デザイナーによって読み取られ、プロセス デザイナーでどのようにパレメーターを設定できるかを定義します。

入力または出力パラメーターとしてプロパティの以下の種類を使用できます。

||||
|--|--|--|
|[bool](/dotnet/api/system.boolean)|[DateTime](/dotnet/api/system.datetime)|[[小数]](/dotnet/api/system.decimal)|
|[Double](/dotnet/api/system.double)|<xref:Microsoft.Xrm.Sdk.EntityReference>|[int](/dotnet/api/system.int32)|
|<xref:Microsoft.Xrm.Sdk.Money>|<xref:Microsoft.Xrm.Sdk.OptionSetValue>|[string](/dotnet/api/system.string)|

### <a name="input-and-output-parameters"></a>入力および出力パラメーター

プロセス デザイナーの入力または出力パラメーターに表示するテキストを定義するには、[.NET 属性](/dotnet/standard/attributes/index) を使用し、次のパターンを使用します。

```csharp
[Input("Integer input")]
public InArgument<int> IntInput { get; set; }
```

または

```csharp
[Output("Integer output")]
public OutArgument<int> IntOutput { get; set; }
```

クラスの 1 つのプロパティは、両方の属性を含めることにより、入力および出力パラメーターの両方とすることができます:

```csharp
[Input("Int input")]  
[Output("Int output")]  
public InOutArgument<int> IntParameter { get; set; }
```


### <a name="required-values"></a>必要な値

ワークフロー活動をプロセスで使用するときに必要な入力パラメータを作成する場合は、`[RequiredArgument]` 属性を使用する必要があります。

### <a name="default-values"></a>既定値

入力パラメーターとして渡す値または出力パラメーターとして設定する値が定義されていない場合、既定値を指定できます。 たとえば、ブール値プロパティの既定値を設定するには:

```csharp
[Input("Bool input")]
[Default("True")]
public InArgument<bool> Bool { get; set; }
```

既定値の形式はプロパティの種類に応じて異なります。 例が次の表にあります。

|型|例|
|--|--|
|[bool](/dotnet/api/system.boolean)|[既定値 ("True")]|
|[DateTime](/dotnet/api/system.datetime)|[既定 ("2004-07-09T02:54:00Z")]|
|[[小数]](/dotnet/api/system.decimal)|[既定 ("23.45")]|
|[Double](/dotnet/api/system.double)|[既定 ("23.45")]|
|<xref:Microsoft.Xrm.Sdk.Money>|[既定 ("23.45")]|
|<xref:Microsoft.Xrm.Sdk.EntityReference>|[既定 ("3B036E3E-94F9-DE11-B508-00155DBA2902"、"取引先企業")]|
|[int](/dotnet/api/system.int32)|[既定 ("23")]|
|<xref:Microsoft.Xrm.Sdk.OptionSetValue>|[既定 ("3")]|
|[string](/dotnet/api/system.string)|[既定 ("文字列既定")]|

### <a name="entityreference-parameters"></a>EntityReference パラメーター

<xref:Microsoft.Xrm.Sdk.EntityReference> パラメーターのプロパティを定義するとき、`ReferenceTarget` 属性を使用する必要があります。 これによって、許可される属性の種類が確立されます。 たとえば、次のようになります。

```csharp
[Input("EntityReference input")]
[Output("EntityReference output")]
[ReferenceTarget("account")]
public InOutArgument<EntityReference> AccountReference { get; set; }
```

### <a name="optionsetvalue-parameters"></a>OptionSetValue パラメーター

<xref:Microsoft.Xrm.Sdk.OptionSetValue> パラメーターのプロパティを定義するとき、`AttributeTarget` 属性を使用する必要があります。 この属性は、パラメータの値を有効なセットを含むエンティティと属性を定義します。 たとえば、次のようになります。

```csharp
[Input("Account IndustryCode value")]
[AttributeTarget("account", "industrycode")]
[Default("3")]
public InArgument<OptionSetValue> IndustryCode { get; set; }
```

## <a name="add-your-code-to-the-execute-method"></a>Execute メソッドへのコードの追加

[CodeActivity.Execute(CodeActivityContext) メソッド](/dotnet/api/system.activities.codeactivity.execute?view=netframework-4.6.2) メソッドに含めるロジックはワークフロー活動の内容を定義します。

> [!IMPORTANT]
> `Execute` メソッド内のコードはステートレスとして記述される必要があります。 1 つ呼び出しから次にデータを渡すためにグローバルまたはメンバー変数を使用することは推奨されていません。
> パフォーマンスを向上させるため、Common Data Service では、ユーザー定義のワークフロー活動インスタンスをキャッシュしています。 このため、コンストラクターは、ユーザー定義のワークフロー活動のすべての呼び出しでは呼び出されません。 また、ユーザー定義のワークフロー活動を複数のシステムのスレッドが同時に実行する可能性があります。 [CodeActivityContext](/dotnet/api/system.activities.codeactivitycontext) パラメーターを介して `Execute` メソッドに渡される情報のみを使用する必要があります。

### <a name="reference-parameters"></a>Reference パラメーター

クラスに対して定義されたパラメーターを参照するには、`Execute` メソッドに渡される [CodeActivityContext](/dotnet/api/system.activities.codeactivitycontext) インスタンスを必要とし、それらが提供する [Argument.Get](/dotnet/api/system.activities.argument.get?view=netframework-4.6.2) または [Argument.Set (ActivityContext、オブジェクト) ](/dotnet/api/system.activities.argument.set?view=netframework-4.6.2) メソッドを使用します。 次の例では、入力パラメーターの値へのアクセスおよび出力パラメーターの値の設定を示しています。

```csharp
using Microsoft.Xrm.Sdk.Workflow;
using System.Activities;

namespace SampleWorkflowActivity
{
  public class IncrementByTen : CodeActivity
  {
    [RequiredArgument]
    [Input("Decimal input")]
    public InArgument<decimal> DecInput { get; set; }

    [Output("Decimal output")]
    public OutArgument<decimal> DecOutput { get; set; }

    protected override void Execute(CodeActivityContext context)
    {
      decimal input = DecInput.Get(context);
      DecOutput.Set(context, input + 10);
    }
  }
}
```

### <a name="get-contextual-information"></a>コンテキスト情報を取得する

コードにコンテキスト情報が必要な場合、<xref:Microsoft.Xrm.Sdk.Workflow.IWorkflowContext> インターフェイスで [CodeActivityContext.GetExtension<T> メソッド](/dotnet/api/system.activities.activitycontext.getextension)を使用してこれにアクセスできます。 このオブジェクトは、操作のコンテキストを記述する多くの読み取り専用プロパティにアクセスできる <xref:Microsoft.Xrm.Sdk.IExecutionContext> インターフェイスから派生しています。 `IWorkflowContext` では、ワークフロー アセンブリを使用している実行中のワークフロー特有の類似したコンテキスト情報を提供します。

`IWorkflowContext` にアクセスするには `Execute` 関数の次のコードを使用します。

```csharp
protected override void Execute(CodeActivityContext context)
{
 IWorkflowContext workflowContext = context.GetExtension<IWorkflowContext>();

...
```

### <a name="use-the-organization-service"></a>組織サービスの使用

組織サービスを使用してデータ操作の実行が必要になる場合、<xref:Microsoft.Xrm.Sdk.IOrganizationServiceFactory> インターフェイスで [CodeActivityContext.GetExtension<T>](/dotnet/api/system.activities.activitycontext.getextension) メソッドを使用してこれにアクセスできます。 そこから、<xref:Microsoft.Xrm.Sdk.IOrganizationServiceFactory.CreateOrganizationService(System.Nullable{System.Guid})> メソッドを使用して、データ操作を実行するために使用できるサービス プロキシのインスタンスにアクセスできます。 <xref:Microsoft.Xrm.Sdk.Workflow.IWorkflowContext>.<xref:Microsoft.Xrm.Sdk.IExecutionContext.InitiatingUserId> 操作が電話プロセスと同じコンテキストで行われるようにする場合、使用するユーザー コンテキストを特定するために使用できます。
組織サービスにアクセスするには `Execute` 関数の次のコードを使用します。

```csharp
protected override void Execute(CodeActivityContext context)
{
 IWorkflowContext workflowContext = context.GetExtension<IWorkflowContext>();
 IOrganizationServiceFactory serviceFactory = context.GetExtension<IOrganizationServiceFactory>();

 // Use the context service to create an instance of IOrganizationService.             
 IOrganizationService service = serviceFactory.CreateOrganizationService(workflowContext.InitiatingUserId);

...
```

## <a name="register-your-assembly"></a>アセンブリの登録

ユーザー定義のワークフロー活動を含むアセンブリを登録するには、プラグイン登録ツール (PRT) を使用します。 これは、プラグインを登録するために使用するツールと同じです。プラグインとユーザー定義のワークフロー活動の両方で、環境にアップロードするアセンブリを登録する必要があります。 ただし、ユーザー定義のワークフロー活動のステップは登録しません。

ユーザー定義のワークフロー活動の場合、ワークフロー プロセス デザイナーでの表示をコントロールするために、次のプロパティを指定する必要があります。

|フィールド|説明|
|--|--|
|説明|プロセス デザイナーの UI に表示されませんが、この情報を格納する PluginType エンティティから取得されたデータからドキュメントを生成するときに便利な場合があります。|
|FriendlyName|プラグインのユーザー フレンドリ名です。|
|Name|表示されたメニューの名前|
|WorkflowActivityGroupName|Common Data Service プロセス デザイナーのメイン メニューに追加されるサブメニューの名前。|

![説明のプロパティの設定](media/create-workflow-activity-set-properties.png)

> [!NOTE]
> これらの値は、ワークフロー活動をテストするときにアンマネージド ソリューションに表示されません。 ただし、このワークフロー活動を含む管理ソリューションをエクスポートする場合、これらの値はプロセス デザイナーに表示されます。

## <a name="debug-workflow-activities"></a>ワークフロー活動のデバッグ

Common Data Service に展開されるユーザー定義のワークフロー活動を使用すると、ローカル デバッグのために再生し、情報をエンティティに記述するトレース サービスを使用するプロファイルを取得できます。 

次の例は、次のメッセージ: `Add your message.` を記述するためにトレース サービスを使用することを示しています。

```csharp
protected override void Execute(CodeActivityContext context)
{
//Create the tracing service
ITracingService tracingService = executionContext.GetExtension<ITracingService>();

//Use the tracing service
tracingService.Trace("{0} {1} {2}.","Add","your","message");

...
```

詳細:
 - [ワークフロー活動のデバッグ](debug-workflow-activites.md)
 - [トレースを使用する](../debug-plug-in.md#use-tracing)
 - [トレース ログの表示](../tutorial-write-plug-in.md#view-trace-logs)

## <a name="add-to-solution"></a>ソリューションへの追加

**既定のソリューション**に追加されるプラグイン登録ツールを使用してアセンブリを登録する場合には、**Common Data Service の既定のソリューション**と混同しないでください。 **既定のソリューション** には環境に適用されるすべてのアンマネージド カスタマイズが含まれているため、ソリューションを使用してユーザー設定ワークフロー活動を配布する前にアンマネージド ソリューションに追加する必要があります。 たとえば、**Common Data Service の既定のソリューション**または作成した任意のアンマネージド ソリューションに追加できます。

## <a name="manage-changes-to-custom-workflow-activities"></a>ユーザー定義のワークフロー活動への変更の管理

ユーザー定義のワークフロー活動のコードを保守する必要があります。 コード変更には大きな変更が含まれる場合があるので、この変更を管理する必要があります。 ユーザー定義のワークフロー アセンブリを更新またはアップグレードするには、さまざまな手順を使用します。

ユーザー定義のワークフロー活動を含むアセンブリの登録時には、アセンブリのバージョンが含まれています。 この情報はアセンブリからのリフレクションを使用して得られます。 Visual Studio プロジェクトの `AssemblyInfo.cs` ファイルを使用してバージョン番号をコントロールできます。

下部のセクションはこのように表示されます:


```
// Version information for an assembly consists of the following four values:
//
//      Major Version
//      Minor Version 
//      Build Number
//      Revision
//
// You can specify all the values or you can default the Build and Revision Numbers 
// by using the '*' as shown below:
//[assembly: AssemblyVersion("1.0.0.*")]
[assembly: AssemblyVersion("1.0.0.0")]
[assembly: AssemblyFileVersion("1.0.0.0")]
```

このバージョン情報は、新しい機能を含めるときに、更新を展開されたアセンブリまたはアップグレード アセンブリに適用できるので重要です。

### <a name="update-a-custom-workflow-activity-assembly"></a>ユーザー定義のワークフロー活動アセンブリの更新

パブリック クラスやメソッド シグネチャを大幅に変更しないバグまたはリファクター コードを修正するために変更する場合、実行中のすべてのプロセスが自動的に新しいバージョンのアセンブリを使用して開始するようにアセンブリを更新できます。

#### <a name="to-update-an-assembly"></a>アセンブリを更新するには:

1. `AssemblyInfo.cs` `AssemblyVersion` 属性の**ビルド番号**と**リビジョンの値**のみを変更します。 たとえば、`1.0.0.0` から `1.0.10.5` に変更します。
1. アセンブリを更新するには、プラグイン登録ツールを使用します。 詳細: [アセンブリの更新](../register-plug-in.md#update-an-assembly)

#### <a name="upgrade-a-custom-workflow-activity-assembly"></a>ユーザー定義のワークフロー活動アセンブリの更新:

パブリック クラスやメソッド シグネチャへの大幅な変更を含む変更を行う場合、パラメーターの変更など、元のシグネチャを使用するように定義されたすべての現在実行中のプロセスを切断します。 この場合、アセンブリをアップグレードする必要があります。 これによって、プロセス デザイナーで適用するバージョンを定義するオプションを公開する新しいユーザー定義のワークフロー活動が作成されます。 これによって、活動を使用する各プロセスを新しいアセンブリに含まれる変更に適応するように再構成することができます。 元のアセンブリを使用するすべてプロセスがアップグレードされたアセンブリを使用して更新された後、古いアセンブリの登録を取り消すことができます。

#### <a name="to-upgrade-an-assembly"></a>アセンブリを更新するには:

1. 新しいアセンブリには、既存のアセンブリと同じ `Name`、`PublicKeyToken`、および `Culture` があることを確認してください。
1. `AssemblyInfo.cs` `AssemblyVersion` 属性の**メジャー バージョン**および/または**マイナー バージョン**の値を変更します。 たとえば、`1.0.0.0` から `2.0.0.0` に変更します。
1. 新しいアセンブリとしてアセンブリを登録するには、プラグイン登録ツールを使用します。 詳細: [アセンブリの登録](../register-plug-in.md#register-an-assembly)
1. ユーザー定義のワークフロー活動を使用した各プロセスの場合、プロセスを非アクティブ化してユーザー定義のワークフロー活動を使用する手順を編集する必要があります。

    使用するアセンブリのバージョンを選択するために使用できるプロセス デザイナーで**バージョン**を検索します。

    ![ワークフロー設定バージョン](media/workflow-set-version.png)

新しいアセンブリを使用するようにすべてのプロセスが変換されるとき、もう使用できないようにするために、アセンブリの登録解除にプラグイン登録ツールを使用できます。 詳細: [コンポーネントの登録解除](../register-plug-in.md#unregister-components)


### <a name="see-also"></a>関連項目

[プラグインとワークフロー開発に関するベストプラクティスとガイダンス](../best-practices/business-logic/index.md) 
[チュートリアル: ワークフロー拡張機能の作成](tutorial-create-workflow-extension.md)<br />
[サンプル: カスタム ワークフロー活動の作成](sample-create-custom-workflow-activity.md)<br />
[サンプル: ユーザー定義ワークフロー活動を使用した次回の誕生日の更新](sample-update-next-birthday-using-custom-workflow-activity.md)<br />
[サンプル: ユーザー定義ワークフロー活動でクレジット スコアを計算する](sample-calculate-credit-score-custom-workflow-activity.md)
