---
title: Power BI ダッシュボードのデータ アラートを設定する | Microsoft Docs
description: このタスクでは、保留中のプロジェクトの承認に時間がかかりすぎる場合に通知するアラート、およびアラート発生時に対応するフローを Power BI に追加します。
author: NickWaggoner
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: ''
ms.date: 06/12/2017
ms.author: niwaggon
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 89c22bec8972c0d58c559a09d4e9f0a8a8e3b7f5
ms.sourcegitcommit: 90245baddce9d92c3ce85b0537c1ac1cf26bf55a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2019
ms.locfileid: "57799090"
---
# <a name="set-up-data-alerts-for-the-power-bi-dashboard"></a>Power BI ダッシュボードのデータ アラートを設定する
> [!NOTE]
> この記事は、SharePoint Online で PowerApps、Microsoft Flow、Power BI を使用するチュートリアル シリーズの一部です。 シリーズ全般に関することや、関連するファイルのダウンロードの詳細については、[シリーズの概要](sharepoint-scenario-intro.md)に関する記事をご覧ください。

このタスクでは、保留中のプロジェクトの承認に時間がかかりすぎる場合に通知するアラート、およびアラート発生時に対応するフローを Power BI に追加します。 アラートについて詳しくは、「[Power BI サービスでのデータ アラート](https://docs.microsoft.com/power-bi/service-set-data-alerts)」を参照してください。

## <a name="step-1-create-an-alert"></a>手順 1:アラートを作成します。
1. Power BI サービスで、前回のタスクで作成したダッシュボードを開きます。
2. 1 つの数値が表示されたカードで、省略記号 (**. . .**) をクリックまたはタップします。
   
    ![承認待ちの最大日数が表示されたカード](./media/sharepoint-scenario-alerts-flow/07-01-01-tile-ellipsis.png)
3. 右上にある ![ベル アイコン](./media/sharepoint-scenario-alerts-flow/icon-bell.png).
   
    ![タイル メニュー](./media/sharepoint-scenario-alerts-flow/07-01-02-tile-bell.png)
4. 右側のウィンドウで、**[アラート ルールの追加]** をクリックまたはタップします。
   
    ![[アラート ルールの追加]](./media/sharepoint-scenario-alerts-flow/07-01-03-add-alert.png)
5. アラートを実行する頻度などの、アラートで使用可能なオプションを確認します。 **[しきい値]** に「25」の値を入力し、**[保存して閉じる]** をクリックまたはタップします。
   
    ![アラートのしきい値を設定して保存](./media/sharepoint-scenario-alerts-flow/07-01-04-save-alert.png)

56 は 25 のしきい値を超えていますが、アラートがすぐに発生するわけではありません。 データが更新されるとアラートが発生しますが、これは[シナリオ全体をおさらい](sharepoint-scenario-summary.md)するときに確認できます。

アラートが発生すると、Power BI がアラートの作成者に電子メールを送信します。次の手順では、Microsoft Flow を使用して追加の電子メールを送信する方法を説明します。

## <a name="step-2-create-a-flow-that-responds-to-the-alert"></a>手順 2:アラートに応答するフローを作成します。
1. flow.microsoft.com にサインインし、**[サービス]**、**[Power BI]** の順にクリックまたはタップします。
   
    ![Microsoft Flow 内の Power BI](./media/sharepoint-scenario-alerts-flow/07-01-05-power-bi.png)
2. **[Power BI データ アラートがトリガーされたときに対象ユーザーに電子メールを送信する]** をクリックまたはタップします。
   
    ![Power BI データ アラートがトリガーされたときに電子メールを送信](./media/sharepoint-scenario-alerts-flow/07-01-06-alert-flow.png)
3. **[このテンプレートを使用する]** をクリックまたはタップします。
4. まだサインインしていない場合、Outlook および Power BI にサインインし、**[続行]** をクリックまたはタップします。
   
    ![サインインして続行](./media/sharepoint-scenario-alerts-flow/07-01-08-continue.png)
5. **[アラート ID]** のドロップダウン リストで、**[Alert for Max days pending approval]\(承認待ちの最大日数のアラート\)** を選択します。
   
    ![指定とトリガーとしてのアラート](./media/sharepoint-scenario-alerts-flow/07-01-09-choose-alert.png)
6. **[宛先]** ボックスに、有効な電子メール アドレスを入力します。
   
    ![電子メールの送信先を指定](./media/sharepoint-scenario-alerts-flow/07-01-10-choose-email.png)
7. **[編集]** をクリックまたはタップして、更新できるその他のフィールドを表示します。
   
    ![アラート メールの編集](./media/sharepoint-scenario-alerts-flow/07-01-11-email-full.png)
8. 画面の右上の **[フローの作成]**、**[完了]** の順にクリックします。
   
    ![[完了] ボタン](./media/sharepoint-scenario-alerts-flow/07-01-12-done.png)

[シナリオ全体をおさらいする](sharepoint-scenario-summary.md)ときに、このフローが実行されます。 今度は、このシナリオの最後のタスクである、SharePoint への Power BI レポートの埋め込みに進みます。

## <a name="next-steps"></a>次の手順
このチュートリアル シリーズの次の手順では、[SharePoint Online に Power BI プロジェクト レポートを埋め込み](sharepoint-scenario-embed-report.md)ます。

