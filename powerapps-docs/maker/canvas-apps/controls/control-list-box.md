---
title: 'リスト ボックス コントロール: リファレンス | Microsoft Docs'
description: 各種プロパティとサンプルを含む、リスト ボックス コントロールに関する情報です
author: fikaradz
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: tapanm
ms.date: 10/25/2016
ms.author: fikaradz
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 4b12bb62011e24e2dfdb12d9d355432aa2bcadb6
ms.sourcegitcommit: 7dae19a44247ef6aad4c718fdc7c68d298b0a1f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2019
ms.locfileid: "71986573"
---
# <a name="list-box-control-in-powerapps"></a>PowerApps のリスト ボックス コントロール
ユーザーが 1 つまたは複数の項目を選択できるリストです。

## <a name="description"></a>説明
**リスト ボックス** コントロールは、使用可能なすべての選択肢が常に表示されており ( **[ドロップ ダウン](control-drop-down.md)** コントロールと異なる点)、ユーザーは一度に複数の項目を選択できます ( **[ラジオ](control-radio.md)** コントロールと異なる点)。

## <a name="key-properties"></a>主要なプロパティ
**[Default](properties-core.md)** – ユーザーが変更する前のコントロールの初期値です。

**[Items](properties-core.md)** – ギャラリー、リスト、グラフなどのコントロールに表示されるデータのソースです。

**Selected** –選択された項目を表すデータレコード。

ギャラリー、リスト、またはグラフを追加すると、既定ではプロパティの一覧に**項目**が表示されます。新しいコントロールに表示されるデータを簡単に指定できます。 たとえば、ギャラリーの **Items** プロパティは、Salesforce の **Account** テーブルや、Excel で作成してクラウドにアップロードした **在庫管理** という名前の表や、**カンファレンスの講師**と名前をつけた SharePoint リストなどに設定できます。

## <a name="additional-properties"></a>その他のプロパティ
**[AccessibleLabel](properties-accessibility.md)** – スクリーン リーダー用のラベルです。

**[BorderColor](properties-color-border.md)** – コントロールの境界線の色です。

**[BorderStyle](properties-color-border.md)** – コントロールの境界線を **Solid** (実線)、**Dashed** (破線)、**Dotted** (点線)、**None** (なし) のいずれに指定します。

**[BorderThickness](properties-color-border.md)** – コントロールの境界線の太さです。

**[Color](properties-color-border.md)** – コントロールのテキストの色です。

**[DisplayMode](properties-core.md)** – コントロールで、ユーザー入力を許可するか (**Edit**)、データの表示のみを許可するか (**View**)、許可しないか (**Disabled**) を設定します。

**[DisabledBorderColor](properties-color-border.md)** – コントロールの **[DisplayMode](properties-core.md)** プロパティが **Disabled** に設定されている場合のコントロールの境界線の色です。

**[DisabledColor](properties-color-border.md)** – コントロールの **[DisplayMode](properties-core.md)** プロパティが **Disabled** に設定されている場合のコントロール内のテキストの色です。

**[DisabledFill](properties-color-border.md)** – コントロールの **[DisplayMode](properties-core.md)** プロパティが **Disabled** に設定されている場合のコントロールの背景色です。

**[Fill](properties-color-border.md)** – コントロールの背景色です。

**[FocusedBorderColor](properties-color-border.md)** – コントロールにフォーカスがあるときのコントロールの境界線の色です。

**[FocusedBorderThickness](properties-color-border.md)** – コントロールにフォーカスがあるときのコントロールの境界線の太さです。

**[Font](properties-text.md)** – テキストを表記するフォントのファミリー名です。

**[FontWeight](properties-text.md)** –コントロール内のテキストの重み:**Bold**、 **Semibold**、 **Normal**、または**淡い**。

**[Height](properties-size-location.md)** – コントロールの上端と下端の距離です。

**[HoverBorderColor](properties-color-border.md)** – コントロール上にユーザーがマウス ポインターを重ねているときのコントロールの境界線の色です。

**[HoverColor](properties-color-border.md)** – コントロールにユーザーがマウス ポインターを重ねているときのコントロール内のテキストの色です。

**[HoverFill](properties-color-border.md)** – コントロールにユーザーがマウス ポインターを重ねているときのコントロールの背景色です。

**[Italic](properties-text.md)** – コントロール内のテキストを斜体にするかどうかを指定します。

**ItemPaddingLeft** – リスト ボックス内のテキストと左端の間の距離です。

**[LineHeight](properties-text.md)** – テキストの行間やリスト内の項目間などの距離です。

**[OnChange](properties-core.md)** – ユーザーが (スライダーを調整するなどして) コントロールの値を変更した場合のアプリの反応を指定します。

**[OnSelect](properties-core.md)** – ユーザーがコントロールをタップまたはクリックした場合のアプリの反応を指定します。

**[PaddingBottom](properties-size-location.md)** – コントロール内のテキストとそのコントロールの下端間の距離です。

**[PaddingLeft](properties-size-location.md)** – コントロール内のテキストとそのコントロールの左端間の距離です。

**[PaddingRight](properties-size-location.md)** – コントロール内のテキストとそのコントロールの右端間の距離です。

**[PaddingTop](properties-size-location.md)** – コントロール内のテキストとそのコントロールの上端間の距離です。

**[PressedBorderColor](properties-color-border.md)** – コントロールをユーザーがタップまたはクリックしたときのコントロールの境界線の色です。

**[PressedColor](properties-color-border.md)** – コントロールをユーザーがタップまたはクリックしたときのコントロール内のテキストの色です。

**[PressedFill](properties-color-border.md)** – コントロールをユーザーがタップまたはクリックしたときのコントロールの背景色です。

**[Reset](properties-core.md)** – コントロールを既定値に戻すかどうかを指定します。

**Selectedtext (非推奨)** –選択された項目を表す文字列値。

**[SelectionColor](properties-color-border.md)** – リスト内で選択された項目のテキストの色、またはペン コントロールの選択ツールの色です。

**[SelectionFill](properties-color-border.md)** – リストで選択された項目またはペン コントロールの選択領域の背景色です。

**SelectMultiple** – ユーザーがリスト ボックスの複数の項目を選択できるかどうかを指定します。

**[Size](properties-text.md)** – コントロールに表示されるテキストのフォント サイズです。

**[Strikethrough](properties-text.md)** – コントロールに表示されるテキストに取り消し線を付けるかどうかを指定します。

**[TabIndex](properties-accessibility.md)** – 他のコントロールに関連するキーボード ナビゲーションの順序です。

**[Tooltip](properties-core.md)** – ポインターをコントロールに合わせたときに表示される説明テキストです。

**[Underline](properties-text.md)** – コントロールに表示されるテキストの下に線を引くかどうかを指定します。

**[Visible](properties-core.md)** – コントロールを表示するか非表示にするかを指定します。

**[Width](properties-size-location.md)** – コントロールの左端と右端の間の距離です。

**[X](properties-size-location.md)** – コントロールの左端とその親コンテナー (親コンテナーがない場合は画面) の左端間の距離です。

**[Y](properties-size-location.md)** – コントロールの上端とその親コンテナー (親コンテナーがない場合は画面) の上端間の距離です。

## <a name="related-functions"></a>関連する関数
[**Distinct**( *DataSource*, *ColumnName* )](../functions/function-distinct.md)

## <a name="example"></a>例
1. **リスト ボックス** コントロールを追加して **CategoryList** という名前を付け、 **[Items](properties-core.md)** プロパティを次の式に設定します。<br>
   **["Carpet","Hardwood","Tile"]**
   
    [コントロールの追加、命名、構成についてはこちらをご覧ください](../add-configure-controls.md)。
   
    ![リスト ボックス内の床のカテゴリ](./media/control-list-box/category-listbox.png)
2. 3 つの **[ドロップ ダウン](control-drop-down.md)** コントロールを追加し、**CategoryList** の下に移動して、**CarpetList**、**HardwoodList**、**TileList** という名前を付けます。
3. 各 **[ドロップ ダウン](control-drop-down.md)** コントロールの **[Items](properties-core.md)** プロパティに、次の値の 1 つを設定します。
   
   * CarpetList: **["Caserta Stone Beige","Ageless Beauty Clay", "Lush II Tundra"]**
   * HardwoodList: **["Golden Teak","Natural Hickory", "Victoria Mahogany"]**
   * TileList: **["Honey Onyx Marble","Indian Autumn Slate", "Panaria Vitality Ceramic"]**
     
     ![ドロップダウン リストの床の名前](./media/control-list-box/flooring-names.png)
4. 各 **[ドロップ ダウン](control-drop-down.md)** コントロールの **[Visible](properties-core.md)** プロパティに、次の値の 1 つを設定します。
   
   * CarpetList**If (カテゴリ一覧の "カーペット" SelectedItems, true)**
   * HardwoodList**If (カテゴリの一覧の "SelectedItems, true)**
   * TileList**If (カテゴリの一覧の "Tile" SelectedItems, true)**
     
     **[If](../functions/function-if.md)** 関数や[その他の関数](../formula-reference.md)については各関連記事を参照してください。
5. F5 キーを押し、**CategoryList** で 1 つまたは複数の項目を選択します。
   
    選択に基づいて、適切な **[ドロップ ダウン](control-drop-down.md)** コントロールが表示されます。
   
    ![ドロップダウン リストの床の名前](./media/control-list-box/selected-lists.png)
6. (省略可能) Esc キーを押して既定のワークスペースに戻ります。


## <a name="accessibility-guidelines"></a>アクセシビリティのガイドライン
### <a name="color-contrast"></a>色のコントラスト
以下の間には適切な色のコントラストが必要です。
* **SelectionColor** と **SelectionFill**
* **SelectionFill** と **[Fill](properties-color-border.md)**
* **[HoverFill](properties-color-border.md)** と **[Fill](properties-color-border.md)**
* **[PressedFill](properties-color-border.md)** と **[Fill](properties-color-border.md)**

これは、[標準の色のコントラスト要件](../accessible-apps-color.md)に追加されるものです。

### <a name="screen-reader-support"></a>スクリーン リーダーのサポート
* **[AccessibleLabel](properties-accessibility.md)** が存在する必要があります。

### <a name="keyboard-support"></a>キーボードのサポート
* **[TabIndex](properties-accessibility.md)** を 0 以上にして、キーボード ユーザーがそこに移動できるようにする必要があります。
* フォーカス インジケーターは明確に表示する必要があります。 これを実現するには **[FocusedBorderColor](properties-color-border.md)** と **[FocusedBorderThickness](properties-color-border.md)** を使用します。

    > [!NOTE]
  > Tab キーを押すと、**リスト ボックス**に移動またはリスト ボックスから移動します。 方向キーを押すと、**リスト ボックス**の別の内容に移動します。
