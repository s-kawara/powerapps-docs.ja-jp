---
title: 'データ テーブル コントロール: リファレンス | Microsoft Docs'
description: データ テーブル コントロールに関する情報 (各種プロパティとサンプルを含む)
documentationcenter: na
author: jasongre
manager: kfile
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: reference
ms.component: canvas
ms.date: 06/05/2017
ms.author: kfend
ms.openlocfilehash: aa6e778a1c0426c696aaf48c542eccc4887c0e36
ms.sourcegitcommit: 68fc13fdc2c991c499ad6fe9ae1e0f8dab597139
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2018
ms.locfileid: "31836249"
---
# <a name="data-table-control-in-powerapps"></a>PowerApps のデータ テーブル コントロール
データのセットを表形式で表示します。

## <a name="description"></a>説明
**データ テーブル** コントロールには、コントロールに表示される各フィールドの列ヘッダーを含む形式でデータセットが表示されます。 アプリ メーカーとして、表示されるフィールドやその順序を詳細にコントロールできます。 **ギャラリー** コントロールなど、**データ テーブル** コントロールには、選択した行をポイントする **Selected** プロパティが保持されます。 したがって、**データ テーブル** コントロールは他のコントロールにリンクすることできます。

## <a name="capabilities"></a>機能
PowerApps では、2017 年 5 月 5 日に**データ テーブル** コントロールを導入しました。 このセクションでは、サポートされている機能とサポートされていない機能に関する情報を提供します。

### <a name="now-available"></a>提供開始
* **データ テーブル** コントロールの読み取り専用データ。
* **データ テーブル** コントロールで常に単一行を選択。
* **データ テーブル** コントロールの接続されたデータ ソースまたはローカル データ ソースへのリンク。
* 変更を保存していない場合も、アプリの実行中に**データ テーブル** コントロールの列の幅を調整できる。
* Common Data Service など、この機能を実装しているコネクターに既定のフィールドのセットをリンクすると、**データ テーブル** コントロールに表示される。 必要に応じて、これらのフィールドなどを表示または非表示にすることができます。
* 列の幅や見出しのテキストのカスタマイズ。
* **データ テーブル** コントロールでのハイパーリンクの表示。
* **データ テーブル** コントロールのコピーと貼り付け。

### <a name="not-yet-available"></a>現時点では利用不可
* 個別の列のスタイルのカスタマイズ。
* **データ テーブル** コントロールのフォーム コントロールへの追加。
* すべての行の高さの変更。
* **データ テーブル** コントロールでの画像の表示。
* 関連エンティティからのフィールドの表示。
* 組み込み機能を使用した列見出しによるデータのフィルター処理および並べ替え。
* **データ テーブル** コントロールの **ギャラリー** コントロールへの追加。
* **データ テーブル** コントロールでのデータの編集。
* 複数の行の選択。

### <a name="known-issues"></a>既知の問題
* **Items** プロパティに **FirstN** 関数を使用すると、データが表示されません。

## <a name="key-properties"></a>主要なプロパティ
* [**Items**](properties-core.md) – **データ テーブル** コントロールに表示されるデータのソースです。
* **Selected** – **データ テーブル** コントロールで選択された行です。

## <a name="other-properties"></a>その他のプロパティ
* [**BorderColor**](properties-color-border.md) – **データ テーブル** コントロールの境界線の色です。
* [**BorderStyle**](properties-color-border.md) – **データ テーブル** コントロールの境界線のスタイルです。 オプションは、**[実線]**、**[破線]**、**[点線]**、および **[なし]** です。
* [**BorderThickness**](properties-color-border.md) – **データ テーブル** コントロールの境界線の太さです。
* [**Color**](properties-color-border.md) – すべてのデータ行の既定のテキスト色です。
* [**Fill**](properties-color-border.md) – すべてのデータ行の既定の背景色です。
* [**Font**](properties-text.md) – すべてのデータ行の既定のフォントです。
* [**FontWeight**](properties-text.md) – すべてのデータ行の既定のフォントの太さです。
* **HeadingColor** – 列見出しのテキストの色です。
* **HeadingFill** – 列見出しの背景色です。
* **HeadingFont** – 列見出しのフォントです。
* **HeadingFontWeight** – 列見出しのフォントの太さです。
* **HeadingSize** – 列見出しのフォント サイズです。
* [**Height**](properties-size-location.md) – **データ テーブル** コントロールの上端と下端の距離です。
* [**HoverColor**](properties-color-border.md) – マウス ポインターがポイントしている行のテキストの色です。
* [**HoverFill**](properties-color-border.md) – マウス ポインターがポイントしている行の背景色です。
* **NoDataText** – **データ テーブル** コントロールに表示するレコードがないときに、ユーザーが受け取るメッセージです。
* **SelectedColor** – 選択された行のテキストの色です。
* **SelectedFill** – 選択した行の背景色です。
* [**Size**](properties-text.md) – すべてのデータ行の既定のフォント サイズです。
* [**Visible**](properties-core.md) – **データ テーブル** コントロールが表示されるか、それとも非表示になるかを決定する値です。
* [**Width**](properties-size-location.md) – **データ テーブル** コントロールの左端と右端の間の距離です。
* [**X**](properties-size-location.md) – **データ テーブル** コントロールの左端とその親コンテナーの左端 (親コンテナーがない場合は画面の左端) との間の距離です。
* [**Y**](properties-size-location.md) – **データ テーブル** コントロールの上端とその親コンテナーの上端 (親コンテナーがない場合は画面の上端) との間の距離です。

## <a name="related-functions"></a>関連する関数
* [**Filter(DataSource, Formula)**](../functions/function-filter-lookup.md)(*DataSource*, *Formula*)
* [**Search(DataSource, SearchString, Column)**](../functions/function-filter-lookup.md)(*DataSource*, *SearchString*, *Column*)

## <a name="examples"></a>例
### <a name="basic-usage"></a>基本的な使用方法
1. 空白のタブレット アプリを作成します。
2. **[挿入]** タブで、**[データ テーブル]** をクリックまたはタップします。
   
    ![データ テーブル コントロールを画面に追加します](./media/control-data-table/insert-data-table.png)
   
    **データ テーブル** コントロールが画面に追加されます。
3. **データ テーブル** コントロール **SalesOrderTable** の名前を変更し、画面全体をカバーするようにサイズを変更します。
4. 右側のウィンドウで、**[データ ソースが選択されていません]** のテキストの右側にある下矢印をクリックまたはタップしてから、**[データ ソースの追加]** をクリックまたはタップします。
   
    ![データ ソースの追加](./media/control-data-table/add-data-to-data-table.png)
5. 接続の一覧で、Common Data Service データベースの接続をクリックまたはタップします。
   
    ![データ ソースの接続を選択します](./media/control-data-table/choose-cds-data-table.png)
6. エンティティの一覧で、**[販売注文]** をクリックまたはタップしてから、**[接続]** をクリックまたはタップします。
   
    ![Sales order エンティティを選択する](./media/control-data-table/choose-so-data-table.png)
   
    これで、**データ テーブル** コントロールが、**Sales order** データ ソースに接続されます。 その機能をサポートするコネクタを使用しているため、いくつかの初期フィールドが**データ テーブル** コントロールに表示されます。
   
    ![データ テーブル](./media/control-data-table/pre-order-data-table.png)
7. 右側のウィンドウで、1 つ以上のチェック ボックスを選択し、個別のフィールドを表示または非表示にします。
   
    たとえば、**CustomerPurchaseOrderReference** の横にあるチェック ボックスを選択して、このフィールドを非表示にします。
8. 右側のウィンドウで、フィールドを上下にドラッグして、フィールドの順序を変更します。
   
    ![必要に応じてフィールドの順序を変更する](./media/control-data-table/field-re-order-data-table.png)
   
    **SalesOrderTable** コントロールに、指定した順序でフィールドが表示されます。
   
    ![更新後のデータ テーブル](./media/control-data-table/post-order-data-table.png)

### <a name="restyle-the-header-for-the-data-table-control"></a>データ テーブル コントロールのヘッダーのスタイルを変更する
1. **データ テーブル** コントロールが選択されているときに、右側のウィンドウの **[詳細]** タブをクリックまたはタップします。
2. **HeadingFill** プロパティのフィールドをクリックまたはタップし、値を **RGBA(62,96,170,1)** に変更します。
3. **HeadingColor** プロパティのフィールドをクリックまたはタップし、値を **White** に変更します。
4. **HeadingSize** プロパティのフィールドをクリックまたはタップし、値を **14** に変更します。
   
    ![データ テーブル](./media/control-data-table/restyled-data-table.png)

### <a name="connect-a-data-table-control-to-another-control"></a>データ テーブル コントロールを別のコントロールに接続する
1. **編集フォーム** コントロールを画面に追加します。
2. **データ テーブル** コントロールと**編集フォーム** コントロールのサイズを変更して、**データ テーブル** コントロールが画面の左側、**編集フォーム** コントロールが画面の右側の部分に表示されるようにします。
   
    ![同じ画面上に配置されたデータ テーブルと編集フォーム](./media/control-data-table/data-table-empty-form.png)
3. **Form1** が選択されているときに、右側のウィンドウで、列の数を **1** に変更します。
4. **Form1** を **Sales order** データ ソースに接続します。
   
    いくつかの初期フィールドが **Form1** に表示されます。
   
    ![初期フィールドを含む Form1](./media/control-data-table/data-table-disconnected-form.png)
5. 右側のウィンドウで、**[詳細]** タブをクリックまたはタップします。
6. **Form1** の **Item** プロパティを **SalesOrderTable.Selected** に設定します。
   
    **Form1** に、**データ テーブル** コントロールで選択された行の情報が表示されます。
   
    ![データ テーブルに接続さた編集フォーム](./media/control-data-table/connected-form-data-table.png)


## <a name="accessibility-guidelines"></a>アクセシビリティのガイドライン
### <a name="color-contrast"></a>色のコントラスト
以下の間には適切な色のコントラストが必要です。
* [**Color**](properties-color-border.md) と [**Fill**](properties-color-border.md)
* **HeadingColor** と **HeadingFill**
* **SelectedColor** と **SelectedFill**
* [**HoverColor**](properties-color-border.md) と [**HoverFill**](properties-color-border.md)

これは、[標準の色のコントラスト要件](../accessible-apps-color.md)に追加されるものです。

### <a name="screen-reader-support"></a>スクリーン リーダーのサポート
* **NoDataText** を指定する必要があります。
