---
title: キャンバスアプリの PowerApps コンポーネントフレームワーク |Microsoft Docs
description: キャンバスアプリのコードコンポーネントを作成する
keywords: ''
ms.author: nabuthuk
author: Nkrb
manager: kvivek
ms.date: 08/31/2019
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 5d100dc3-bd82-4b45-964c-d90eaebc0735
ms.openlocfilehash: e1c6b4bad1280bdabf8c27e30396b368276ff10b
ms.sourcegitcommit: 2a3430bb1b56dbf6c444afe2b8eecd0e499db0c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2019
ms.locfileid: "72347224"
---
# <a name="powerapps-component-framework-for-canvas-apps"></a>キャンバスアプリ用の PowerApps コンポーネントフレームワーク

> [!IMPORTANT]
> この機能は引き続き試験段階であり、既定では無効になっています。 詳細については、「[試験機能とプレビュー機能](../../maker/canvas-apps/working-with-experimental.md)」を参照してください。

PowerApps component framework を使用すると、アプリの作成者はアプリまたはアプリで使用するコードコンポーネントを作成できます。 詳細情報: [PowerApps component framework の概要](overview.md) 

この実験的なプレビューでは、powerapps component framework により、アプリの開発者は、PowerApps CLI ツールを使用してコードコンポーネントの作成、デバッグ、インポート、キャンバスアプリへの追加を行うことができます。 この実験的なプレビューでは、特定の Api のみがサポートされています。 各 API でキャンバスアプリがサポートされているかどうかを確認することをお勧めします。 

> [!WARNING]
> コードコンポーネントには、Microsoft によって生成されない可能性があり、セキュリティトークンとデータにアクセスできる可能性のあるコードが含まれています。 コードコンポーネントをアプリに追加するときは、コードコンポーネントソリューションが信頼できるソースからのものであることを確認してください。

## <a name="prerequisites"></a>前提条件

環境で PowerApps コンポーネント機能を有効にするには、システム管理者特権が必要です。

> [!IMPORTANT]
> 既定では、PowerApps component framework はモデル駆動型アプリに対して有効になっています。

## <a name="enable-powerapps-component-framework-feature"></a>PowerApps コンポーネントフレームワーク機能の有効化

コードコンポーネントをアプリに追加するには、PowerApps component framework 機能を使用する各環境で有効にする必要があります。 環境でアプリ内のコードコンポーネントを使用できるようにするには、次のようにします。

1. [PowerApps にサインインします](https://powerapps.microsoft.com/en-us/)。

2. **設定**アイコンを選択し、 **[管理センター]** を選択します。
    
    ![設定と管理センター](media/select-admin-center-from-settings.png "の設定と管理センター") 

3. この機能を有効にする環境を選択し、省略記号 ( **..** .) を選択して、 **[設定]** を選択します。

4. **[製品]** タブで、 **[機能]** を選択します。

   Powerapps コンポーネント![フレームワーク]を有効にする(media/enable-pcf-feature.png "powerapps コンポーネントフレームワークを")有効にする

5. 使用可能な機能の一覧から、**キャンバスアプリの PowerApps component framework** の下にある オン を**オン** に設定します。

6. 次に、コードコンポーネントを追加するアプリを開き、[**ファイル** > **アプリの設定**] に移動して **[詳細設定]** を選択します。

   Powerapps コンポーネント![フレームワークのコンポーネントを有効に]する(media/enable-components-for-pcf.png "powerapps component framework のコンポーネントを有効")にする
   
7. **[実験的な機能]** セクションで、 **[コンポーネント]** を **[** オン] に切り替えます。

## <a name="implementing-code-components"></a>実装 (コードコンポーネントを)

環境で PowerApps component framework の機能を有効にした後、コードコンポーネントのロジックの実装を開始できます。 [サンプルコンポーネントの実装](implementing-controls-using-typescript.md)に関するトピックでは、カスタムロジックとマニフェストファイルを実装するコードコンポーネントを作成し、デバッグプロセスを実行し、ソリューションの zip ファイルを作成して、ソリューションを共通にインポートするためのステップバイステップのプロセスを示します。データサービス。

> [!NOTE]
> コードコンポーネントの実装は、モデル駆動型アプリとキャンバスアプリ (試験的プレビュー) の両方で同じです。 唯一の違いは、コードコンポーネントの追加です。 

## <a name="add-components-to-a-canvas-app"></a>キャンバスアプリにコンポーネントを追加する

> [!NOTE]
> モデル駆動型アプリのフィールドまたはエンティティにコードコンポーネントを追加する方法については、「[モデル駆動型アプリへのコードコンポーネントの追加](add-custom-controls-to-a-field-or-entity.md)」を参照してください。

キャンバスアプリにコードコンポーネントを追加するには:

1. PowerApps Studio に移動します。
2. 新しいキャンバスアプリを作成するか、コードコンポーネントを追加する既存のアプリを編集します。

   > [!IMPORTANT]
   > 次の手順に進む前に、ソリューション zip ファイルが既に Common Data Service に[インポート](https://docs.microsoft.com/en-us/powerapps/maker/common-data-service/import-update-export-solutions)されていることを確認してください。

3. **コンポーネントのインポート** > **コンポーネント**の**挿入** >  にアクセスします。 
 
    ![コンポーネント]の挿入コンポーネントの(media/insert-components-import.png "挿入")

4. **[コード (試験段階)]** タブを選択し、一覧からコンポーネントを追加して、 **[インポート]** を選択します。 これにより、 **[コンポーネント]** メニューにサンプルコンポーネントが追加されます。

    ![コンポーネント]の(media/import-component-add-sample-component.png "インポート")サンプルコンポーネントのインポート

5. **コンポーネント**に移動し、コンポーネントを選択してアプリに追加します。

   ![サンプルコンポーネント]の追加(media/add-sample-component-from-list.png "サンプルコンポーネント")の追加

## <a name="delete-a-code-component"></a>コードコンポーネントの削除 

キャンバスアプリからコードコンポーネントを削除するには、削除するコードコンポーネントを選択し、メニューの **[削除]** ボタンを選択します。 コードコンポーネントがアプリから削除されると、すべてのコードコンポーネント要素がアプリとアプリパッケージから削除されます。 

## <a name="update-existing-code-components"></a>既存のコードコンポーネントを更新する

コードコンポーネントを更新すると、マニフェストファイルに*version*属性が指定されるため、最新の変更がランタイムに反映されます。 キャンバスアプリの場合、既存のコードコンポーネントを更新するときに、 *version*属性を更新する必要はありません。 設計上、キャンバスアプリは最新のコードコンポーネントを取得し、実行時に表示します。 キャンバスアプリには、同じコンポーネントの1つのバージョンのみが存在できます。

> [!NOTE]
> 既存のコードコンポーネントが更新されるのは、アプリが PowerApps Studio で閉じられた場合、または開かれていない場合のみです。 アプリを再度開くと、コードコンポーネントを更新するように求められます。 コードコンポーネントを削除したり、コードコンポーネントをアプリに追加し直したりするだけで、コンポーネントは更新されません。

## <a name="see-also"></a>関連項目

[PowerApps コンポーネントフレームワークの概要](overview.md)<br/>
[サンプルコンポーネントの実装](implementing-controls-using-typescript.md)

