---
title: 'チュートリアル: ワークフロー拡張を作成する (Common Data Service)| Microsoft Docs'
description: このチュートリアルは、ワークフロー デザイナーを拡張してカスタム活動を追加するプロセスおよびワークフロー アセンブリを使用するロジックが示されます
ms.custom: ''
ms.date: 07/16/2019
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
# <a name="tutorial-create-workflow-extension"></a>チュートリアル: ワークフロー拡張の作成

このチュートリアルは、ワークフロー デザイナーを拡張してカスタム活動を追加するプロセスと、ワークフロー アセンブリを使用するロジック (ワークフロー活動と呼ばれることもあります) を示します。 この方法で作成した拡張は、ワークフロー、ユーザー定義アクション、またはダイアログ内で使用できます。

このチュートリアルでは、要件およびプロセスに焦点を当てるために非常に単純な例を以下の目的で使用します。

- Visual Studio クラス ライブラリ プロジェクトの作成
- CodeActivity クラスの追加
- 入力および出力パラメーターの定義
- ビジネス ロジックの追加
- アセンブリのサインとビルド
- アセンブリの登録
- アセンブリをテストする
- ソリューションへのアセンブリの追加

## <a name="prerequisites"></a>前提条件

- Common Data Service インスタンスおよび管理者権限
- ワークフローの構成方法について理解する。 詳細: [クラシックCommon Data Serviceワークフロー](/flow/workflow-processes)
- 取引先企業を編集できるモデル駆動型のアプリケーション。

## <a name="goal"></a>目標

以下の例では、ワークフロー、ダイアログ、またはアクション プロセスで使用可能な簡単なユーザー定義のワークフロー活動を作成します。 詳細: [ワークフロー ステージとステップの構成](/flow/configure-workflow-steps)

このユーザー定義のワークフロー活動は、次の要件を満たします。

1. 10 進数入力パラメーターを受け入れる
1. 入力パラメーター + 10 に等しい値を出力する

**取引先企業** エンティティのワークフローでは、2 つの手順を使用して **利用限度額** 値を大きくするために使用できます。

![このチュートリアルの目標](media/tutorial-create-workflow-activity-goal.png)

手順 1 では、**取引先企業利用限度額** 値を受け入れて、10 ごとに増分するために、 **サンプル: 10 ごとに増分** カスタム ワークフロー活動を使用します。
手順 2 では、値が増分された **取引先企業利用限度額** 値を更新するために、**レコードの更新** 操作を使用します。

### <a name="step-1-get-incremented-account-credit-limit"></a>手順 1: 取引先企業の利用限度額を増分する

最初のステップが追加されたら、ユーザー定義のワークフロー活動が **サンプル** グループで使用可能になり、同じ **10 ごとに増分** が設定されます。

![10 ごとに増分ステップ](media/tutorial-create-workflow-activity-increment-by-10-step.png)

**プロパティの設定** ボタンをクリックして最初のステップを構成するとき、**小数の入力** プロパティが必要になり、**取引先企業** エンティティの **利用限度額** 属性などの 10 進値のみ受け入れます。

![10 進数入力の設定](media/tutorial-create-workflow-activity-step1.png)

### <a name="step-2-set-new-account-credit-limit"></a>手順 2: 新しい取引先企業利用限度額の設定

2 番目の手順では、**レコードの更新** アクションは、増分した値で **取引先企業の利用限度額** 値を更新するために、**取引先企業の利用限度額を増分する** ステップの出力を割り当てます。

![利用限度額の更新](media/tutorial-create-workflow-activity-step2.png)

## <a name="create-a-visual-studio-class-library-project"></a>Visual Studio クラス ライブラリ プロジェクトの作成

このプロジェクトは、10 進数値を 10 ごとに増分するシンプルなワークフロー アセンブリを作成します。

1. Visual Studioを起動します。
1. **ファイル**メニューで**新規**をクリックし、**プロジェクト**をクリックします。
1. *クラス ライブラリ* を検索し、 **クラス ライブラリ (.NET Framework)** を選択します。

    ![クラス ライブラリ (.NET Framework) を検索する](media/create-new-class-library-project.png)

1. **[次へ]** をクリックします。
1. ソリューションの名前と場所を指定します。

    ![Visual Studio 2019に新しいプロジェクト ダイアログを構成します。](media/configure-your-new-project.png)

    > [!NOTE]
    > プロジェクトにわかりやすいプロジェクト名を選択します。 この例では、`SampleWorkflowActivity` が使用されます。

1. **[作成]** をクリックします。
1. **ソリューション エクスプローラー** でプロジェクトを右クリックし、 **プロパティ**を選択します。 **アプリケーション** タブで、  **.NET Framework 4.6.2** が対象のフレームワークとして設定されていることを確認します。

    ![プロジェクト プロパティの設定](media/tutorial-create-workflow-activity-workflow-project.png)

1. **ソリューション エクスプローラー**で、プロジェクトを右クリックして、 **管理 NuGet パッケージ...** を選択します  

    ![NuGet パッケージの管理](media/tutorial-create-workflow-activity-manage-nuget-packages.png)

1. [Microsoft.CrmSdk.Workflow](https://www.nuget.org/packages/Microsoft.CrmSdk.Workflow/)NuGet パッケージを参照し、それをインストールします。

    ![Microsoft.CrmSdk.Workflow NuGet パッケージをインストールします。](media/select-install-microsoft.crmsdk.workflow-nuget-package.png)

    > [!NOTE]
    > インストールするパッケージが [crmsdk](https://www.nuget.org/profiles/crmsdk) により所有されていることを確認します。 必要な `Microsoft.Xrm.Sdk.dll` アセンブリも含まれるように、このパッケージには、`Microsoft.Xrm.Workflow.dll` が含められ、[Microsoft.CrmSdk.CoreAssemblies](https://www.nuget.org/packages/Microsoft.CrmSdk.CoreAssemblies/) パッケージへの依存関係が含まれます。 

1. **ライセンスの承認** ダイアログで **同意する** をクリックする必要があります。

    ![使用許諾契約書に同意する](media/tutorial-create-workflow-activity-license-acceptance.png)

## <a name="rename-the-class-file"></a>クラス ファイルの変更

1. **ソリューション エクスプローラー**で、既定の Class1.cs ファイルを右クリックし、 **名前の変更**を選択します。

    ![Class1.cs ファイルの名称変更](media/rename-class1-file.png)

    > [!NOTE]
    > 活動にわかりやすいクラス名を選択します。 この例では、クラス `IncrementByTen` に名前を付けます。

1. クラス名の変更を確認するダイアログボックスで、 **はい** を選択します。

    ![はい を選択してクラスの名前を変更します。](media/rename-file-dialog.png)

1. IncrementByTen.cs ファイルを開き、次の using ディレクティブを追加します。

    ```csharp
    using System.Activities;
    using Microsoft.Xrm.Sdk;
    using Microsoft.Xrm.Sdk.Workflow;
    ```

1. 次に示すように、クラスが [CodeActivity](/dotnet/api/system.activities.codeactivity) クラスから継承するようにして、パブリック アクセス修飾子を付与します。

    ```csharp
    public class IncrementByTen: CodeActivity
        {

        }
    ```

1. Visual Studio クイック アクションを使用するか手動で、`CodeActivity` クラスから **実行** メソッドを追加します。

    ![CodeActivity インターフェイスの実装](media/tutorial-create-workflow-activity-implement-codeactivity-interface.png)

1. クラスは次のようになりました。

    ```csharp
    public class IncrementByTen : CodeActivity
    {
        protected override void Execute(CodeActivityContext context)
        {
            throw new NotImplementedException();
        }
    }
    ```

## <a name="define-input-and-output-parameters"></a>入力および出力パラメーターの定義

1. 出力パラメーターの値が 10 ごとに増分された入力したパラメーターの値となる一連の入出力パラメーターに関する情報を追加します。

    ```csharp
    public class IncrementByTen : CodeActivity
    {
        [RequiredArgument]
        [Input("Decimal input")]
        public InArgument<decimal> DecInput { get; set; }

        [Output("Decimal output")]
        public OutArgument<decimal> DecOutput { get; set; }

        protected override void Execute(CodeActivityContext context)
        {
            
        }
    }
    ```

    > [!NOTE]
    > アセンブリのパラメーターに関するメタデータを提供するために使用される [.NET 属性](/dotnet/standard/attributes)の使用方法に注目してください。 詳細: [パラメーターの追加](workflow-extensions.md#add-parameters)

## <a name="add-your-business-logic"></a>ビジネス ロジックの追加

10 ごとに入力値を増分するためのロジックを適用するために、Execute メソッド内にロジックを追加します。

```csharp
    protected override void Execute(CodeActivityContext context)
    {
      decimal input = DecInput.Get(context);
      DecOutput.Set(context, input + 10);
    }
```

## <a name="sign-and-build-the-assembly"></a>アセンブリのサインとビルド

1. ユーザー定義のワークフロー活動 (およびプラグイン) のアセンブリに署名が必要です。 プロジェクトプロパティの **署名** タブで、 **アセンブリに署名する** を選択します。 **厳密な名前のキーファイルを選択する**にて、 **&lt;新規...&gt;** オプションを選択します。
    このチュートリアルの目的では、パスワードを設定する必要はありません。 この例では、`SampleWorkflowActivity.snk` という新しい厳密な名前のキーファイルを作成しました。

    ![アセンブリへのサイン](media/tutorial-create-workflow-activity-sign-assembly.png)

1. デバッグ モードでソリューションをビルドし、`SampleWorkflowActivity.dll` アセンブリが `/bin/Debug` フォルダーにあることを確認します。

> [!NOTE]
> アセンブリの開発中は、 **Debug** ビルド構成を使用することができます。 アセンブリを運用サーバーまたはソリューションに展開する際には、 **リリース** ビルド構成を使用する必要があります。

## <a name="register-your-assembly"></a>アセンブリの登録

ユーザー定義のワークフロー活動アセンブリは、プラグイン登録ツールを使用して登録します。 このツールは、グラフィカル ユーザー インターフェイスを提供します。このツールを使用して、プラグインを含むアセンブリまたはユーザー定義のワークフロー活動のアセンブリを登録できます。 プラグイン登録ツールを取得するには、[NuGet からのツールのダウンロード](../download-tools-nuget.md)を参照してください。

[!INCLUDE [cc-connect-plugin-registration-tool](../includes/cc-connect-plugin-registration-tool.md)]

### <a name="register-your-assembly"></a>アセンブリの登録

1. **登録** > **新しいアセンブリの登録**の順に選択します

    ![アセンブリ コマンドの登録](media/tutorial-create-workflow-activity-register-assembly.png)

1. **新しいアセンブリの登録** ダイアログ ボックスで、省略記号ボタン (**...**) をクリックし、`/bin/Debug` フォルダー内の `SampleWorkflowActivity.dll` に移動します。

    ![アセンブリの登録ダイアログ](media/tutorial-create-workflow-activity-register-assembly-dialog.png)

    > [!NOTE]
    > 注意: Common Data Service で手順 3 および 4 に関してのみ使用できるオプションが選択されており、無効なオプションは動作しません。

1. **選択したプラグインの登録**をクリックします。 確認ダイアログが表示されます。

    ![登録済みプラグイン ダイアログ](media/tutorial-create-workflow-activity-register-plug-in-dialog.png)

1. **OK** をクリックして **新しいアセンブリの登録** ダイアログを閉じます。

### <a name="configure-activity-names"></a>アクティビティ名を構成する

1. **登録されたプラグインとユーザー定義ワークフロー活動** のリストで、**(アセンブリ) SampleWorkflowActivity** を見つけ、展開して **(ワークフロー活動) SampleWorkflow.Activity.IncrementByTen - Isolatable** を表示します。
1. **(ワークフロー活動) SampleWorkflow.Activity.IncrementByTen - Isolatable** を選択し、**プロパティ** 領域で、次の表の値を使用して **編集可能なプロパティ** を編集します。

    |編集可能なフィールド|元の値|新しい値|説明|
    |--|--|--|--|
    |説明||入力パラメーターに 10 を加えた値を返します。|プロセス デザイナーの UI に表示されませんが、この情報を格納する PluginType エンティティから取得されたデータからドキュメントを生成するときに便利な場合があります。|
    |FriendlyName|GUID 値|IncrementByTen|プラグインのユーザー フレンドリ名です。|
    |Name|SampleWorkflowActivity.IncrementByTen|10 ごとに増分|表示されたメニューの名前|
    |WorkflowActivityGroupName|SampleWorkflowActivity (1.0.0.0)|サンプル|Common Data Service プロセス デザイナーのメイン メニューに追加されるサブメニューの名前。|

    > [!NOTE]
    > **名前** と **WorkflowActivityGroupName** が null に設定されている場合、ユーザー定義活動はプロセス デザイナーに表示されません。

1. **保存** (アイコン) をクリックして変更を保存します。

    ![ワークフロー活動プロパティを保存する](media/tutorial-create-workflow-activity-set-workflow-activity-properties.png)

## <a name="test-your-assembly"></a>アセンブリをテストする

新しいワークフロー活動を使用するプロセスを作成することでその新しいワークフロー活動をテストできます。 上の[目標](#goal)セクションで説明されているワークフローを作成するためにこれらの手順を使用します。

1. [PowerApps](https://make.powerapps.com/?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc) を開く
1. **ソリューション**を選択します。
1. **CDS 既定の発行者** ソリューションを開きます。
1. メニューで **...** を展開し、 **クラシックに切り替える**を選択します。
    
    ![クラシック ユーザー インターフェイスに切り替える](media/switch-to-classic-solution-ui.png)

1. **コンポーネント** リストで **プロセス** を選択します。
1. **新規作成** を選択し、**プロセスの作成** ダイアログで次を入力します。

    |フィールド|Value|
    |--|--|
    |[プロセス名]|SampleWorkflowActivity.IncrementByTen のテスト|
    |カテゴリ|ワークフロー|
    |エンティティ|取引先企業|
    |[このワークフローをバックグラウンドで実行する (推奨)]|選択解除済み|

    > [!NOTE]
    > **バックグラウンドでこのワークフローを実行する** オプションは、これをリアルタイム (同期) ワークフローにするために選択解除されています。 これにより、テストが簡単になります。

    ![プロセスの作成](media/tutorial-create-workflow-activity-test-activity-process.png)

1. **OK** をクリックします。
1. 以下の変更を適用します。

    |フィールド|Value|
    |--|--|
    |スコープ|組織|
    |開始時期: レコード フィールドの変更|選択済み、ダイアログで指定された `name` フィールド|

    ![テスト ワークフローの構成](media/tutorial-create-workflow-activity-configuration-test-workflow.png)

    > [!NOTE]
    > **スコープ** を **組織** に設定すると、組織内のすべてのユーザーが適用することができるワークフローを作成します。

1. 次の**ステップ**を追加します。

    ![SampleWorkflowActivity.IncrementByTen ステップの追加](media/tutorial-create-workflow-activity-use-sample-step.png)

1. ステップ **説明** を **取引先企業の利用限度額を増分する** に設定し、**プロパティのプロパティ** をクリックします。
1. 既定値 0 を持つ取引先企業利用限度額に **10 進数入力** プロパティの値を設定します。

    ![10 進数入力プロパティを設定する](media/tutorial-create-workflow-activity-configure-first-step.png)

1. **保存して閉じる**をクリックします。
1. **レコードの更新** ステップを追加します

    ![レコードの更新ステップを追加する](media/tutorial-create-workflow-activity-add-update-record-step.png)

1. **プロパティの設定** をクリックし、**取引先企業の利用限度額を増分する** ステップの値に **利用限度額** の値を設定します。

    ![利用限度額の値を設定する](media/tutorial-create-workflow-activity-set-credit-limit.png)

    ワークフロー ステップは、次のように表示されます。

    ![完了したワークフロー](media/tutorial-create-workflow-activity-completed-workflow.png)

1. **保存して閉じる**をクリックします。
1. メニューで **アクティブ化** をクリックし、ワークフローをアクティブ化します...

    ![ワークフローのアクティブ化コマンド](media/tutorial-create-workflow-activity-activate-command.png)

1. **プロセスのアクティブ化の確認** ダイアログで **アクティブ化** をクリックします。

    ![[プロセスのアクティブ化の確認] ダイアログ](media/tutorial-create-workflow-activity-process-activate-confirmation-dialog.png)

1. モデル駆動型のアプリに移動して、取引先企業の一覧を表示します。
1. 取引先企業を選択します。
1. **取引先企業名** フィールドの値を編集します。
1. 取引先企業レコードを保存します。
1. 編集した取引先企業の **利用限度額** 値が 10 増分されたことを確認します。

    ![取引先企業の利用限度額が増分されたことを確認する](media/tutorial-create-workflow-verify-credit-limit.png)

## <a name="add-your-assembly-to-a-solution"></a>ソリューションへのアセンブリの追加

ソリューションのユーザー定義のワークフロー活動を配布するには、それを含む登録されているアセンブリをアンマネージド ソリューションに追加する必要があります。

1. [PowerApps](https://make.powerapps.com/?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc)を使用して、アセンブリを追加する アンマネージド ソリューションを開きます。
1. **既存を追加する** > **その他** > **プラグイン アセンブリ**を選択します

    ![既存のプラグイン アセンブリを追加する](media/add-existing-plugin-assembly.png)

1. プラグイン アセンブリを名前で検索します。この場合は「SampleWorkflowActivity」です。
1. プラグイン アセンブリを選択し、 **追加**を選択します。

### <a name="see-also"></a>関連項目

[ワークフローの拡張機能](workflow-extensions.md)<br />
[サンプル: カスタム ワークフロー活動の作成](sample-create-custom-workflow-activity.md)<br />
[サンプル: ユーザー定義ワークフロー活動を使用した次回の誕生日の更新](sample-update-next-birthday-using-custom-workflow-activity.md)<br />
[サンプル: ユーザー定義ワークフロー活動でクレジット スコアを計算する](sample-calculate-credit-score-custom-workflow-activity.md)