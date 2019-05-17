---
title: 実行コンテキストを理解する (Common Data Service) | Microsoft Docs
description: 実行時にプラグインに渡されるデータについて説明します。
ms.custom: ''
ms.date: 1/23/2019
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: phecke
ms.author: pehecke
manager: kvivek
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---

# <a name="understand-the-execution-context"></a>実行コンテキストを理解する

**イベント実行パイプライン** は、登録されているプラグインに、処理中の現在の操作とプラグインの実行環境に関する豊富なデータを渡します。 <xref:Microsoft.Xrm.Sdk.IPluginExecutionContext> インターフェースを実装する変数を設定することで、プラグイン コードでこのデータにアクセスできます。

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

## <a name="parametercollections"></a>ParameterCollections

実行コンテキストのすべてのプロパティは読み取り専用になっています。 しかし `InputParameters`、`OutputParameters`、および `SharedVariables` は、<xref:Microsoft.Xrm.Sdk.ParameterCollection> 値です。 プラグインが登録されているイベント実行パイプラインのステージに応じて、運用動作を変更するためにこれらのコレクションの項目の値を操作することができます。

<xref:Microsoft.Xrm.Sdk.ParameterCollection> 値は <xref:System.Collections.Generic.KeyValuePair%602> 構造として定義されます。 プロパティにアクセスするために、メッセージによって公開されるプロパティの名前について知る必要があります。 たとえば、<xref:Microsoft.Xrm.Sdk.Messages.CreateRequest> の一部として渡す <xref:Microsoft.Xrm.Sdk.Entity> プロパティにアクセスするには、そのプロパティの名前が `Target` であることを確認する必要があります。 次に、このようなコードを使用して、この値にアクセスできます:

```csharp
var entity = (Entity)context.InputParameters["Target"];
```
SDK アセンブリで定義されているメッセージの名前を理解するには、<xref:Microsoft.Xrm.Sdk.Messages> と <xref:Microsoft.Crm.Sdk.Messages> のドキュメントを使用します。 ユーザー定義アクションについては、システムで定義されるパラメーターの名前を参照してください。

## <a name="inputparameters"></a>InputParameters

`InputParameters` は、<xref:Microsoft.Xrm.Sdk.OrganizationRequest>.<xref:Microsoft.Xrm.Sdk.OrganizationRequest.Parameters> の値を表します Web サービスから入力する操作を表すプロパティ。

[メッセージを組織サービスと共に使用する](org-service/use-messages.md) で説明されているように、システムで発生するすべての操作は最終的に、<xref:Microsoft.Xrm.Sdk.IOrganizationService>.<xref:Microsoft.Xrm.Sdk.IOrganizationService.Execute*> よって処理されている `OrganizationRequest` クラスのインスタンスです。  メソッド。

[イベント フレームワーク](event-framework.md) で説明されているように、操作が一連のステージに移動し、データがデータベースに記述される前に実行するステージでプラグインを登録できます。 **PreValidation**および **PreOperation**ステージ内で、データ操作の予測結果をコントロールできるように `InputParameters` の値を確認して変更できます。

`InputParameters` コレクションの値が許容できない条件を表す場合、操作を取り消して同期プラグインを持つユーザーにエラーを表示する <xref:Microsoft.Xrm.Sdk.InvalidPluginExecutionException> (好適には**PreValidation**ステージで) をスローするか、またはプラグインが非同期の場合には、エラーをログ記録することができます。 詳細: [操作のキャンセル](handle-exceptions.md#cancelling-an-operation)

## <a name="outputparameters"></a>OutputParameters

`OutputParameters` は、<xref:Microsoft.Xrm.Sdk.OrganizationResponse>.<xref:Microsoft.Xrm.Sdk.OrganizationResponse.Results> の値を表します 操作の戻り値を表すプロパティ。 `OutputParameters` はデータベースのトランザクション後まで設定されないので、**PostOperation**ステージに登録されたプラグインに対してのみ使用できます。 操作により戻った値を変更する場合、`OutputParameters` 内で変更できます。

## <a name="shared-variables"></a>共有変数

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
> [!IMPORTANT]
> 共有される変数のコレクションに追加されたデータは、シリアル化可能な種類のデータである必要があります。そうしないと、データをシリアル化する方法をサーバーが判断できず、プラグインの実行が失敗します。  
  
 段階 20 または 40 で登録されたプラグインの場合、作成、更新、削除の際に実行する段階 10 で登録されたプラグインから、または <xref:Microsoft.Crm.Sdk.Messages.RetrieveExchangeRateRequest> によって共有される変数にアクセスするには、<xref:Microsoft.Xrm.Sdk.IPluginExecutionContext.ParentContext>.**SharedVariables** コレクションにアクセスする必要があります。 それ以外の場合は、<xref:Microsoft.Xrm.Sdk.IPluginExecutionContext>.**SharedVariables** にコレクションが格納されます。 

## <a name="entity-images"></a>エンティティ イメージ

エンティティをパラメータの 1 つとして含むプラグインのステップを登録すると、<xref:Microsoft.Xrm.Sdk.IExecutionContext.PreEntityImages> および/または <xref:Microsoft.Xrm.Sdk.IExecutionContext.PostEntityImages> プロパティを使用してエンティティ データのコピーを*スナップショット*またはイメージとして含めるように指定するオプションがあります。

このデータは、イベント パイプラインを介して渡されるエンティティ データの比較ポイントを提供します。 これらのイメージを使用すると、プラグインにコードを含めて属性値を比較するだけのエンティティを取得するよりもはるかに優れたパフォーマンスが得られます。

エンティティ イメージを定義するには、固有イメージにアクセスするために使用できるエンティティ エイリアス値を指定します。 たとえば、プレ エンティティ イメージをエイリアス「`a`」で定義する場合、次のコードを使用して、`name` 属性値にアクセスすることができます。

```csharp
var oldAccountName = (string)context.PreEntityImages["a"]["name"];
```

詳細: [エンティティ イメージの定義](register-plug-in.md#define-entity-images)

### <a name="see-also"></a>関連項目

[イベント フレームワーク](event-framework.md)  
[プラグインを記述する](write-plug-in.md)