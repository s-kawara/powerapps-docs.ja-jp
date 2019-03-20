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
ms.openlocfilehash: 798a355e1c8728b41f3e92f183d4a4e2831b7cc2
ms.sourcegitcommit: 90245baddce9d92c3ce85b0537c1ac1cf26bf55a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2019
ms.locfileid: "57799458"
---
# <a name="add-and-configure-a-canvas-app-control-in-powerapps"></a>PowerApps でキャンバス アプリ コントロールを追加および構成する

キャンバス アプリへのさまざまな UI 要素の追加や、要素の外観と動作の構成を、ツールバー、**[プロパティ]** タブ、数式バーなどから直接行います。 これらの UI 要素はコントロールと呼ばれ、構成する内容はプロパティと呼ばれます。

## <a name="prerequisites"></a>前提条件

1. PowerApps のライセンスがまだしていない場合[サインアップ](../signup-for-powerapps.md)、し[サインイン](https://web.powerapps.com?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc)します。
1. **ことを独自のアプリ**、ポインターを合わせる**空白からのキャンバス アプリ**、し、**このアプリの作成**です。
1. クイック ツアーを求められたら、選択**次**、PowerApps インターフェイスの主要な領域に慣れるために (または選択**スキップ**)。

    常に行うツアー後で、画面の右上隅の近くの疑問符アイコンを選択し、選択して**紹介ツアー**します。

## <a name="add-and-select-a-control"></a>追加し、コントロールを選択します。

**挿入** タブで、次の手順のいずれかを実行します。

- 選択**ラベル**または**ボタン**のこれらの種類のコントロールを追加します。
- コントロールのカテゴリを選択し、追加するコントロールの型を選択します。

たとえば、選択**新しい画面**、し、**空白**をアプリに、空の画面を追加します。 (画面とは、その他の種類のコントロールを含むことのできるコントロールの一種です)。

![画面を追加します。](./media/add-configure-controls/add-screen.png)

新しい画面の名前は**Screen2**左側のナビゲーション ウィンドウに表示されます。 このペインでは、アプリでコントロールの階層リストが表示されますを簡単に検索し、各コントロールを選択できます。

![一覧で Screen2](./media/add-configure-controls/list-screen2.png)

この一覧のしくみを示すためには、次のように選択します。**ラベル**上、**挿入**タブ。新しいコントロールのもと**Screen2**階層リストでします。

![一覧で Screen2](./media/add-configure-controls/add-label.png)

画面で、6 つのハンドルを使用して、ボックスには、既定では、ラベルが囲まれます。 その型のボックスには、どのコントロールが選択されているが囲まれます。 画面をクリックしてまたはタップで (ただし、ラベルの外側) を選択した場合、ボックス、ラベルに表示されなくなります。 ラベルを選択させる、もう一度をクリックしてまたはタップし、またはをクリックしてまたはタップ**Label2**コントロールの階層リストでします。

> [!IMPORTANT]
> 構成するには、常にコントロールを選択する必要があります。

## <a name="rename-a-control"></a>コントロールの名前を変更します。

名前を変更するコントロールをポイントし、コントロールの階層リストで選択し、表示される省略記号ボタンを選択します。**の名前を変更**します。 簡単にアプリを構築できるように、覚えやすい一意の名前を入力できます。

![コントロール名の変更](./media/add-configure-controls/rename-control.png)

## <a name="delete-a-control"></a>コントロールを削除します。

削除するコントロールをポイントし、コントロールの階層リストが表示されたら、クリックして、省略記号ボタンを選択します。**削除**します。 画面のないコントロールを削除するをするには、キャンバス上のコントロールを選択して、Del キーを押します。

![コントロールを削除します。](./media/add-configure-controls/delete-control.png)

## <a name="reorder-screens"></a>画面の順序を変更します。

上へ移動またはダウンが表示されたら、省略記号ボタンを選択する画面、コントロールの階層一覧内をポイントし、**上へ移動**または**を下へ移動**します。

![画面の順序を変更します。](./media/add-configure-controls/reorder-screen.png)

> [!NOTE]
> アプリが開かれると、コントロールの階層リストの上部にある画面は、通常最初表示されます。 さまざまな画面を設定して指定できますが、 **[OnStart](controls/control-screen.md)** プロパティが含まれた数式を**[Navigate](functions/function-navigate.md)** 関数。

## <a name="move-and-resize-a-control"></a>移動し、コントロールをサイズ変更

コントロールを移動するには、4 方向の矢印が表示されるように選択し、その中心をポイントし、別の場所にコントロールをドラッグします。

![コントロールを移動します。](./media/add-configure-controls/move-control.png)

コントロールのサイズを変更するには、両方向矢印が表示されるように選択し、選択ボックスでいずれかのハンドルにマウスとハンドルをドラッグします。

![コントロールを移動します。](./media/add-configure-controls/resize-control.png)

> [!NOTE]
> ようにこのトピックの後で説明することができますも移動およびサイズ変更コントロールの任意の組み合わせを変更することでその **[X](controls/properties-size-location.md)**、  **[Y](controls/properties-size-location.md)**、 **[高さ](controls/properties-size-location.md)**、および**[幅](controls/properties-size-location.md)** プロパティ、数式バーにします。

## <a name="change-the-text-of-a-label-or-a-button"></a>ラベルまたはボタンのテキストを変更します。

ラベルやボタンを選択、コントロールに表示されるテキストをダブルクリックし、したいテキストを入力します。

![テキストの変更](./media/add-configure-controls/change-text.png)

> [!NOTE]
> このトピックでは後で説明する、に応じて変更することでこのテキストを変更することもするその**[テキスト](controls/properties-core.md)** 数式バーでのプロパティ。

## <a name="configure-a-control-from-the-toolbar"></a>ツールバーからコントロールを構成する

ツールバーからコントロールを構成することにより、コントロールを直接構成する場合よりも幅広いオプションを指定できます。

たとえば、ラベルを選択、選択、**ホーム**タブをクリックし、ラベルのテキストのフォントを変更します。

![フォントの変更](./media/add-configure-controls/change-font.png)

## <a name="configure-a-control-from-the-properties-tab"></a>[プロパティ] タブでコントロールを構成する

使用して、**プロパティ** タブで、さまざまなオプション、ツールバーからコントロールを構成するよりも指定できます。

たとえば、コントロールを選択して表示し、したり変更することによって非表示にするその**Visible**プロパティ。

![可視性の設定](./media/add-configure-controls/set-visibility.png)

## <a name="configure-a-control-in-the-formula-bar"></a>数式バーでコントロールを構成する

直接、ツールバーで、またはコントロールを構成する代わりに、**プロパティ** タブで、プロパティの一覧でプロパティを選択し、数式バーで値を指定してコントロールを構成できます。 この方法により、プロパティをアルファベット順に検索したり、より多くの種類の値を指定したりできます。

たとえば、ラベルを選択およびし、次のように構成できます。

- 選択して動かします**X**または**Y**プロパティの一覧と、数式バーに別の番号を指定します。

    ![X の設定のプロパティ](./media/add-configure-controls/x-property.png)

- サイズを選択して変更**高さ**または**幅**プロパティの一覧と、数式バーに別の番号を指定します。

    ![高さのプロパティを設定します。](./media/add-configure-controls/height-property.png)

- 選択してそのテキストを変更**テキスト**プロパティの一覧と、数式バーにリテラル文字列、式、または数式の任意の組み合わせを指定します。

    - リテラル文字列は引用符で囲まれているし、入力したとおりに表示されます。 **「こんにちは, world」** はリテラル文字列です。

        ![リテラル文字列 Text プロパティを設定します。](./media/add-configure-controls/literal-string.png)

    - 式は、関数が含まれていないし、別のコントロールのプロパティに基づくことがあります。 **Screen1.Height**の高さを示す式は、 **Screen1**します。

        ![式に Text プロパティを設定します。](./media/add-configure-controls/expression.png)

    - 数式には、1 つまたは複数の関数が含まれています。 **今すぐ**関数、ローカル タイム ゾーンの現在の日付と時刻を返します、**テキスト**関数など、日付、時刻、および通貨の値を書式設定します。

        ![テキスト プロパティを数式に設定します。](./media/add-configure-controls/formula.png)

        数式は、ようにデータを更新、並べ替え、フィルター処理し、およびその他の操作を実行できますが、通常、この例よりもはるかに複雑です。 詳細については、次を参照してください。、[数式のリファレンス](formula-reference.md)します。

## <a name="next-steps"></a>次の手順

- などの一般的なコントロールを構成するための手順を参照[画面](add-screen-context-variables.md)、[一覧](add-list-box-drop-down-list-radio-button.md)、[ギャラリー](add-gallery.md)、[フォーム](add-form.md)、および[グラフ](use-line-pie-bar-chart.md)します。
- コントロールの各種類に関するリファレンス情報を検索、[制御参照](reference-properties.md)します。
