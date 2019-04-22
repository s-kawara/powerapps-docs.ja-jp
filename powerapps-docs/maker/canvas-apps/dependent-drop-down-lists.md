---
title: キャンバス アプリでの依存のドロップダウン リストの作成 |Microsoft Docs
description: PowerApps でキャンバス アプリで別のドロップダウン リストをフィルター処理するドロップダウン リストを作成します。
author: emcoope-msft
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: anneta
ms.date: 04/04/2019
ms.author: emcoope
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: dc1b3b87e2c1fdcd4ab7eb6634db7f9e7c049ec2
ms.sourcegitcommit: f84095d964fe1fe5cc5290e5edbee284bd768e1e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/18/2019
ms.locfileid: "59042757"
---
# <a name="create-dependent-drop-down-lists-in-a-canvas-app"></a>キャンバス アプリでの依存のドロップダウン リストを作成します。

依存 (またはカスケード) のドロップダウン リストを作成するときに、ユーザーは、別のリストのフィルター オプションの一覧で、オプションを選択します。 多くの組織では、ユーザーがフォームの記入をより効率的に依存するリストを作成します。 たとえば、国または地域、都市の一覧をフィルター処理する、ユーザーは選択可能性がありますや、ユーザーは、そのカテゴリ内のコードのみを表示するカテゴリを選択可能性があります。

ベスト プラクティスとしては、アプリを使用してユーザーを更新するデータ ソースから別のリスト (たとえば、国/地域と市区町村)、「親」と「子」の値のデータ ソースを作成します。 この方法で実行する場合は、複数のアプリで、同じ親と子のデータを使用することができ、アプリまたはそれらを使用するアプリを再発行しなくてもそのデータを更新することができます。 コレクションまたは静的なデータを使用して、同じ結果を行うことができますが、エンタープライズ シナリオの推奨はありません。

このトピックのシナリオでは、格納する従業員の送信問題、**インシデント**フォームを使用してリスト。 従業員の指定時に、ストアの場所だけでなく、インシデントが発生したもその場所内の部署。 ある同じ部門では、これをしないすべての場所、**場所**リストによって、従業員がその部門がない場所の部門を指定できません。

このトピックでは、データ ソースとして Microsoft SharePoint リストを使用しますが、表形式のデータ ソースのすべての機能は同じです。

## <a name="create-data-sources"></a>データ ソースを作成します。

A**場所**一覧の各場所で部署を示しています。

| Location | Department |
|----------------|------------------|
| Eganville      | パン屋さん           |
| Eganville      | デリ             |
| Eganville      | 生成          |
| Renfrew        | パン屋さん           |
| Renfrew        | デリ             |
| Renfrew        | 生成          |
| Renfrew        | 薬剤         |
| Renfrew        | フローラル           |
| Pembroke       | パン屋さん           |
| Pembroke       | デリ             |
| Pembroke       | 生成          |
| Pembroke       | フローラル           |

**インシデント**一覧には、連絡先情報と各インシデントに関する情報が表示されます。 として日付列を作成、**日付**列として他の列を作成するが、 **1 つの行のテキスト**構成を簡略化およびを避けるのために列[委任](./delegation-overview.md)で警告Microsoft PowerApps。

| 名 | 姓 | 電話番号     | Location | Department | 説明       | Date      |
|------------|-----------|------------------|----------------|------------|-------------------------|-----------|
| Tonya       | Cortez.   | (206) 555 - 1022 | Eganville      | 生成    | 問題がありました。   | 2/12/2019 |
| Moses     | Laflamme     | (425) 555 - 1044 | Renfrew        | フローラル     | ここには、問題が発生しました. | 2/13/2019 |

既定では、カスタム SharePoint リストが含まれて、**タイトル**列の一覧で項目を保存する前にデータを含める必要がありますが、名前を変更または削除することはできません。 データをする必要がないように、列を構成します。

1. 右上隅の近く、歯車アイコンを選択し、選択**設定を一覧表示**します。
1. **設定**] ページで、[**タイトル**列の一覧にします。
1. **情報がこの列に含まれることが必要です。** を選択します**いいえ**します。

無視してその変更を行う、**タイトル**列、またはすることができます[削除](https://support.office.com/article/edit-a-list-column-in-sharepoint-online-77130c2e-76d1-4f80-af8b-4c6f47b264b8)他の少なくとも 1 つの列が表示された場合の既定のビューから。

## <a name="open-the-form"></a>フォームを開きます。

1. 開く、**インシデント**、一覧表示し、 **PowerApps** > **フォームをカスタマイズする**します。

    > [!div class="mx-imgBorder"]
    > ![インシデントの一覧を開き、PowerApps を選択します > フォームをカスタマイズします。](./media/dependent-drop-down-lists/open-form.png "インシデントの一覧を開き、PowerApps を選択します > フォームをカスタマイズします。")

    PowerApps Studio で既定のフォームでブラウザー タブを開きます。

1. (省略可能)**フィールド**ウィンドウで、マウス、**タイトル**フィールドを選択し、表示される省略記号 (...) を選択します。**削除**します。

    閉じている場合、**フィールド**ウィンドウで、開くことができますもう一度選択して**SharePointForm1**で、左側のナビゲーション バーとを選択する**フィールドを編集**で**プロパティ**右側のウィンドウのタブ。

1. (省略可能)削除する前の手順を繰り返して、**添付ファイル**フォームのフィールド。

    フォームに追加したフィールドだけが表示されます。

    > [!div class="mx-imgBorder"]
    > ![タイトルと添付ファイル フィールドのないフォームします。](./media/dependent-drop-down-lists/default-form.png)

## <a name="replace-the-controls"></a>コントロールを置換します。

1. **フィールド**ウィンドウで、横にある矢印を選択します**場所**します。

    閉じている場合、**フィールド**ウィンドウで、開くことができますもう一度選択して**SharePointForm1**で、左側のナビゲーション バーとを選択する**フィールドを編集**で**プロパティ**右側のウィンドウのタブ。

1. 開く、**コントロール型**、一覧表示し、**許可値**します。

    > [!div class="mx-imgBorder"]
    > ![許可される値](./media/dependent-drop-down-lists/change-control.png)

    入力のメカニズムに変更を**ドロップダウン**コントロール。

1. 次の手順を繰り返して、**部門**カード。

## <a name="add-the-locations-list"></a>場所の一覧を追加します。

1. 選択**ビュー** > **データソース** > **データ ソースの追加**します。

1. 選択または SharePoint 接続を作成しを含むサイトを指定、**場所**一覧。

1. その一覧については、チェック ボックスを選択し、選択**Connect**します。

    > [!div class="mx-imgBorder"]
    > ![データ ペイン](./media/dependent-drop-down-lists/select-list.png)

    接続の表示の一覧、**インシデント**一覧、フォームの基になると、**場所**は特定の場所と、フォーム内の部署の一覧。

    > [!div class="mx-imgBorder"]
    > ![SharePoint データ ソース](./media/dependent-drop-down-lists/data-sources.png)

## <a name="unlock-the-cards"></a>カードのロックを解除します。

1. 選択、**場所**カードで、**詳細**右側のウィンドウでタブを選び**プロパティを変更するロックの解除**。

1. 前の手順を繰り返して、**部門**カード。

## <a name="rename-the-controls"></a>コントロールの名前を変更します。

コントロールの名前を変更する場合は、それらをより簡単に特定することができ、例としてはわかりやすくします。 他のベスト プラクティスを検出するには、確認、 [Coding Standards とガイドラインに関するホワイト ペーパー](https://aka.ms/powerappscanvasguidelines)します。

1. **場所**カードの選択、**ドロップダウン**コントロール。

1. 入力または貼り付けることにより、選択したコントロールの名前を変更、右側のウィンドウの上部に近い**ddLocation**します。

    > [!div class="mx-imgBorder"]
    > ![コントロールの名前を変更します。](./media/dependent-drop-down-lists/rename-control.png)

1. 前の 2 つの手順を繰り返して、**部門**カードの名前を変更する、**ドロップダウン**に制御を**ddDepartment**します。

## <a name="configure-the-locations"></a>場所を構成します。

1. 設定、**項目**プロパティの**ddlocation**に次の式。

    `Distinct(Locations, Location)`

1. (省略可能)Alt キーを押したまま、開く**ddLocation**、3 つの場所が一覧に表示されることを確認します。

## <a name="configure-the-departments"></a>部門を構成します。

1. 選択**ddDepartment**、し、**プロパティ**選択の右側のウィンドウのタブ**によって異なります。**

1. **コントロールを親**、いることを確認**ddLocation**上にある一覧に表示されますおよび**結果**下の一覧に表示されます。

    > [!NOTE]
    > 文字列がデータの行の実際の ID と一致しない場合は、選択**ID**の代わりに**結果**します。

1. **照合フィールド**を選択します**場所**上にある一覧で選択**場所**クリックして下の一覧で**適用**します。

    > [!div class="mx-imgBorder"]
    > ![リンクに依存します。](./media/dependent-drop-down-lists/depends-on.png)

    **項目**プロパティの**ddDepartment**次の数式に設定されます。

    `Filter(Locations, Location = ddLocation.Selected.Result)`

    この数式は、項目をフィルター処理**ddDepartment**でユーザーの選択に基づく**ddLocation**します。 このような構成により、部署の「子」リストとして「親」の場所のデータに反映されている、**場所**SharePoint のリストを指定します。

1. **プロパティ**タブ右側のペインの一覧を開き、次に**値**、し、**部門**します。

    この手順からオプションを表示するテキストを設定する、**部門**の列、**場所**SharePoint のリスト。

    > [!div class="mx-imgBorder"]
    > ![部門の値](./media/dependent-drop-down-lists/dept-value.png)

## <a name="test-the-form"></a>フォームをテストします。

開く場所の一覧には、Alt キーを押し、中に選択して、部門の一覧を開きますいずれかを選択します。

場所および部門のリスト内の情報を反映して、**場所**SharePoint のリスト。

> [!div class="mx-imgBorder"]
> ![場所の一覧を開き、Renfrew から Pembroke に、選択範囲を変更して、部門の一覧を開きます](./media/dependent-drop-down-lists/dropdowns.gif)

## <a name="save-and-open-the-form-optional"></a>保存し、(省略可能) のフォームを開きます。

1. 開く、**ファイル**] メニューの [クリックして**保存** > **SharePoint に発行** > **をSharePointに発行**.

1. 左上隅で、戻る矢印を選択し、**[SharePoint に戻る]** を選択します。

1. コマンド バーで **[新規]** を選択し、カスタマイズしたフォームを開きます。

## <a name="faq"></a>FAQ

**すべてのデータを表示できません。 ソースは、すべての空白または間違ったデータがあります。**
これらの方法のいずれかのコントロールに対して適切なフィールドを表示しているかどうかを確認します。

- ドロップダウン リストを選択し、選択、**値**プロパティ、**プロパティ**右側のウィンドウのタブ。

    > [!div class="mx-imgBorder"]
    > ![変更ドロップダウン](./media/dependent-drop-down-lists/drop-down-display-field.png)

- コンボ ボックスを選択し、プライマリ テキストで表示するフィールドであることを確認します。

    > [!div class="mx-imgBorder"]
    > ![変更のコンボ ボックス](./media/dependent-drop-down-lists/combo-box-display-field.png)

**子のドロップダウン リストには、重複した項目が含まれています。**
この現象は、一般的な原因を使用して、**ルックアップ**SharePoint での列または**選択肢**PowerApps の関数。 重複を削除するには、ラップ、 **Distinct**に関するデータを正しく返す関数。 詳細情報:[Distinct 関数](functions/function-distinct.md)します。

## <a name="known-limitations"></a>既知の制限

この構成で使用できる**ドロップダウン**コントロールだけでなく**コンボ ボックス**と**リスト ボックス**一度に 1 つの選択を許可するコントロール。 使用することはできません、**依存**複数選択できるようにする場合、それらのコントロールのいずれかの構成。 このアプローチは、共通のデータ サービスのオプション セットを操作するためお勧めしません。

**依存**構成は、静的データまたはコレクションをサポートしていません。 これらのソースで依存のドロップダウン リストを構成するには、数式バーに直接式を編集します。 さらに、PowerApps をサポートしていない SharePoint の 2 つの選択肢フィールドせず、データの一致するテーブルを使用して、定義することはできません**照合フィールド**この UI 内で。
