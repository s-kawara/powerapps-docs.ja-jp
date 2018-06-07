---
title: Excel でテーブルを書式設定する | Microsoft Docs
description: Excel のデータを使うには、データをテーブルに書式設定する必要があります。 列の名に "image" というキーワードを追加します。
documentationcenter: na
author: yifwang
manager: kfile
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: conceptual
ms.component: canvas
ms.date: 04/03/2018
ms.author: yifwang
ms.openlocfilehash: fd458fe6c8962bbc4443c1de7aad0f1c4eea7fac
ms.sourcegitcommit: 68fc13fdc2c991c499ad6fe9ae1e0f8dab597139
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2018
ms.locfileid: "31826622"
---
# <a name="format-a-table-in-excel-and-naming-tips"></a>Excel でのテーブルの書式設定と名前付けのヒント
Excel のデータをテーブルとして書式設定することは、PowerApps で使うための前提条件です。 このコンテンツに従うことで、Excel でテーブルを書式設定する方法と、Excel で列の名前を付けるときのヒントがわかります。

## <a name="how-to-format-a-table-in-excel"></a>Excel でテーブルの書式を設定する方法
Excel の **[ホーム]** タブの **[テーブルとして書式設定]** をクリックすることで、データをテーブルに変換できます。

![Excel によるテーブルの書式設定](./media/how-to-excel-tips/format-table.png)

書式設定されたテーブルを作成するもう 1 つの方法は、**[挿入]** タブからテーブルとして作成することです。

![Excel によるテーブルの挿入](./media/how-to-excel-tips/insert-table.png)

テーブルを簡単に見つけられるように、**[テーブル ツール]** の **[デザイン]** でテーブルの名前を変更します。 テーブルに意味のある名前を付けておくと便利です。1 つの Excel ファイルに複数のテーブルがある場合は特にそうです。

![Excel によるテーブル名の変更](./media/how-to-excel-tips/rename-table.png)

## <a name="naming-tips-in-excel"></a>Excel での名前付けに関するヒント
Excel のテーブルで、イメージの列に "image" というキーワードを追加してみてください。 このようにすると、イメージ コントロールを含むギャラリーでこのテーブルを使うときに、イメージ列とイメージ コントロールがバインドされます。

![Excel のテーブルとイメージの接続](./media/how-to-excel-tips/connect-gallery.png)

## <a name="next-steps"></a>次の手順
* 指定したテーブルに基づいて、[PowerApps で Excel からアプリケーションを生成](get-started-create-from-data.md)します。 生成されたアプリには、レコードの閲覧用、単一レコードに関する詳細の表示用、レコードの作成/更新用の 3 つの画面が既定で存在します。
* Excel で書式を設定したテーブルを使用して、[アプリを最初から作成](get-started-create-from-blank.md)します。 アプリを手動で作成およびカスタマイズして、表のデータを表示、参照、編集することができます。
