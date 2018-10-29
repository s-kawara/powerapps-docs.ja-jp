---
title: PowerApps、Microsoft Flow、Power BI と SharePoint Online の統合 (概要) | Microsoft Docs
description: このチュートリアル シリーズでは、SharePoint リスト、および SharePoint Online と統合する 3 つの主要テクノロジである PowerApps、Microsoft Flow、Power BI に基づいてプロジェクト管理用の基本的なキャンバス アプリを作成する方法を説明します。
author: mgblythe
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: ''
ms.date: 12/19/2017
ms.author: mblythe
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: fa2631d065425ab57e47dccbb470f577d6474f23
ms.sourcegitcommit: 429b83aaa5a91d5868e1fbc169bed1bac0c709ea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/24/2018
ms.locfileid: "42831025"
---
# <a name="integrate-powerapps-microsoft-flow-and-power-bi-with-sharepoint-online"></a>PowerApps、Microsoft Flow、Power BI と SharePoint Online の統合
SharePoint Online をご利用で、ビジネス プロセスの自動化と効率化をお望みですか? PowerApps、Microsoft Flow、または Power BI を使用しているものの、SharePoint Online でどのように使用すればいいかをもっと知りたいですか? お探しのものはここにあります。 このチュートリアル シリーズでは、SharePoint リスト、および SharePoint Online と統合する 3 つの主要テクノロジである PowerApps、Microsoft Flow、Power BI に基づいてプロジェクト管理用の基本的なキャンバス アプリを作成する方法を説明します。 これらのテクノロジの連携により、お客様のビジネスの *測定* 、結果に基づく *行動* 、ワークフローの *自動化* が容易に可能です。 このシリーズを終了すると、次のようなすばらしいシナリオが完成します。

![完成シナリオの図](./media/sharepoint-scenario-intro/composite-with-background.png)

## <a name="business-scenario"></a>ビジネス シナリオ
このチュートリアル シリーズでは、SharePoint Online のサイトを持つ Contoso という会社が、このサイトでプロジェクトの申請、承認、開発、最終確認のライフサイクル全体を管理しています。 *プロジェクト申請者* (各部門のトップなど) が SharePoint リストに項目を追加して、IT プロジェクトを申請します。 *プロジェクト承認者* (IT マネージャーなど) によってプロジェクトが検討され、承認または却下されます。 承認されると、プロジェクトは *プロジェクト管理者* に割り当てられ、同じアプリを使用して追加の詳細が 2 つ目のリストに追加されます。 SharePoint に埋め込まれた Power BI レポートを使用して、  *ビジネス アナリスト* が現在および完了したプロジェクトの見直しを行います。  承認メールの送信と Power BI のアラートへの対応には Microsoft Flow を使用します。

## <a name="getting-started-quickly"></a>すぐに始める
このチュートリアル シリーズで紹介するシナリオは、本格的なプロジェクト管理や分析アプリと比べると単純ですが、それでもすべてのタスクを完了するには時間がかかります。 PowerApps、Microsoft Flow、Power BI を SharePoint の使用についての簡単な概要を必要とされる場合は、次の記事をご覧ください。

* **PowerApps**: 「[PowerApps を使用して、SharePoint 内からアプリを生成する](generate-app-from-sharepoint-list-interface.md)」と「[SharePoint リストのデータを管理するアプリの生成](app-from-sharepoint.md)」
* **Microsoft Flow**: 「[Microsoft Flow での承認待ち](https://docs.microsoft.com/flow/wait-for-approvals)」
* **Power BI**: 「[SharePoint Online にレポート Web パーツを埋め込む](https://docs.microsoft.com/power-bi/service-embed-report-spo)」

完了したら、このページに戻って完全なシナリオをご確認ください。

このシナリオ内でも関心のあるタスクに取り組んで、時間がある場合はタスクを完了することができます。 タスク 1 で SharePoint リストを設定したら、お好きな順序でタスク 2 ～ 5 に取り組むことができます。そのあとのタスク 6 ～ 8 は順番に取り組んでください。 最後に、このシナリオの[ダウンロード パッケージ](https://aka.ms/o4ia0f)の一部として、完成した 2 つのアプリと Power BI Desktop レポートが 1 つ含まれています。 各タスクのすべての手順を完了していない場合でも、これらをご覧になって例から学ぶことができます。

## <a name="prerequisites"></a>前提条件
シナリオを完了するには、次のサブスクリプションとデスクトップ ツールが必要です。 Office 365 Business Premium サブスクリプションには、PowerApps と Microsoft Flow が含まれています。

| **サブスクリプションまたはツール** | **リンク** |
| --- | --- |
| Office 365 Business Premium のサブスクリプション |[無料試用版のサブスクリプション](https://signup.microsoft.com/Signup?OfferId=467eab54-127b-42d3-b046-3844b860bebf&dl=O365_BUSINESS_PREMIUM&ali=1) |
| Power BI Pro のサブスクリプション |[無料試用版のサブスクリプション](https://powerbi.microsoft.com/get-started/) (**無料試用版**をクリック) |
| Power BI Desktop |[無料ダウンロード](https://powerbi.microsoft.com/get-started/) (**無料ダウンロード**をクリック) |

各テクノロジの基本的な知識があることが望ましいですが、これらのテクノロジの一部になじみがない場合でも、シナリオを完了できます。 次のコンテンツを使用すると、すばやく習得できます。

* [SharePoint の使用を開始する](https://support.office.com/article/Get-started-with-SharePoint-909ec2f0-05c8-4e92-8ad3-3f8b0b6cf261)
* [PowerApps ガイド学習](../../guided-learning/index.md)
* [Microsoft Flow ガイド学習](https://docs.microsoft.com/flow/guided-learning/)
* [Power BI ガイド付き学習](https://docs.microsoft.com/power-bi/guided-learning/)

## <a name="next-steps"></a>次の手順
このチュートリアル シリーズの次の手順では、シリーズ全体で使用する [SharePoint Online リストを設定](sharepoint-scenario-setup.md)します。

