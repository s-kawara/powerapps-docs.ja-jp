---
title: レポートウィザードを使用してレポートを作成する |Microsoft Docs
description: PowerApps のレポートウィザードを使用してレポートを作成する
author: mduelae
manager: kvivek
ms.service: powerapps
ms.component: pa-user
ms.topic: conceptual
ms.date: 06/27/2019
ms.author: mkaur
ms.custom: ''
ms.reviewer: ''
ms.assetid: ''
search.audienceType:
- enduser
search.app:
- PowerApps
- D365CE
ms.openlocfilehash: 0f953c44d81742baca39058cd68180ca63833eb6
ms.sourcegitcommit: e9671e018c1ee4b640528915350a367758991b6a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2019
ms.locfileid: "67420285"
---
# <a name="create-a-report-using-the-report-wizard"></a>レポート ウィザードを使用してレポートを作成する


レポートウィザードを使用すると、データを簡単に分析できるグラフやテーブルを含むレポートを作成できます。 

レポートウィザードを使用して作成されたすべてのレポートは、フェッチベースのレポートです。 レポートウィザードで生成されたすべてのレポートは、横モードで印刷されることに注意してください。

## <a name="create-a-new-report"></a>新しいレポートを作成する

1. 左側のナビゲーションウィンドウで、[レポート] 領域を選択します。  
2. コマンドバーで **[新規]** を選択します。

    > [!div class="mx-imgBorder"]
    > ![新しいレポートを作成する](media/newreport.png "新しいレポートを作成する")
  
3. **レポート: 新しいレポート**画面が表示されます。 **[レポートの種類]** では、既定の選択をそのままにして、レポート**ウィザードのレポート**を作成し、 **[レポートウィザード]** ボタンを選択します。 

    > [!div class="mx-imgBorder"]
    > ![レポートウィザード](media/report_wizard.png "レポートウィザード画面")
  
4. 次の画面では、既定の選択をそのまま使用し、 **[次へ]** を選択します。
 
    > [!div class="mx-imgBorder"]
    > ![レポートウィザード](media/report_wizard_1.png "レポートウィザード画面")
   
4. **[レポートのプロパティ]** 画面で、レポートの名前を入力し、レポートに含めるレコードを選択して、 **[次へ]** を選択します。
 
    > [!div class="mx-imgBorder"]
    > ![レポートのプロパティ画面](media/report_wizard_2.png "レポートのプロパティ画面")
  
5.  **[レポートに含めるレコードの選択]** 画面で、レポートに含めるレコードを決定するフィルターを選択します。 たとえば、過去60日間に変更されたレコードの結果のみを表示する場合は、この画面でそのフィルターを設定できます。 データがフィルター処理されないようにするには、 **[クリア]** を選択します。

    > [!div class="mx-imgBorder"]
    > ![レポートに含めるレコードを選択します *](media/report_wizard_3.png "レポートに含めるレコードを選択します")
  
6. [**フィールド**のレイアウト] 画面で、レポートのレイアウトを選択します。 [**グループを追加するにはここをクリック**し、データをグループ化する方法を選択します] を選択します。

    > [!div class="mx-imgBorder"]
    > ![レイアウトフィールド](media/report_wizard_4.png "レイアウトフィールド")

7. レポートにグループ化するデータの**レコードの種類**と**列**を選択します。 選択が完了したら、[ **OK]** を選択します。

    > [!div class="mx-imgBorder"]
    > ![dd グループ化画面](media/report_wizard_5.png "グループ化画面の追加")
  
8. 前の手順で選択したレコードの種類に関連するデータ列に**列を追加するに**は、ここをクリックします。  

    > [!div class="mx-imgBorder"]
    > ![グループ化画面の追加](media/report_wizard_6.png "グループ化画面の追加")

9. **[列の追加]** 画面で、列に対して表示するデータを選択し、[ **OK]** を選択します。 

    > [!div class="mx-imgBorder"]
    > [![列の追加] 画面][(media/report_wizard_7.png "列の追加] 画面")
  
10. 追加する追加の列に対して、前の手順を繰り返します。 完了したら、[フィールドの**レイアウト**] 画面で、**次**のようになります。
 
    > [!div class="mx-imgBorder"]
    > [![列の追加] 画面][(media/report_wizard_8.png "列の追加] 画面")
  
11. **[レポートの形式]** 画面で、レポートの書式を設定する方法 を選択し、 **[次へ]** を選択します。
 
    > [!div class="mx-imgBorder"]
    > ![レポートの書式設定](media/report_wizard_9.png "レポートの書式設定画面")

12. レポートの概要を確認し、 **[次へ]** をクリックして、 **[完了]** を選択します。 これで、システムのレポートの一覧にこのレポートが表示されます。

    > [!div class="mx-imgBorder"]
    > ![レポートを表示する](media/report_wizard_10.png "レポートを表示する")

### <a name="see-also"></a>関連項目
[レポートの操作](work-with-reports.md) 

[既存のレポートを追加する](add-existing-report.md)

[レポートフィルターの編集](edit-report-filter.md)

[レポートに表示されていないデータに関する問題のトラブルシューティング](troubleshoot-reports.md)


