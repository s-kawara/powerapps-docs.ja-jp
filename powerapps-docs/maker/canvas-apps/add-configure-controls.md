---
title: キャンバス アプリ コントロールを追加および構成する | Microsoft Docs
description: ツールバー、[プロパティ] タブ、数式バーなどからキャンバス アプリ コントロールを直接追加および構成するための詳細な手順です。
author: AFTOwen
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: ''
ms.date: 01/25/2019
ms.author: anneta
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 3311433b3950bcf48dc6c7b7969da501e542952c
ms.sourcegitcommit: c52c1869510a9a37d9f7b127e06f07583529588b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2019
ms.locfileid: "64670889"
---
# <a name="add-and-configure-a-canvas-app-control-in-powerapps"></a>PowerApps でキャンバス アプリ コントロールを追加および構成する

キャンバス アプリへのさまざまな UI 要素の追加や、要素の外観と動作の構成を、ツールバー、**[プロパティ]** タブ、数式バーなどから直接行います。 これらの UI 要素はコントロールと呼ばれ、構成する内容はプロパティと呼ばれます。

## <a name="prerequisites"></a>前提条件

1. PowerApps のライセンスをまだお持ちでない場合は、[サインアップ](../signup-for-powerapps.md)してから、[サインイン](https://web.powerapps.com?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc)してください。
1. **自分のアプリを作成する**の下にある**キャンバス アプリを一から作成**にポインターを合わせ、**このアプリの作成**を選択します。
1. クイック ツアーを求められたら、**次**を選択し、 PowerApps インターフェイスの主要な領域に慣れてください (または**スキップ**を選択します)。

    画面の右上隅の近くの疑問符アイコンを選択し、**紹介ツアー**を選択すると、いつでもツアーに参加できます。

## <a name="add-and-select-a-control"></a>コントロールの追加と選択

**挿入** タブで、次の手順のいずれかを実行します。

- これらの種類のコントロールを追加するには、**ラベル** または **ボタン** を選択します。
- コントロールのカテゴリを選択し、追加するコントロールの種類を選択します。

たとえば、**[新しい画面]** を選択し、**[空]** を選択して、アプリに空の画面を追加します。(画面とは、その他の種類のコントロールを含むことのできるコントロールの一種です)。

![画面を追加します。](./media/add-configure-controls/add-screen.png)

新しい画面の名前は **Screen2** で左側のナビゲーション ウィンドウに表示されます。このペインでは、アプリのコントロール階層リストが表示されるので、各コントロールを簡単に検索し、選択することができます。

![一覧で Screen2](./media/add-configure-controls/list-screen2.png)

この一覧のしくみを示すためには、**[挿入]** タブの **[ラベル]** を選択します。新しいコントロールが、階層リストの **[Screen2]** の下に表示されます。

![一覧で Screen2](./media/add-configure-controls/add-label.png)

この画面では、6 つのハンドルを持つボックスがラベルを囲みます。その種類のボックスは、選択されたコントロールを囲みます。画面の内側をクリックまたはタップ (ただし、ラベルの外側) して画面を選択すると、ボックスがラベルに表示されなくなります。ラベルをもう一度選択するには、内側をクリックまたはタップするか、コントロールの階層リストでその名前をクリックまたはタップします。

> [!IMPORTANT]
> 設定する前に、必ずコントロールを選択する必要があります。

## <a name="rename-a-control"></a>コントロールの名前を変更します。

コントロールの階層リストで、名前を変更するコントロールにカーソルを合わせ、表示される省略記号ボタンを選択し、**名前を変更**を選択します。簡単にアプリを構築できるように、覚えやすい一意の名前を入力できます。

![コントロール名の変更](./media/add-configure-controls/rename-control.png)

## <a name="delete-a-control"></a>コントロールを削除します。

コントロールの階層リストで、削除するコントロールにカーソルを合わせ、省略記号ボタンを選択し、**削除**を選択します。画面でないコントロールを削除するには、キャンバス上のコントロールを選択して、Del キーを押すこともできます。

![コントロールを削除します。](./media/add-configure-controls/delete-control.png)

## <a name="reorder-screens"></a>画面の順序を変更します。

コントロールの階層リストで、上下に移動する画面にカーソルを合わせ、省略記号ボタンを選択し、**上へ移動**または**下へ移動**を選択します。

![画面の順序を変更します。](./media/add-configure-controls/reorder-screen.png)

> [!NOTE]
> アプリが開かれると、通常、コントロールの階層リストの最上部にある画面が最初に表示されます。ただし、**[OnStart](controls/control-screen.md)** プロパティで **[Navigate](functions/function-navigate.md)** 関数を含む式を設定することで、別の画面を指定できます。

## <a name="move-and-resize-a-control"></a>コントロールの移動とサイズ変更

コントロールを移動するには、4 方向の矢印が表示されるように選択し、その中心をポイントし、別の場所にコントロールをドラッグします。

![コントロールを移動します。](./media/add-configure-controls/move-control.png)

コントロールのサイズを変更するには、両方向矢印が表示されるように選択し、選択ボックスでいずれかのハンドルにマウスとハンドルをドラッグします。

![コントロールを移動します。](./media/add-configure-controls/resize-control.png)

> [!NOTE]
> このトピックの後で説明するように、数式バーの **[X](controls/properties-size-location.md)**、**[Y](controls/properties-size-location.md)**、**[高さ](controls/properties-size-location.md)**、および**[幅](controls/properties-size-location.md)**プロパティの組合せを変更して、コントロールの移動とサイズを変更することができます。

## <a name="change-the-text-of-a-label-or-a-button"></a>ラベルまたはボタンのテキストを変更します。

ラベルやボタンを選択し、コントロールに表示されるテキストをダブルクリックしてから、変更したいテキストを入力します。

![テキストの変更](./media/add-configure-controls/change-text.png)

> [!NOTE]
> このトピックでは後で説明するように、数式バーの **[テキスト](controls/properties-core.md)** プロパティを変更してテキストを変更することもできます。

## <a name="configure-a-control-from-the-toolbar"></a>ツールバーからコントロールを構成する

ツールバーからコントロールを構成することにより、コントロールを直接構成する場合よりも幅広いオプションを指定できます。

たとえば、ラベルを選択し、**[ホーム]** タブを選択して、ラベル内のテキストのフォントを変更することができます。

![フォントの変更](./media/add-configure-controls/change-font.png)

## <a name="configure-a-control-from-the-properties-tab"></a>[プロパティ] タブでコントロールを構成する

**[プロパティ]** タブを使用すると、ツールバーからコントロールを構成するよりも多くの異なるオプションを指定できます。

たとえば、コントロールを選択してから、**[Visible]** プロパティを変更することによって表示または非表示にできます。

![可視性の設定](./media/add-configure-controls/set-visibility.png)

## <a name="configure-a-control-in-the-formula-bar"></a>数式バーでコントロールを構成する

ツールバーまたは **[プロパティ]** タブで直接コントロールを設定する代わりに、プロパティの一覧でプロパティを選択し、数式バーで値を指定してコントロールを構成できます。この方法により、プロパティをアルファベット順に検索したり、より多くの種類の値を指定したりできます。

たとえば、ラベルを選択およびし、次のように構成できます。

- プロパティ リストで **[X]** または **[Y]** を選択し、数式バーに別の番号を指定して移動します。

    ![X の設定のプロパティ](./media/add-configure-controls/x-property.png)

- プロパティ リストで **[高さ]** または **[幅]** を選択し、数式バーに別の数字を指定してサイズを変更します。

    ![高さのプロパティを設定します。](./media/add-configure-controls/height-property.png)

- プロパティ リストで **[テキスト]** を選択し、数式バーにリテラル文字列、式、または数式の任意の組み合わせを指定してテキストを変更します。

    - リテラル文字列は引用符で囲まれており、入力したとおりに表示されます。「**Hello, world**」はリテラル文字列です。

        ![リテラル文字列 Text プロパティを設定します。](./media/add-configure-controls/literal-string.png)

    - 式には関数は含まれておらず、多くの場合、別のコントロールのプロパティに基づいています。**[Screen1.Height]** は、**[Screen1]** の高さを表す式です。

        ![式に Text プロパティを設定します。](./media/add-configure-controls/expression.png)

    - 数式には、1 つ以上の関数が含まれています。**[Now]** 関数はローカル タイム ゾーンの現在の日付と時刻を返します。**[Text]** 関数は、日付、時刻、および通貨の値を書式設定します。

        ![テキスト プロパティを数式に設定します。](./media/add-configure-controls/formula.png)

        数式は通常、この例よりもはるかに複雑であるため、データの更新、並べ替え、フィルター処理、その他の操作を実行できます。詳細については、[数式のリファレンス](formula-reference.md) を参照してください。

## <a name="next-steps"></a>次の手順

- [画面](add-screen-context-variables.md)、[一覧](add-list-box-drop-down-list-radio-button.md)、[ギャラリー](add-gallery.md)、[フォーム](add-form.md)、および[グラフ](use-line-pie-bar-chart.md)などの一般的なコントロールを設定するための手順を説明します。
- [制御参照](reference-properties.md) で各タイプのコントロールに関する情報を参照します。
