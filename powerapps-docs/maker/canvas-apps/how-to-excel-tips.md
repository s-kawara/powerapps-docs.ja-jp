---
title: Excel でテーブルを書式設定する | Microsoft Docs
description: PowerApps で Excel データを使用するには、データをテーブルとして書式設定する必要があります。 列の名に "image" というキーワードを追加します。
author: yifwang
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: tapanm
ms.date: 04/03/2018
ms.author: yifwang
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 164de5c1b2534901563ab888cfd83641dbe5a9c5
ms.sourcegitcommit: 7dae19a44247ef6aad4c718fdc7c68d298b0a1f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2019
ms.locfileid: "71990030"
---
# <a name="format-a-table-in-excel-and-naming-tips"></a>Excel でのテーブルの書式設定と名前付けのヒント
PowerApps で Excel データに基づいてキャンバス アプリを作成できるのは、Excel データがテーブルとして書式設定されている場合に限られます。 このコンテンツに従うことで、Excel でテーブルを書式設定する方法と、Excel で列の名前を付けるときのヒントがわかります。

## <a name="how-to-format-a-table-in-excel"></a>Excel でテーブルの書式を設定する方法
Excel の **[ホーム]** タブの **[テーブルとして書式設定]** をクリックすることで、データをテーブルに変換できます。

![Excel によるテーブルの書式設定](./media/how-to-excel-tips/format-table.png)

**[挿入]** タブ上で **[テーブル]** を選択してテーブルを作成することもできます。

![Excel によるテーブルの挿入](./media/how-to-excel-tips/insert-table.png)

テーブルを簡単に見つけられるように、 **[テーブル ツール]** の **[デザイン]** でご利用のテーブルの名前を変更します。 テーブルに意味のある名前を付けておくと便利です。同じ Excel ファイルに複数のテーブルがある場合は特にそうです。

![Excel によるテーブル名の変更](./media/how-to-excel-tips/rename-table.png)

## <a name="naming-tips-in-excel"></a>Excel での名前付けに関するヒント
ご利用のテーブル内の列にイメージが含まれている場合は、その列の名前に "image" を含めます。 このキーワードにより、その列はギャラリー内のイメージ コントロールにバインドされます。

![Excel のテーブルとイメージの接続](./media/how-to-excel-tips/connect-gallery.png)

## <a name="next-steps"></a>次の手順
* 指定したテーブルに基づいて、[PowerApps で Excel からアプリケーションを生成](get-started-create-from-data.md)します。 生成されたアプリには、レコードの閲覧用、単一レコードに関する詳細の表示用、レコードの作成/更新用の 3 つの画面が既定で存在します。
* Excel で書式を設定したテーブルを使用して、[アプリを最初から作成](get-started-create-from-blank.md)します。 アプリを手動で作成およびカスタマイズして、表のデータを表示、参照、編集することができます。
