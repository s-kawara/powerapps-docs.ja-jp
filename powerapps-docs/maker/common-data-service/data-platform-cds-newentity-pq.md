---
title: Power Query を使用して Common Data Service for Apps のエンティティにデータを追加する | Microsoft Docs
description: Power Query を使って Common Data Service (CDS) for App の新規または既存のエンティティに別のデータ ソースからデータを追加する詳しい手順を説明します。
author: AFTOwen
manager: kfile
ms.service: powerapps
ms.devlang: na
ms.topic: conceptual
ms.component: cds
ms.date: 03/21/2018
ms.author: anneta
ms.openlocfilehash: 60d1843e48a1dc1d310d877bcba67460da557993
ms.sourcegitcommit: b3b6118790d6b7b4285dbcb5736e55f6e450125c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2018
---
# <a name="add-data-to-an-entity-in-common-data-service-for-apps-by-using-power-query"></a>Power Query を使用して Common Data Service for Apps のエンティティにデータを追加する
この手順では、[Common Data Service (CDS) for Apps](data-platform-intro.md) にエンティティを作成し、Power Query を使って OData フィードからデータをエンティティに格納します。 同じ手法を使って、次のようなオンライン ソースやオンプレミスのソースからデータを統合できます。

* SQL Server
* Salesforce
* IBM DB2
* Access
* Excel
* Web API
* OData フィード
* テキスト ファイル

また、新規または既存のエンティティに読み込む前に、データのフィルター処理、変換、結合を行うこともできます。

PowerApps のライセンスを持っていない場合は、[無料でサインアップ](../signup-for-powerapps.md)できます。

## <a name="prerequisites"></a>前提条件
このトピックの手順を行うには、エンティティを作成できる[環境](../canvas-apps/working-with-environments.md)に切り替える必要があります。

## <a name="specify-the-source-data"></a>ソース データを指定する

1. [PowerApps](https://web.powerapps.com) にサインインし、左端近くにある **[データ]** の下向き矢印をクリックまたはタップします。

    ![PowerApps のホーム ページ](./media/data-platform-cds-newentity-pq/sign-in.png)

1. 表示される一覧で、**[データ統合]** をクリックまたはタップし、ウィンドウの右上隅にある **[新しいプロジェクト]** をクリックまたはタップします。

1. データ ソースの一覧で、**[OData]** をクリックまたはタップします。

    ![OAuth コネクタを選ぶ](./media/data-platform-cds-newentity-pq/choose-odata.png)

1. **[接続設定]** に次の URL を入力するか貼り付けて、**[次へ]** を選びます。<br>
`http://services.odata.org/V4/Northwind/Northwind.svc/`

1. テーブルの一覧で **Customers** のチェック ボックスをオンにして、**[次へ]** をクリックまたはタップします。

    ![Customers テーブルを選ぶ](./media/data-platform-cds-newentity-pq/select-table.png)

1. (省略可能) 含める列の選択、1 つまたは複数の方法でのテーブルの変換、インデックス列または条件列の追加、その他の変更を加え、ニーズに合わせてスキーマを修正します。

1. 右下隅で **[次へ]** をクリックまたはタップします。

## <a name="specify-the-target-entity"></a>ターゲット エンティティを指定する
1. **[設定を読み込む]** で、**[新しいエンティティに読み込む]** を選びます。

    ![新しいエンティティの名前を指定する](./media/data-platform-cds-newentity-pq/new-entity-name.png)

    新しいエンティティに異なる名前または表示名を付けることもできますが、このチュートリアルのとおりに進めるなら既定値のままにします。

1. **[プライマリ名フィールド]** の一覧で **ContactName** をクリックまたはタップし、右下隅の **[次へ]** をクリックまたはタップします。

    異なるプライマリ名前フィールドを指定すること、または作成しているエンティティの各フィールドにソース テーブルの異なる列をマップすることの、どちらか一方または両方を行うことができます。 このチュートリアルのとおりに進めるなら、既定の列マッピングのままにします。

1. **[読み込み状態]** が **[完了]** になったら、右下隅の **[完了]** を選びます。

1. **[データ]** (左端近く) で、**[エンティティ]** を選んでデータベース内のエンティティの一覧を表示します。

    OData フィードから作成した **Customers** エンティティが、カスタム エンティティとして表示されます。

    ![標準エンティティとカスタム エンティティの一覧](./media/data-platform-cds-newentity-pq/entity-list.png)

> [!WARNING]
> Power Query を使ってデータを既存のエンティティに追加する場合は、そのエンティティのすべてのデータが上書きされます。

**[既存のエンティティに読み込む]** を選んだ場合は、**Customers** テーブルからのデータを追加するエンティティを指定できます。 たとえば、Common Data Service が出荷する **Account** エンティティにデータを追加できます。 **[ソース列]** ではさらに、**Customers** テーブルの **ContactName** 列のデータを **Accounts** エンティティの **Name** 列に追加する、といったことを指定できます。

![新しいエンティティの名前を指定する](./media/data-platform-cds-newentity-pq/existing-entity.png)

これはとても心躍る機能です。お客様のご意見をお待ちしております。 この機能に関する[提案およびフィードバックをお寄せください](https://powerusers.microsoft.com/t5/PowerApps-Community/ct-p/PowerApps1)。

[アクセス許可に関するエラー メッセージ](data-platform-cds-newentity-troubleshooting-mashup.md)が表示されたら、管理者に連絡してください。