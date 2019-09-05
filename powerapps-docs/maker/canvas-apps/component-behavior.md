---
title: コンポーネントの動作の数式 |Microsoft Docs
description: コンポーネントベースのアクションが発生したときに1つ以上のタスクを実行するようにアプリをトリガーします。
author: yifwang
ms.service: powerapps
ms.topic: article
ms.date: 05/24/2019
ms.author: yifwang
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: c8ec4edd835f12fb6fccf04ba0fb27f1e755cac0
ms.sourcegitcommit: ea3ab5926541c60a9e7c17f52f937c9812d48c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/05/2019
ms.locfileid: "70310052"
---
# <a name="behavior-formulas-for-components"></a>コンポーネントの動作に関する数式

> [!IMPORTANT]
> この機能は引き続き試験段階であり、既定では無効になっています。 詳細については、「[試験機能とプレビュー機能](working-with-experimental.md)」を参照してください。

イベントによってコンポーネントインスタンスの変更がトリガーされたときに実行される1つまたは複数の[動作の数式](working-with-formulas-in-depth.md)を指定します。 たとえば、コンポーネントの**onreset**プロパティを、コンポーネントインスタンスで**reset**関数を実行したときに、初期化を実行し、入力をクリアし、値をリセットする1つ以上の数式に設定します。

## <a name="onreset"></a>OnReset

コンポーネントを選択した状態で、プロパティのドロップダウンリスト (数式バーの右側) で **[Onreset]** を選択し、1つまたは複数の数式を入力します。

> [!div class="mx-imgBorder"]
> ![OnReset の例](./media/component-behavior/example-onreset.png)

**Onreset**をテストするには、コンポーネントをリセットするようにコントロールを構成します。 たとえば、ボタンの**Onselect**プロパティを次の数式に設定します。**リセット**(*ComponentName*)

> [!div class="mx-imgBorder"]
> ![[リセット] ボタン](./media/component-behavior/reset-button.png)
