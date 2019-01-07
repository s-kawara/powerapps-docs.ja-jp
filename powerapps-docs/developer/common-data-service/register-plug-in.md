---
title: プラグインの登録 (アプリ用 Common Data Service) | Microsoft Docs
description: プラグインを登録して Common Data Service for Apps にカスタム ビジネス ロジックを適用する方法について説明します。
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

# <a name="register-a-plug-in"></a>プラグインの登録


書き込み、登録、およびプラグインをデバッグするプロセスは次のとおりです:

1. Visual Studio に .NET Framework クラス ライブラリ プロジェクトを作成します。
1. `Microsoft.CrmSdk.CoreAssemblies` NuGet パッケージをプロジェクトに追加します。
1. ステップとして登録されるクラスの <xref:Microsoft.Xrm.Sdk.IPlugin> インターフェイスを実装します。
1. インターフェイスに必要な <xref:Microsoft.Xrm.Sdk.IPlugin.Execute*> メソッドにコードを追加する
    1. 必要なサービスへの参照を取得する
    1. ビジネス ロジックの追加
1. アセンブリにサインし、ビルドする
1. アセンブリをテストする
    1. **テスト環境でアセンブリを登録する**
    1. **アンマネージド ソリューションに、登録されたアセンブリとステップを追加する**
    1. アセンブリの動作をテストする
    1. 想定されたトレース ログが書き込まれたことを確認する
    1. 必要に応じてアセンブリをデバッグする


このトピックの内容は上記**太字**のステップについて説明し、次のチュートリアルをサポートしています。

- [チュートリアル: プラグインを書き込み登録する](tutorial-write-plug-in.md)
- [チュートリアル: プラグインをデバッグする](tutorial-debug-plug-in.md)
- [チュートリアル: プラグインを更新する](tutorial-update-plug-in.md)

## <a name="plugin-registration-tool-prt"></a>Plugin Registration Tool (PRT)

Plugin Registration Tool (PRT) を使用してプラグイン アセンブリと手順を登録します。

PRT は、NuGet からダウンロード可能なツールの 1 つです。 [NuGet からのダウンロード](download-tools-nuget.md)の手順に従います。 そのトピックには、最新の NuGet ツールをダウンロードするために PowerShell スクリプトを使用するための手順が含まれます。

PRT をダウンロードしたら、[チュートリアル: プラグインの作成と登録](tutorial-write-plug-in.md)にある [Plug-in Registration Tool を使用した接続](tutorial-write-plug-in.md#connect-using-the-plug-in-registration-tool)の手順を使用して、CDS for Apps 環境に接続します。

## <a name="register-an-assembly"></a>アセンブリの登録

アセンブリの登録は、CDS for Apps データベースにアセンブリをアップロードするプロセスです。 [チュートリアル: プラグインの作成と登録](tutorial-write-plug-in.md)の[アセンブリの登録](tutorial-write-plug-in.md#register-your-assembly)にある説明を参照してください。

> [!NOTE]
> アセンブリの *分離モード* と *場所* に関連するオプションがあります。 これらは、設置型展開に適用されるオプションを示します。 CDS for Apps は、設置型展開では使用できませんので、これらのオプションの既定のオプション **サンドボックス** および **データベース** を常に使用できます。

アセンブリがアップロードされると、`PluginAssembly` エンティティに格納されます。 プロパティの大半は、インポートされたエンティティのリフレクションを使用して設定されます。 アセンブリの base64 エンコードされたバイトは、`Content` 属性に格納されます。 PRT でアセンブリの **プロパティ** を参照しているときは、**説明** 属性値の編集のみ行うことができます。

### <a name="view-registered-assemblies"></a>登録されたアセンブリの表示

PRT を使用しないでアプリケーション ソリューション エクスプローラーで登録されているアセンブリに関する情報を表示できます。

[!INCLUDE [cc_navigate-solution-from-powerapps-portal](../../includes/cc_navigate-solution-from-powerapps-portal.md)]

> [!NOTE]
> PRT を使用して追加した各アセンブリは、システムの **既定のソリューション** に追加されます (**Common Data Serices の既定のソリューション** と混同しないでください)。 **既定のソリューション** を表示するには、**ソリューション** にある **すべてのソリューション** を選択し、ビューを **すべてのソリューション - 内部** に変更します。
> 
> ソリューションに関する情報の詳細については、[ソリューションの概要](introduction-solutions.md)を参照してください。

![すべてのソリューション (内部)](media/all-solutions-internal-view.png)

ここでは、この環境に登録されているアセンブリすべてを検索できます。

![すべての登録されたアセンブリの表示](media/view-plug-in-assemblies-default-solution.png)

### <a name="query-registered-assemblies-with-code"></a>コードを使用した登録されているアセンブリの照会

PRT またはアプリケーションを使用しないで登録されているアセンブリに関する情報を表示するには、ブラウザーで次の Web API クエリを使用します。

```
[org uri]]/api/data/v9.0/pluginassemblies
?$filter=ishidden/Value eq false
&$select=
createdon,
culture,
customizationlevel,
description,
isolationmode,
major,
minor,
modifiedon,
name,
pluginassemblyid,
publickeytoken,
version
```

または、以下の FetchXml を使用して記述したプログラムで取得します。

```xml
<fetch>
  <entity name='pluginassembly' >
    <attribute name='createdon' />
    <attribute name='culture' />
    <attribute name='customizationlevel' />
    <attribute name='description' />
    <attribute name='isolationmode' />
    <attribute name='major' />
    <attribute name='minor' />
    <attribute name='modifiedon' />
    <attribute name='name' />
    <attribute name='pluginassemblyid' />
    <attribute name='publickeytoken' />
    <attribute name='version' />
    <filter type='and' >
      <filter>
        <condition attribute='ishidden' operator='eq' value='false' />
      </filter>
    </filter>
  </entity>
</fetch>
```
詳細: [FetchXML と FetchExpression の使用](org-service/entity-operations-query-data.md#use-fetchxml-with-fetchexpression)

## <a name="add-your-assembly-to-a-solution"></a>ソリューションへのアセンブリの追加

[登録済みアセンブリの表示](#view-registered-assemblies)で説明されているように、作成したアセンブリ登録はシステムの **既定のソリューション** に追加されています。 アンマネージド ソリューションにアセンブリを追加する必要があるため、他の組織に配布できます。

使用しているアンマネージド ソリューションで、**プラグイン アセンブリ** に移動するためにソリューション エクスプローラー使用します。 リスト メニューで、**既存を追加** を選択します。

![既存のプラグイン アセンブリを追加](media/add-existing-plug-in-assembly.png)

次に、ソリューションにコンポーネントとしてアセンブリを追加します。

![ソリューション コンポーネントとしてプラグイン アセンブリを選択](media/select-plug-in-assembly-as-solution-component.png)

追加したプラグイン アセンブリを選択すると、含まれるプラグイン クラスを参照できます。

![プラグイン アセンブリとクラス](media/view-plug-in-classes-solution-explorer.png)

> [!NOTE]
> 既存またはそれ以降のステップ登録は、プラグイン アセンブリを含むアンマネージド ソリューションに追加されません。 ソリューションに、各登録手順を個別に追加する必要があります。 詳細情報: [ソリューションへのステップの追加](#add-step-to-solution)

## <a name="register-plug-in-step"></a>プラグイン ステップの登録

アセンブリが読み込まれるかアップロードされたら、<xref:Microsoft.Xrm.Sdk.IPlugin> を実装するクラスが PRT で使用可能になります。 [チュートリアル: プラグインの作成と登録](tutorial-write-plug-in.md)にある[新しいステップの登録](tutorial-write-plug-in.md#register-a-new-step)の手順を使用して、新しいステップ登録を作成します。

ステップを登録するとき、イベント パイプラインの段階と、コードが応答するように登録する操作の性質に応じて、使用可能な多くのオプションがあります。

### <a name="general-configuration-information-fields"></a>一般的な構成情報フィールド

|フィールド|説明|
|--|--|
|**メッセージ**|PRT は、システムの使用可能なメッセージ名をオートコンプリートします。 詳細: [メッセージを組織サービスと共に使用する](org-service/use-messages.md)|
|**主エンティティ**|PRT は、選択したメッセージに適用される有効なエンティティをオートコンプリートします。 これらのメッセージには、<xref:Microsoft.Xrm.Sdk.Entity> または <xref:Microsoft.Xrm.Sdk.EntityReference> 型を受け入れる `Target` パラメーターがあります。 有効なエンティティが適用される場合、プラグインを呼び出す回数を制限する場合はこれを設定する必要があります。 <br />`Update`、`Delete`、`Retrieve`、`RetrieveMultiple` などのコア エンティティ メッセージや、このメッセージと共に適用可能なメッセージで空白のままにした場合、このメッセージをサポートするすべてのエンティティでプラグインが呼び出されます。|
|**副エンティティ**|このフィールドは、`Target` パラメーターとしての <xref:Microsoft.Xrm.Sdk.EntityReference> の配列を受け入れた廃止されたメッセージの下位互換性を保つために残されています。 このフィールドは、通常は使用されなくなりました。|
|**フィルタリング属性**|`Update` メッセージを使用して **主エンティティ** を設定すると、フィルタリング属性は、プラグインの実行を、選択した属性が更新プログラムに含まれている場合に制限します。 これはパフォーマンスのベスト プラクティスです。 |
|**イベント ハンドラー**|この値は、アセンブリの名前とプラグイン クラスに基づいて設定されます。 |
|**ステップ名**|ステップの名前。 値は、ステップの構成に基づいて事前設定されますが、この値は変更できます。|
|**ユーザーのコンテキストで実行**|ステップの偽装を適用するためのオプションを提供します。 既定の値は **呼び出し元ユーザー** です。 呼び出し元ユーザーに、ステップで操作を実行する特権がない場合、これらの特権を持つユーザーにこれを設定する必要があります。 詳細: [偽装](write-plug-in.md#impersonation) |
|**実行順序**|同じメッセージの同じステージに対して複数のステップを登録することができます。 このフィールドの数値により、最も小さい数字から最も大きい数字が適用される順序が決定されます。 ステージでプラグインが適用される順序を制御するには、このオプションを編集します。|
|**説明**|ステップの説明です この値は、事前設定されますが、上書きできます。|

> [!NOTE]
> `Update` イベント用に登録されたプラグインを 2 回呼び出すことができるケースがあります。 詳細 : [特化された更新操作の動作](special-update-operation-behavior.md)


### <a name="event-pipeline-stage-of-execution"></a>実行のイベント パイプライン ステージ

プラグインの目的に最適なイベント パイプラインのステージを選択します。

|オプション|説明|
|--|--|
|**事前検証**|[!INCLUDE [cc-prevalidation-description](../../includes/cc-prevalidation-description.md)]|
|**事前操作**|[!INCLUDE [cc-preoperation-description](../../includes/cc-preoperation-description.md)]|
|**PostOperation**|[!INCLUDE [cc-postoperation-description](../../includes/cc-postoperation-description.md)]|

詳細: [イベント実行パイプライン](event-framework.md#event-execution-pipeline)

### <a name="execution-mode"></a>実行モード

非同期実行と同期実行の 2 つのモードがあります。

|オプション|説明|
|--|--|
|**非同期**|操作の完了後に実行するシステム ジョブに、適用するビジネス ロジックの実行コンテキストと定義が移動されます。|
|**同期**|プラグインは、実行の段階および実行順序に応じてすぐに実行されます。 すべての操作全体が、これらが完了するまで待機します。|

非同期プラグインは **PostOperation** ステージでのみ登録することができます。 システム ジョブのしくみの詳細については、[非同期サービス](asynchronous-service.md)を参照してください。

### <a name="deployment"></a>展開

|オプション|説明|
|--|--|
|**サーバー**|プラグインは、アプリ用 CDS サーバーで実行されます。|
|**オフライン**|プラグインは、ユーザーがオフライン モードになると Dynamics 365 for Outlook クライアント内で実行されます。|

<!-- TODO Add link to where more information about offline-plugins will be documented -->

### <a name="set-configuration-data"></a>構成データの設定

**Unsecure Configuration** および **Secure Configuration** フィールドでは、構成データを指定して、特定のステップのプラグインに渡すことができます。

このデータを使用してプラグインがステップでどのように機能するかを制御するために、コンストラクターの文字列値を受け入れるようにプラグインを作成できます。 詳細: [プラグインへの構成データの引き渡し](write-plug-in.md#pass-configuration-data-to-your-plug-in)

### <a name="define-entity-images"></a>エンティティ イメージの定義

プラグイン内では、操作に含まれていなかった主エンティティ プロパティを参照することができます。 たとえば、`Update` 操作では、変更前の値を知ることができますが、実行コンテキストはこの情報を提供しておらず、変更された値のみが含まれます。 

プラグイン ステップが実行パイプラインの **PreValidation** または **PreOperation** 段階に登録されている場合、プロパティの現在の値を取得するために組織サービスを使用することができますが、これはパフォーマンスにとって良い手法ではありません。 より優れたプラクティスは、プラグイン ステップ登録を使用してエンティティ イメージを定義する方法です。 これにより、変更された値と比較するために使用できる操作の前に存在していたとおりに、興味のあるフィールドを含むエンティティの "スナップショット" が取得されます。 

#### <a name="messages-that-support-entity-images"></a>エンティティ イメージをサポートするメッセージ

CDS for Apps では、以下のメッセージだけがエンティティ イメージをサポートしています。

|メッセージ|要求クラス プロパティ| 説明|
|--|--|--|
|`Assign`|`Target`|割り当てられたエンティティ。|
|`Create`|`Target`|作成されたエンティティ。|
|`Delete`|`Target`|削除されたエンティティ。|
|`DeliverIncoming`|`EmailId`|配布された電子メール ID。|
|`DeliverPromote`|`EmailId`|配布された電子メール ID。|
|`Merge`|`Target` または `SubordinateId`|   子エンティティのデータが結合される親エンティティ、または親エンティティに結合される子エンティティ。|
|`Route`|`Target`|転送されるアイテム。|
|`Send`|`FaxId`、`EmailId`、または `TemplateId` |送信されるアイテム。|
|`SetState`|`EntityMoniker`|状態が設定されるエンティティ。|
|`Update`|`Target`|更新されたエンティティ。|


#### <a name="types-of-entity-images"></a>エンティティ イメージの種類

2 種類のエンティティ イメージがあります: **プレ イメージ** および **ポスト イメージ**。 構成すると、これらのイメージがそれぞれ <xref:Microsoft.Xrm.Sdk.IExecutionContext.PreEntityImages> および <xref:Microsoft.Xrm.Sdk.IExecutionContext.PostEntityImages> プロパティとして実行コンテキスト内で使用可能になります。 名前が示すように、これらのスナップショットは、操作の前または操作の後にエンティティがどのような内容かを示しています。 エンティティ イメージを構成すると、`PreEntityImages` または `PostEntityImages` プロパティから特定のエンティティ イメージへのアクセスに使用するキー値となる*エンティティ エイリアス*値を定義します。

#### <a name="availability-of-images"></a>イメージの可用性

エンティティ イメージを構成するとき、登録した手順の段階と操作の種類に応じて使用可能なエンティティ イメージの種類が異なりますことを認識しておく必要ことは重要です。 たとえば、次のようになります。

- エンティティが存在しないため、`Create` メッセージの **プリ イメージ** が存在することはできません。
- エンティティが存在しなくなったため、`Delete` メッセージの **ポスト イメージ** が存在することはできません。
- トランザクションの完了までどのエンティティ プロパティが存在するかを確認する方法がないので、実行パイプラインの **PostOperation** 段階に登録されている手順にのみ**ポスト イメージ**が存在できます。
- **PostOperation** ステージで登録した`Update` 操作については、**プリ イメージ**と**ポスト イメージ**の両方が存在することができます。


#### <a name="add-an-entity-image"></a>エンティティ イメージの追加

[チュートリアル: プラグインの更新](tutorial-update-plug-in.md)の[イメージの追加](tutorial-update-plug-in.md#add-an-image)手順を参照し、エンティティ イメージを追加します。

### <a name="add-step-to-solution"></a>ソリューションへのステップの追加

[ソリューションへのアセンブリの追加](#add-your-assembly-to-a-solution)で説明されているように、**プラグイン アセンブリ**は、アンマネージド ソリューションに追加できるソリューション コンポーネントです。 **SDK メッセージ処理手順**は、ソリューション コンポーネントでもあり、配布する順序でアンマネージド ソリューションに追加する必要もあります。

ソリューションにステップを追加する手順は、アセンブリの追加に似ています。 **既存を追加** コマンドを使用して、目的のアンマネージド ソリューション用に移動します。 唯一異なるのは、ステップを追加するが、ステップで使用するクラスを含むアセンブリをまだ追加していない場合、足りない必要なコンポーネントを追加するように求められることです。

![不足している必須コンポーネント ダイアログ](media/missing-required-component.png)

これが発生した場合は、通常、**OK** を選択し、アンマネージド ソリューションと共にアセンブリを持ち込む必要があります。 これを選択しないのは、アセンブリを含む別のソリューションが既にインストールされている環境にインストールされるようにソリューションが設計されている場合だけです。

同様に、ソリューションでアセンブリを削除してもそれに依存するステップは削除されない点に注意してください。

## <a name="update-an-assembly"></a>アセンブリの更新

前に登録したアセンブリを変更して再構築したら、それを更新する必要があります。 ステップについては、[チュートリアル: プラグインの更新](tutorial-update-plug-in.md)にある[プラグイン アセンブリ登録の更新](tutorial-update-plug-in.md#update-the-plug-in-assembly-registration)ステップを参照してください。

### <a name="assembly-versioning"></a>アセンブリ バージョン管理

展開されたマネージド ソリューションの一部であるプラグイン アセンブリに変更を加える場合、そのマネージド ソリューションを更新した場合に変更が与える可能性がある影響を考慮する必要があります。 アセンブリのバージョンによって動作が制御されます。

Microsoft Visual Studio プロジェクトの `Assembly.info` ファイルで定義されている `major.minor.build.revision` のセマンティック バージョン管理形式を使用して、プラグイン アセンブリのバージョンを管理できます。 新しいソリューションでアセンブリ バージョン番号のどの部分が変更されるかにより、インポートによって既存のソリューションが更新されるときに、次の動作が適用されます。

- **ビルドまたはリビジョンのアセンブリ バージョン番号が変更されます**

  これは一括アップグレードと見なされます。 更新されたアセンブリを含むソリューションがインポートされると、アセンブリの古いバージョンは削除されます。 古いソリューションの既存の手順は、新しいバージョンのアセンブリを参照するように自動的に変更されます。

- **メジャーまたはマイナー アセンブリ バージョン番号が変更されます**

  改訂されたアセンブリを含む更新されたソリューションがインポートされるとき、そのアセンブリは、既存ソリューションに含まれるそのアセンブリの旧バージョンとはまったく異なるアセンブリと見なされます。 既存ソリューション内のプラグイン登録手順では、引き続き古いバージョンのアセンブリが参照されます。 古いアセンブリの既存のプラグイン登録手順で改訂後のアセンブリが参照されるようにするには、プラグイン登録ツールを使用して、改訂後のアセンブリの種類を参照するように手順構成を手動で変更する必要があります。 この作業は、後でインポートするために更新後のアセンブリをソリューションにエクスポートする前に行う必要があります。


## <a name="unregister-or-disable-plug-in-components"></a>プラグイン コンポーネントの登録解除または無効化

プラグイン コンポーネントを登録解除または無効化できます。

### <a name="unregister-components"></a>コンポーネントの登録解除

PRT は、アセンブリ、種類、ステップ、イメージの登録を解除するコマンドを提供します。 手順については、[チュートリアル: プラグインの更新](tutorial-update-plug-in.md)の[アセンブリ、プラグイン、ステップの登録解除](tutorial-update-plug-in.md#unregister-assembly-plug-in-and-step)の手順を参照してください。

[PluginAssembly](reference/entities/pluginassembly.md)、[PluginType](reference/entities/plugintype.md), [SdkMessageProcessingStep](reference/entities/sdkmessageprocessingstep.md)、[SdkMessageProcessingStepImage](reference/entities/sdkmessageprocessingstepimage.md) エンティティには削除操作があります。

ソリューション エクスプローラーで**プラグイン アセンブリ**と **Sdk メッセージ処理ステップ**を削除して、同じ結果を生み出すこともできます。

![ソリューション エクスプローラーでの削除手順](media/delete-sdk-message-processing-step.png)

> [!NOTE]
> **プラグイン アセンブリ**を削除することはできませんが、既存の **Sdk メッセージ処理ステップ**はそれに依存しています。 エンティティ イメージは別々に削除できませんが、それらを使用するステップが削除されると削除されます。

### <a name="disable-steps"></a>ステップの無効化

PRT にはステップを無効化および有効化するコマンドがあります。

![PRT を使用したステップの無効化](media/disable-step-prt.png)

![PRT を使用したステップの有効化](media/enable-step-prt.png)

**アクティブ化** と **非アクティブ化** コマンドを使用して、ソリューション エクスプローラーでステップを無効にすることもできます。

![foo](media/step-activate-deactivate-commands-solution-explorer.png)

## <a name="next-steps"></a>次のステップ

[プラグインのデバッグ](debug-plug-in.md)

### <a name="see-also"></a>関連項目
[ビジネス プロセスを拡張するためのプラグインを記述する](plug-ins.md)<br />
[プラグインを記述する](write-plug-in.md)<br />
[チュートリアル: プラグインを書き込み登録する](tutorial-write-plug-in.md)<br />
[チュートリアル: プラグインをデバッグする](tutorial-debug-plug-in.md)<br />
[チュートリアル: プラグインを更新する](tutorial-update-plug-in.md)<br />
