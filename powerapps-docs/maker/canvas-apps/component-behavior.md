---
title: コンポーネントの動作の数式 |Microsoft Docs
description: コンポーネント ベースのアクションが発生したときに、1 つまたは複数のタスクを実行するアプリをトリガーします。
author: yifwang
ms.service: powerapps
ms.topic: article
ms.date: 05/24/2019
ms.author: yifwang
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 7275395a4c21afaebc60e9635461afc08f5e84a0
ms.sourcegitcommit: afe958805d8e1cfa4fdf02c7bceea947185f71f2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/30/2019
ms.locfileid: "66420316"
---
# <a name="behavior-formulas-for-components"></a>コンポーネントの動作の数式

> [!IMPORTANT]
> この機能は、引き続き実験的な既定で無効になります。 詳細については、次を参照してください。[試験的およびプレビュー機能](working-with-experimental.md)します。

1 つ以上指定[動作の数式](working-with-formulas-in-depth.md)イベント コンポーネントのインスタンスの変更をトリガーするときに実行します。 たとえば、コンポーネントを設定**OnReset**値プロパティの初期化を実行、入力のクリアおよびリセットする 1 つまたは複数の数式を**リセット**関数は、コンポーネントのインスタンスで実行します。

## <a name="onreset"></a>OnReset ##

選択したコンポーネントを含む選択**OnReset** (上の右側にある数式バー)、プロパティのドロップダウン リストでし 1 つまたは複数の数式を入力します。

> [!div class="mx-imgBorder"]
> ![OnReset 例](./media/component-behavior/example-onreset.png)

テストする**OnReset**コンポーネントをリセットするコントロールを構成します。 たとえば、設定、 **OnSelect**次の数式に、ボタンのプロパティ。**Reset**(*ComponentName*)

> [!div class="mx-imgBorder"]
> ![[リセット] ボタン](./media/component-behavior/reset-button.png)
