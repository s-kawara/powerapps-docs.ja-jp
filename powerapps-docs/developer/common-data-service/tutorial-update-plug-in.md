---
title: 'チュートリアル: プラグインの更新 (アプリ用 Common Data Service) | Microsoft Docs'
description: 'このチュートリアルでは、プラグインの使用方法を説明するシリーズの 3 番目のチュートリアルです。 '
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
# <a name="tutorial-update-a-plug-in"></a>チュートリアル: プラグインを更新する

このチュートリアルでは、プラグインの使用方法を説明するシリーズの 3 番目のチュートリアルです。 

- [チュートリアル: プラグインを書き込み登録する](tutorial-write-plug-in.md)
- [チュートリアル: プラグインをデバッグする](tutorial-debug-plug-in.md)
- チュートリアル: プラグインを更新する (このチュートリアル)

関連する概念と技術的詳細については、以下を参照してください。

- [ビジネス プロセスを拡張するためのプラグインの使用](plug-ins.md)
- [プラグインを記述する](write-plug-in.md)
- [プラグインの登録](register-plug-in.md)
- [プラグインのデバッグ](debug-plug-in.md)

## <a name="goal"></a>目標

このチュートリアルでは、プラグインで行う追加の一般的な操作について説明します。このチュートリアルでは、以下のことを行います。

 - プラグイン アセンブリを更新する
 - 同期プラグインの作成と登録
 - プラグインで組織データを使用する
 - ユーザーに表示するエラーをスローする
 - コードでプレ エンティティ イメージを設定して使用する
 - アセンブリ、プラグイン、またはステップの登録解除


このチュートリアルの目標は次のとおりです。

- 取引先企業エンティティの更新メッセージの事前検証ステージに登録されている同期プラグインを作成します。 
- プラグインは、プラグインが登録されている場合の組織データを使用して文字列値セットを評価します。 
- 取引先企業の名前がこれらの値の 1 つに変更され、以前の値に新しい名前が含まれていなかった場合は、操作を取り消して、ユーザーにエラー メッセージを戻します。


## <a name="prerequisites"></a>前提条件

- [チュートリアル: プラグインを書き込み登録する](tutorial-write-plug-in.md)を完了する
- [チュートリアル: プラグインをデバッグする](tutorial-debug-plug-in.md)をお勧めしますが、必須ではありません。

> [!NOTE]
> 多くの基本的な手順がは、[チュートリアル: プラグインを作成して登録する](tutorial-write-plug-in.md)で詳しく説明されています。同じレベルの詳細は、このチュートリアルの同じ手順には含まれていません。

## <a name="create-a-new-plug-in-class"></a>新しいプラグイン クラスの作成

1. Visual Studio で、`ValidateAccountName.cs` という名前の **BasicPlugin** プロジェクトに新しいクラスを追加します。
1. 次のコードをクラスに追加して、アセンブリを再作成します。


```csharp
using Microsoft.Xrm.Sdk;
using System;
using System.Collections.Generic;
using System.Linq;

namespace BasicPlugin
{
  public class ValidateAccountName : IPlugin
  {
    //Invalid names from unsecure configuration
    private List<string> invalidNames = new List<string>();

    // Constructor to capture the unsecure configuration
    public ValidateAccountName(string unsecure)
    {
      // Parse the configuration data and set invalidNames
      if (!string.IsNullOrWhiteSpace(unsecure))
        unsecure.Split(',').ToList().ForEach(s =>
        {
          invalidNames.Add(s.Trim());
        });
    }
    public void Execute(IServiceProvider serviceProvider)
    {

      // Obtain the tracing service
      ITracingService tracingService =
      (ITracingService)serviceProvider.GetService(typeof(ITracingService));
      try
      {

        // Obtain the execution context from the service provider.  
        IPluginExecutionContext context = (IPluginExecutionContext)
            serviceProvider.GetService(typeof(IPluginExecutionContext));

        // Verify all the requirements for the step registration
        if (context.InputParameters.Contains("Target") && //Is a message with Target
            context.InputParameters["Target"] is Entity && //Target is an entity
            ((Entity)context.InputParameters["Target"]).LogicalName.Equals("account") && //Target is an account
            ((Entity)context.InputParameters["Target"])["name"] != null && //account name is passed
            context.MessageName.Equals("Update") && //Message is Update
            context.PreEntityImages["a"] != null && //PreEntityImage with alias 'a' included with step
            context.PreEntityImages["a"]["name"] != null) //account name included with PreEntityImage with step
        {
          // Obtain the target entity from the input parameters.  
          var entity = (Entity)context.InputParameters["Target"];
          var newAccountName = (string)entity["name"];
          var oldAccountName = (string)context.PreEntityImages["a"]["name"];

          if (invalidNames.Count > 0)
          {
            tracingService.Trace("ValidateAccountName: Testing for {0} invalid names:", invalidNames.Count);

            if (invalidNames.Contains(newAccountName.ToLower().Trim()))
            {
              tracingService.Trace("ValidateAccountName: new name '{0}' found in invalid names.", newAccountName);

              // Test whether the old name contained the new name
              if (!oldAccountName.ToLower().Contains(newAccountName.ToLower().Trim()))
              {
                tracingService.Trace("ValidateAccountName: new name '{0}' not found in '{1}'.", newAccountName, oldAccountName);

                string message = string.Format("You can't change the name of this account from '{0}' to '{1}'.", oldAccountName, newAccountName);

                throw new InvalidPluginExecutionException(message);
              }

              tracingService.Trace("ValidateAccountName: new name '{0}' found in old name '{1}'.", newAccountName, oldAccountName);
            }

            tracingService.Trace("ValidateAccountName: new name '{0}' not found in invalidNames.", newAccountName);
          }
          else
          {
            tracingService.Trace("ValidateAccountName: No invalid names passed in configuration.");
          }
        }
        else
        {
          tracingService.Trace("ValidateAccountName: The step for this plug-in is not configured correctly.");
        }
      }
      catch (Exception ex)
      {
        tracingService.Trace("BasicPlugin: {0}", ex.ToString());
        throw;
      }
    }
  }
}
```

### <a name="about-the-code"></a>コードについて
- このクラスには、ステップを構成するときに設定されるセキュリティで保護されていない構成を取得するにコンストラクターが含まれます。
- このクラスには、正しく機能するために特定のステップ構成が必要です。
    - 更新メッセージ
    - 取引先企業エンティティで
    - 属性に取引先企業名が含まれている
    - 特定のエイリアス "a" を使用する PreEntityImage
    - 名前属性を含む PreEntityImage
- ステップ構成が正しくない場合は、プラグインは正しく構成されていないトレースにのみ書き込みます
- 有効な名前が組織内で設定されていないと、プラグインは有効な名前が構成に渡されなかったトレースにのみ書き込みます
- 新しい名前が組織を使用する無効な名前のいずれかに一致し、かつ元の名前に新しい名前が含まれない場合、この操作が許可されないユーザーにメッセージと共に <xref:Microsoft.Xrm.Sdk.InvalidPluginExecutionException> がスローされます。

## <a name="update-the-plug-in-assembly-registration"></a>プラグイン アセンブリ登録の更新

[チュートリアル: プラグインを作成して登録する](tutorial-write-plug-in.md)の既存のアセンブリが、既に登録されている必要があります。 既存のアセンブリの登録を解除しないで新しい **ValidateAccountName** プラグインを追加するには、それを更新する必要があります。

1. **(アセンブリ) 基本的なプラグイン** を選択し、**更新** を選択します。

    ![[更新] を選択](media/tutorial-update-plug-in-update.png)

1. **更新アセンブリ: 基本的なプラグイン** ダイアログで、省略記号 (**…**) をクリックしてアセンブリの場所を指定すると、アセンブリが読み込まれます。

    ![更新アセンブリ: 基本的なプラグイン ダイアログ](media/tutorial-update-plug-in-update-assembly.png)

1. アセンブリとの両方のプラグインが選択されていることを確認し、**選択したプラグインの更新** をクリックします。

## <a name="configure-a-new-step"></a>新しい手順の構成

これらの設定を使用して **ValidateAccountName** プラグインを構成します。

|設定|Value|
|--|--|
|メッセージ|Update|
|主エンティティ|取引先企業|
|フィルタリング属性|名前|
|実行のイベント パイプライン ステージ|事前検証|
|実行モード|同期|
|[セキュリティで保護されていない構成]|test、<br />foo、<br />bar|

![新しい手順の登録](media/tutorial-update-plug-in-register-new-step.png)

## <a name="add-an-image"></a>イメージの追加

1. 先ほど登録したステップを右クリックし、**新しいイメージの登録** を選択します。

    ![新しいイメージの登録](media/tutorial-update-plug-in-register-new-image.png)

1. **新しいイメージの登録** ダイアログで、次の設定を持つイメージを構成します。

    |設定|Value|
    |--|--|
    |イメージの種類|プレ イメージ|
    |Name|取引先企業|
    |エンティティ エイリアス|a|
    |パラメーター|名前|

    ![[新しいイメージの登録] ダイアログ](media/tutorial-update-plug-in-register-new-image-dialog.png)

1. イメージを登録すると、プラグイン登録ツールにそれが表示されます。

    ![登録したイメージ](media/tutorial-update-plug-in-image-added.png)

## <a name="test-the-plug-in"></a>プラグインのテスト

1. アプリケーションを開き、既存の取引先企業名を `test`、 `foo`、または `bar` に更新します。
1. 保存しようとすると、次のメッセージが表示されます。

    ![エラー メッセージ](media/tutorial-update-plug-in-error-message.png)

1. `test`、`foo`、`bar` を含む名前を持つ既存の取引先企業を更新した場合、取引先企業を `test`、`foo`、または `bar` に更新するとメッセージが表示されることはありません。

## <a name="unregister-assembly-plug-in-and-step"></a>アセンブリ、プラグイン、ステップの登録解除

プラグイン登録ツールを使用して、アセンブリ、プラグイン、ステップを**登録解除** (削除) します。 アセンブリを削除すると、そのアセンブリのすべてのプラグインと手順が削除されます。

![アセンブリの登録解除](media/tutorial-update-plug-in-unregister.png)
