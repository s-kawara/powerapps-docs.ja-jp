---
title: 'Power BI タイル コントロール: リファレンス | Microsoft Docs'
description: 各種プロパティとサンプルを含む Power BI のタイル コントロールに関する情報です
author: fikaradz
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: anneta
ms.date: 07/07/2016
ms.author: fikaradz
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: ba7d48104d9fdf85573029cc510af2c29d3f6ca0
ms.sourcegitcommit: 5db6e3ac3a622de313a1102417397e126c3f92f2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/15/2018
ms.locfileid: "45640356"
---
# <a name="power-bi-tile-control-in-powerapps"></a>PowerApps の Power BI タイル コントロール

アプリ内の [Power BI](https://powerbi.microsoft.com) タイルを表示するコントロール。

Power BI をお持ちではありませんか。 [サインアップ](https://docs.microsoft.com/power-bi/service-self-service-signup-for-power-bi)してください。

## <a name="description"></a>説明

アプリ内の **[Power BI タイル](https://docs.microsoft.com/power-bi/service-dashboard-tiles)** を表示して、既存のデータ分析とレポートを活用します。 オプション パネルの **[データ]** タブで **Workspace**、**Dashboard**、**Tile** プロパティを設定して、表示するタイルを指定します。

## <a name="sharing-and-security"></a>共有とセキュリティ

Power BI コンテンツを含むアプリを共有するときは、アプリ自体だけでなく、タイルが表示されている[ダッシュボード](https://docs.microsoft.com/power-bi/service-how-to-collaborate-distribute-dashboards-reports)も共有する必要があります。 そうしないと、アプリを開いたユーザーであっても、Power BI コンテンツは表示されません。 Power BI コンテンツを含むアプリには、そのコンテンツに対するアクセス許可が適用されます。

## <a name="performance"></a>パフォーマンス

アプリ内に同時に 4 つ以上の Power BI タイルを読み込むことは推奨されません。 タイルの読み込みとアンロードは、**LoadPowerBIContent** プロパティを設定することによって制御できます。

## <a name="key-properties"></a>主要なプロパティ

**ワークスペース** – タイルの情報源である Power BI ワークスペース。

**ダッシュボード** – タイルの情報源である Power BI のダッシュボード。

**Tile** – 表示する Power BI のタイルの名前。

**LoadPowerBIContent** – true に設定すると、Power BI コンテンツが読み込まれて表示されます。 false に設定すると、Power BI コンテンツはアンロードされ、メモリが解放されてパフォーマンスが最適化されます。

## <a name="additional-properties"></a>その他のプロパティ

**[BorderColor](properties-color-border.md)** – コントロールの境界線の色です。

**[BorderStyle](properties-color-border.md)** – コントロールの境界線を **Solid** (実線)、**Dashed** (破線)、**Dotted** (点線)、**None** (なし) のいずれに指定します。

**[BorderThickness](properties-color-border.md)** – コントロールの境界線の太さです。

**[DisplayMode](properties-core.md)** – コントロールで、ユーザー入力を許可するか (**Edit**)、データの表示のみを許可するか (**View**)、許可しないか (**Disabled**) を設定します。

**[Height](properties-size-location.md)** – コントロールの上端と下端の距離です。

**[OnSelect](properties-core.md)** – ユーザーがコントロールをタップまたはクリックした場合のアプリの反応を指定します。 既定では、タイルに関連付けられた Power BI レポートが開きます。

**TileUrl** – Power BI サービスからタイルが要求される URL。 URL にパラメーターを追加することで、Power BI タイルに 1 つのパラメーターを渡すことができます (例: … & "&$filter=Town/Province eq '" & ListBox1.Selected.Abbr & "'")。 パラメーターでは等価演算子のみを使用できます。

**[Visible](properties-core.md)** – コントロールを表示するか非表示にするかを指定します。

**[Width](properties-size-location.md)** – コントロールの左端と右端の間の距離です。

**[X](properties-size-location.md)** – コントロールの左端とその親コンテナー (親コンテナーがない場合は画面) の左端間の距離です。

**[Y](properties-size-location.md)** – コントロールの上端とその親コンテナー (親コンテナーがない場合は画面) の上端間の距離です。

## <a name="example"></a>例

1. **[挿入]** タブで **[コントロール]** メニューを開き、**[Power BI タイル]** コントロールを追加します。

    [コントロールの追加および構成](../add-configure-controls.md)についてはこちらをご覧ください。

2. オプション パネルの **[データ]** タブで、**[ワークスペース]** の設定の **[マイ ワークスペース]** をクリックまたはタップします。

3. ダッシュボードの一覧でダッシュボードを選び、タイルの一覧でタイルを選びます。

    コントロールが Power BI タイルを表示します。

## <a name="accessibility-guidelines"></a>アクセシビリティのガイドライン

**Power BI タイル**は、Power BI コンテンツの単なるコンテナーです。 アクセシビリティ対応のコンテンツを作成する方法については、[Power BI のアクセシビリティに関するヒント](https://docs.microsoft.com/power-bi/desktop-accessibility)のページを参照してください。

Power BI コンテンツにタイトルがない場合は、**[ラベル](control-text-box.md)** コントロールを使用して見出しを追加し、スクリーン リーダーをサポートすることを検討してください。 ラベルは、Power BI タイルの直前に配置することができます。
