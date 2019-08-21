---
title: レポートの操作 |Microsoft Docs
description: PowerApps でのレポートの操作
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
ms.openlocfilehash: f4647c565b2ecaf469c3b74873ba157ea27a1fd4
ms.sourcegitcommit: 982cab99d84663656a8f73d48c6fae03e7517321
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/28/2019
ms.locfileid: "67457044"
---
# <a name="work-with-reports"></a>レポートを操作する

レポートは、ビジネス目標に対する進行状況を監視するのに役立ちます。 また、傾向を追跡することもできます。これにより、競合他社の恩恵を得ることができます。  

レポートの整理と作成の詳細については、以下を参照してください。[レポートをカスタマイズおよび整理](https://docs.microsoft.com/powerapps/maker/model-driven-apps/add-reporting-to-app)する。
  
## <a name="run-a-report"></a>レポートを実行する  
  
1. 左側のナビゲーションウィンドウで、[レポート] 領域を選択します。 
2. **レポートを実行**> するレポートを選択します。  
  
   > [!NOTE]
   >  **[レポートビューアー]** ダイアログボックスでは、検索条件をそのままにしたり、必要に応じて変更したりできます。  
   
   > [!div class="mx-imgBorder"]
   > ![レポートを実行する](media/report-run.png "レポートを実行する")
 
  
## <a name="share-a-report-with-other-users-or-teams"></a>他のユーザーまたはチームとレポートを共有する    

1. 左側のナビゲーションウィンドウで、[レポート] 領域を選択します。  
2. レポートの一覧で、共有するレポートを選択します。  
3. コマンドバーで **[共有]** を選択します。

   > [!div class="mx-imgBorder"]
   > ![レポートを共有する](media/report-share.png "レポートを共有する")
  
4. **[レポートの共有]** ダイアログボックスで、 **[ユーザー/チームの追加]** を選択します。    
5. **[レコードの参照]** ダイアログボックスで、レポートを共有するユーザーまたはチームレコードを探し、レコードの横にあるチェックボックスをオンにします。

   > [!div class="mx-imgBorder"]
   > ![レポートを共有するユーザーの選択](media/report-share1.png "レポートを共有するユーザーを選択し")ます

6. **[選択]** をクリックして、選択し **[たレコード]** ボックスにユーザーまたはチームのレコードを追加し、 **[追加]** を選択します。

   > [!div class="mx-imgBorder"]
   > ![レポートを共有するためのユーザーの追加](media/report-share2.png "ユーザーを追加してレポートを共有する")
  
7. **[レポートの共有]** ダイアログボックスで、必要な共有アクセスの種類を選択します。 使用できるアクセス許可は次のとおりです。読み取り、書き込み、削除、追加、割り当て、または共有。 これにより、ユーザーまたはチームのレコードが **[選択したレコード]** ボックスに追加されます。

   > [!div class="mx-imgBorder"]
   > ![共有アクセスの選択](media/report-share3.png "共有アクセスの選択")
  

## <a name="share-a-report-with-your-organization-for-admins"></a>組織でレポートを共有する (管理者向け)
 レポートがすべてのユーザーにとって有用である場合は、組織で使用できるようにします。  

1. 左側のナビゲーションウィンドウで、[レポート] 領域を選択します。  
2. レポートの一覧で、共有するレポートを選択します。  
3. コマンドバーの **[編集]** を選択します。  
4. **[アクション]** メニューの **[レポートを組織で使用できるようにする]** を選択します。  
  
   > [!div class="mx-imgBorder"]
   > ![組織でレポートを共有](media/report-share4.png "組織でレポートを共有") する

## <a name="download-a-report"></a>レポートをダウンロードする

1. 左側のナビゲーションウィンドウで、[レポート] 領域を選択します。 
2. レポートの一覧で、共有するレポートを選択します。  
3. コマンドバーの **[編集]** を選択します。  
4. **[アクション]** メニューの **[レポートのダウンロード]** を選択します。  
RDL ファイルには、レポートの基になっている fetchXML が含まれています。
5. ダウンロードが完了したら、レポートを開きます。





### <a name="see-also"></a>関連項目

[レポートウィザードを使用してレポートを作成する](create-report-with-wizard.md)

[既存のレポートを追加する](add-existing-report.md)

[レポートフィルターの編集](edit-report-filter.md)

[レポートに表示されていないデータに関する問題のトラブルシューティング](troubleshoot-reports.md)


