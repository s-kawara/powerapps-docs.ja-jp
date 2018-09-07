---
title: キャンバス アプリでフローを開始する | Microsoft Docs
description: ユーザーによるボタンの選択などのイベントがキャンバス アプリで発生した後に 1 つ以上のタスクを実行するフローを作成します。
author: stepsic-microsoft-com
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: anneta
ms.date: 06/05/2017
ms.author: sharik
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 05d633b20038ad61215a8e898b1ec7afa044b574
ms.sourcegitcommit: 429b83aaa5a91d5868e1fbc169bed1bac0c709ea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/24/2018
ms.locfileid: "42840771"
---
# <a name="start-a-flow-in-a-canvas-app"></a>キャンバス アプリでフローを開始する

Microsoft Flow を使用すると、キャンバス アプリでイベントが発生したときに 1 つ以上のタスクを実行するロジックを作成できます。 たとえば、ユーザーが選択したときに、SharePoint リストのアイテムの作成、電子メールまたは会議出席依頼の送信、クラウドへのファイルの追加、またはこれらのすべての処理を実行するようにボタンを構成できます。 アプリ内の任意のコントロールは、フローを開始するように構成できます。フローは、PowerApps を閉じた後でも実行し続けます。

## <a name="prerequisites"></a>前提条件

* PowerApps に[サインアップ](../signup-for-powerapps.md)。
* [コントロールを構成する](add-configure-controls.md)方法を確認しておきます。

## <a name="create-a-flow"></a>フローの作成

1. [powerapps.com](http://web.powerapps.com?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc) にサインインし、左側のナビゲーション バーで **[フロー]** を選択します。

2. **[マイ フロー]** ページで、**[一から作成]** を選択します。

    ![テンプレートを使用せずにフローを作成するオプション](./media/using-logic-flows/create-from-blank.png)

    **PowerApps** が既定のトリガーとして追加されます。

    ![フローを開始するトリガーとしての PowerApps](./media/using-logic-flows/set-trigger.png)

3. **[新しいステップ]** を選択し、**[アクションの追加]** を選択します。

    ![アクションを追加するオプション](./media/using-logic-flows/add-action.png)

4. **[すべてのサービスとアクションを検索する]** ボックスで、次の例のようにフローのアクションを指定します。

   1. ボックスに「**SharePoint**」と入力し、**[アクション]** の下の一覧の **[SharePoint - 項目の作成]** を選択します。

       ![SharePoint 項目を作成するオプション](./media/using-logic-flows/create-sharepoint-item.png)

   2. ダイアログが表示されたら、SharePoint に接続するための資格情報を指定します。

   3. **[Site Address]\(サイトのアドレス\)** ボックスに、リストを含む SharePoint Online サイトの URL を入力するか貼り付けます。

       > [!NOTE]
      > リストを除いたサイトの URL を指定してください。

   4. **[リスト名]** ボックスで、使用するリストを選択します。

   5. **[タイトル]** ボックスをクリックまたはタップし、**[動的なコンテンツの追加]** を選択します。

       ![[タイトル] フィールドに [PowerApps で確認] パラメーターを追加する](./media/using-logic-flows/ask-in-powerapps.png)

   6. パラメーターの一覧で、**[PowerApps で確認]** を選択します。

       ![パラメーターを追加する](./media/using-logic-flows/add-parameter.png)

5. (省略可) 指定したアドレスに承認のメールを送信したり、別のデータ ソースに関連するエントリを作成するなど、1 つ以上の追加アクションを指定します。

6. 画面上部で、フローの名前を入力するか貼り付けて、**[フローの作成]** を選択します。

    ![フローに名前を付けて保存する](./media/using-logic-flows/name-flow.png)

## <a name="add-a-flow-to-an-app"></a>アプリへのフローの追加
1. PowerApps で **[ファイル]** メニューの **[新規]** を選択します。

2. **[空のアプリ]** タイルで、**[携帯電話レイアウト]** を選択します。

3. **[テキスト入力](controls/control-text-input.md)** コントロールを追加し、**RecordTitle** という名前を付けます。

4. **[ボタン](controls/control-button.md)** コントロールを追加し、**RecordTitle** の下に移動します。

5. **[ボタン](controls/control-button.md)** コントロールを選択した状態で、**[アクション]** タブの **[フロー]** を選択します。

    ![[アクション] タブの [フロー] オプション](./media/using-logic-flows/action-tab.png)

6. 表示されたウィンドウで、前の手順で作成したフローを選択します。

    > [!NOTE]
   > 作成したフローが選べない場合は、フローを作成した環境に PowerApps が設定されているかどうかを確認します。

    ![カスタマイズ ウィンドウからフローを追加する](./media/using-logic-flows/add-flow-from-pane.png)

7. 数式バーで、自動的に追加された数式の末尾に「**RecordTitle.Text)**」と入力するか貼り付けます。

    ![フローを含む OnSelect プロパティ](./media/using-logic-flows/onselect-with-flow.png)

## <a name="test-the-flow"></a>フローのテスト
1. F5 キーを押して (または右上隅の矢印を選択して) プレビューを開きます。

    ![フローを含む OnSelect プロパティ](./media/using-logic-flows/open-preview.png)

2. **RecordTitle** にテキストを入力するか貼り付けて、**[ボタン](controls/control-button.md)** コントロールをクリックまたはタップします。

    指定したリストに、タイトルとして指定したテキストを含む SharePoint アイテムが作成されます。 フローの実行時にリストが開いていたときは、変更内容を表示するためにブラウザー ウィンドウを更新することが必要な場合があります。
