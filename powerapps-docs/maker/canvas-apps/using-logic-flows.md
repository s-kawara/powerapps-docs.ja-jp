---
title: キャンバス アプリでフローを開始する | Microsoft Docs
description: ユーザーによるボタンの選択などのイベントがキャンバス アプリで発生した後に 1 つ以上のタスクを実行するフローを作成します。
author: stepsic-microsoft-com
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: anneta
ms.date: 12/07/2018
ms.author: stepsic
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 5439399a22b47fcf4195cf878208e0e0bd4e0764
ms.sourcegitcommit: 6858f3786e960ca53a400e04734561400dcac5b1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/25/2019
ms.locfileid: "57802586"
---
# <a name="start-a-flow-in-a-canvas-app"></a>キャンバス アプリでフローを開始する

Microsoft Flow を使用すると、キャンバス アプリでイベントが発生したときに 1 つ以上のタスクを実行するロジックを作成できます。 たとえば、ユーザーが選択したときに、SharePoint リストのアイテムの作成、電子メールまたは会議出席依頼の送信、クラウドへのファイルの追加、またはこれらのすべての処理を実行するようにボタンを構成できます。 アプリ内の任意のコントロールは、フローを開始するように構成できます。フローは、PowerApps を閉じた後でも実行し続けます。

> [!NOTE]
> ユーザーがアプリ内からフローを実行するとそのユーザーは、フローで指定されているタスクを実行する権限が必要です。 それ以外の場合、フローは失敗します。

## <a name="prerequisites"></a>前提条件

- PowerApps に[サインアップ](../signup-for-powerapps.md)。
- [コントロールを構成する](add-configure-controls.md)方法を確認しておきます。

## <a name="create-a-flow"></a>フローの作成

1. [PowerApps](http://web.powerapps.com?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc) にサインインします。

1. 左側のナビゲーション バーで、選択**ビジネス ロジック**、し、**フロー**します。

1. 左上隅にある、**自分のフロー**  ページで、**新規**、し、**一から作成**です。

    ![テンプレートを使用せずにフローを作成するオプション](./media/using-logic-flows/create-from-blank.png)

1. 表示されるページの下部には、次のように選択します。**検索数百の接続とトリガー**します。

1. 検索ボックスに「 **PowerApps**、クリックしてして、 **PowerApps**アイコン。

    ![PowerApps のトリガーを作成します。](./media/using-logic-flows/set-trigger.png)
    
1. 次のページには、PowerApps のアイコンを再度選択し、**新しいステップ**します。

1. ボックスをオンに**コネクタとアクションを検索**、この例のように、フローのアクションを指定します。

   1. 型**SharePoint**を選択し、ボックスに**項目の作成**下の一覧で**アクション**します。

       ![SharePoint 項目を作成するオプション](./media/using-logic-flows/create-sharepoint-item.png)

   1. ダイアログが表示されたら、SharePoint に接続するための資格情報を指定します。

   1. **[Site Address]\(サイトのアドレス\)** ボックスに、リストを含む SharePoint Online サイトの URL を入力するか貼り付けます。

       > [!NOTE]
       > リストの名前を URL に追加されません。

   1. **リスト名**ボックスで、使用するリストを指定します。
   
       ![一覧を指定します。](./media/using-logic-flows/list-fields.png)

   1. リストのフィールドの入力ボックスを選択します (など**タイトル**) を選択します**詳細**に動的なコンテンツ ウィンドウで選択し**PowerApps で確認**。 

       ![[タイトル] フィールドに [PowerApps で確認] パラメーターを追加する](./media/using-logic-flows/ask-in-powerapps.png)

1. (省略可能)指定したアドレスに承認メールを送信または別のデータ ソースに関連するエントリを作成するなど、1 つまたは複数の追加手順を指定します。

1. 左上隅の近く入力するか、フローの名前を貼り付けるを選択し、**保存**右上隅の近くです。

## <a name="add-a-flow-to-an-app"></a>アプリへのフローの追加
1. 左側のナビゲーション バーで、選択**作成**です。

1. ポインターを合わせる、**空白からのキャンバス アプリ**タイルをクリックし **このアプリを**します。

1. **[テキスト入力](controls/control-text-input.md)** コントロールを追加し、**RecordTitle** という名前を付けます。

1. **[ボタン](controls/control-button.md)** コントロールを追加し、**RecordTitle** の下に移動します。

1. **[ボタン](controls/control-button.md)** コントロールを選択した状態で、**[アクション]** タブの **[フロー]** を選択します。

    ![[アクション] タブの [フロー] オプション](./media/using-logic-flows/action-tab.png)

1. 表示されたウィンドウで、前の手順で作成したフローを選択します。

    > [!NOTE]
   > 作成したフローが選べない場合は、フローを作成した環境に PowerApps が設定されているかどうかを確認します。

    ![カスタマイズ ウィンドウからフローを追加する](./media/using-logic-flows/add-flow-from-pane.png)

1. 数式バーで、自動的に追加された数式の末尾に「**RecordTitle.Text)**」と入力するか貼り付けます。

    ![フローを含む OnSelect プロパティ](./media/using-logic-flows/onselect-with-flow.png)

## <a name="test-the-flow"></a>フローのテスト
1. ダブルクリックして、**テキスト入力**制御、および入力またはいくつかのテキストを貼り付けます。

1. Alt キーを押しながら選択、 **[ボタン](controls/control-button.md)** コントロール。

    SharePoint のアイテムは、タイトルとして指定したテキストで指定したリストに作成されます。 フローの実行時にリストが開いていたときは、変更内容を表示するためにブラウザー ウィンドウを更新することが必要な場合があります。
