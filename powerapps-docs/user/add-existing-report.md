---
title: PowerApps の外部からレポートを追加する |Microsoft Docs
description: PowerApps の外部からレポートを追加する
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
ms.openlocfilehash: 24faa77b454cf3324e4b7277c94c6cd364aec9a9
ms.sourcegitcommit: e9671e018c1ee4b640528915350a367758991b6a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2019
ms.locfileid: "67420170"
---
# <a name="add-a-report-from-outside-powerapps"></a>PowerApps の外部からレポートを追加する

システムの外部でカスタムレポートを作成した場合は、PowerApps に簡単に追加できます。

カスタムレポートを作成する方法の詳細については、「[レポートおよび分析ガイド](https://docs.microsoft.com/en-us/dynamics365/customer-engagement/analytics/get-started-writing-reports)」を参照してください。

1. 左側のナビゲーションウィンドウで、[レポート] 領域を選択します。 
2. コマンドバーで **[新規]** を選択します。
  
   **別のアプリケーションで作成されたファイルを追加する**  
  
   1. **[ソース]** セクションの **[レポートの種類]** ボックスで、 **[既存のファイル]** を選択します。  
   
     > [!div class="mx-imgBorder"]
     > ![既存のレポートを追加する](media/add_existing_report.png "既存のレポートを追加する")
  
   2. **[ファイルの場所]** ボックスに、追加するファイルのパスとファイル名を入力するか、 **[参照]** をクリックしてファイルを指定します。 
   
      Excel ファイルなど、他にも多くのファイルの種類をアップロードできますが、これを SQL Server Reporting Services レポートやレポートウィザードで作成したレポートのように実行するには、ファイルをにする必要があります。RDL ファイル。 詳細については、「 [SQL Server Data Tools を使用したレポート作成環境](https://docs.microsoft.com/en-us/dynamics365/customer-engagement/analytics/report-writing-environment-using-sql-server-data-tools)」を参照してください。
  
      または  
  
   **Web ページへのリンクの追加**  
  
   1.  **[ソース]** セクションの **[レポートの種類]** ボックスで、 **[web ページへのリンク]** を選択します。  
  
   2.  **[Web ページの url]** ボックスに、web ページの url を入力します。  
  
3. レポートのプロパティを指定します。
  
   1.  **[詳細]** セクションで、レポートのわかりやすい名前と説明を指定します。  
  
   2.  **親**レポートのテキストボックスには、現在のレポートが存在する場合は親レポートが表示されます。  
  
   3. **カテゴリ**。 [**このフィールドの値を選択または変更**する] の![省略](media/ellipsis-button.png "")記号ボタンボタンをクリックし、このレポートに含めるカテゴリを指定します。  
  
   4. **関連するレコードの種類**。 特定のレコードの種類について、ページの [レポート] ボックスの一覧にレポートが表示されるようにするには、[**このフィールドの値を選択または変更**する] の![省略](media/ellipsis-button.png "")記号ボタンボタンをクリックし、[レコードの種類] を選択します。  
  
   5. **に表示**します。 レポートを表示する場所を指定するには、[**このフィールドの値を選択または変更**する] の![省略](media/ellipsis-button.png "")記号ボタンボタンをクリックし、1つまたは複数のオプションを選択します。  
  
        値が選択されていない場合、レポートはエンドユーザーに表示されません。  
  
4. **[保存]** または **[保存して閉じる]** を選択します。  




### <a name="see-also"></a>関連項目
[レポートの操作](work-with-reports.md) 

[レポートウィザードを使用してレポートを作成する](create-report-with-wizard.md)

[レポートフィルターの編集](edit-report-filter.md)

[レポートに表示されていないデータに関する問題のトラブルシューティング](troubleshoot-reports.md)
