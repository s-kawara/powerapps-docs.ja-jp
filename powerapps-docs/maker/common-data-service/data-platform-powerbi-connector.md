---
title: Power BI レポートを作成する | Microsoft Docs
description: Common Data Service for Apps コネクタを使って Power BI Desktop からデータに接続します。
author: clwesene
manager: kfile
ms.service: powerapps
ms.component: cds
ms.topic: conceptual
ms.date: 05/21/2018
ms.author: clwesene
ms.openlocfilehash: bb0bec7cf459eb9084aea4db7264350b7913e578
ms.sourcegitcommit: 79b8842fb0f766a0476dae9a537a342c8d81d3b3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/07/2018
ms.locfileid: "37898758"
---
# <a name="create-a-power-bi-report"></a>Power BI レポートを作成する
Common Data Service for Apps コネクタを利用すると、Power BI Desktop を使ってデータに直接接続し、レポートを作成して Power BI に発行することができます。 Power BI からは、レポートをダッシュボードで使用したり、他のユーザーと共有したり、Power BI モバイル アプリ上でプラットフォーム横断的にアクセスしたりできます。

![Power BI Desktop](./media/data-platform-cds-powerbi-connector/PBIDesktop.png "Power BI Desktop")

## <a name="prerequisites"></a>前提条件

Common Data Service for Apps で Power BI を使うには、以下のことが必要です。

* Power BI Desktop をダウンロードしてインストールします。このアプリケーションは無料であり、ローカル コンピューター上で動作します。 Power BI Desktop は[こちら](https://powerbi.microsoft.com/desktop/)からダウンロードできます。
* ポータルにアクセスするための作成者アクセス許可およびエンティティ内のデータにアクセスするための読み取りアクセス許可が割り当てられている Common Data Service for Apps の環境。

## <a name="finding-your-common-data-service-for-apps-environment-url"></a>Common Data Service for Apps の環境 URL の検索

1. [PowerApps](https://web.powerapps.com) を開き、接続しようとしている環境を選び、右上隅の**設定歯車**をクリックして、**[高度なカスタマイズ]** をクリックします

    ![アプリ環境用の CDS](./media/data-platform-cds-powerbi-connector/CDSEnv1.png "アプリ環境用の CDS")

2. [開発者リソース] セクションの下の **[リソース]** をクリックして、新しいタブを開きます。

    ![アプリ環境用の CDS](./media/data-platform-cds-powerbi-connector/CDSEnv2.png "アプリ環境用の CDS")

3. 新しいタブの URL のルートをコピーします。これが、お使いの環境の一意の URL です。 URL の形式は **https://yourenvironmentid.crm.dynamics.com/** です。URL のこれ以外の部分をコピーしないようにしてください。 Power BI レポートを作成するときに使える便利な場所に保存しておきます。

    ![アプリ環境用の CDS](./media/data-platform-cds-powerbi-connector/CDSEnv3.png "アプリ環境用の CDS")

## <a name="connecting-to-common-data-service-for-apps-from-power-bi-desktop"></a>Power BI Desktop から Common Data Service for Apps への接続

1. **Power BI Desktop** を起動します。初めての場合はようこそ画面が表示されてから、それ以外の場合は直接、空のキャンバスに移動しますが、いずれの場合も、**[データを取得]** をクリックし、**[その他]** を選んで、Power BI Desktop で使用できるすべてのデータ ソースの一覧を開きます。

    ![Power BI Desktop](./media/data-platform-cds-powerbi-connector/CreateReport1.png "Power BI Desktop")

2. **[オンライン サービス]** をクリックし、コネクタの一覧から **[Common Data Service for Apps (Beta)]\(Common Data Service for Apps (ベータ)\)** をクリックします。 **[接続]** をクリックします。

    ![Power BI Desktop](./media/data-platform-cds-powerbi-connector/CreateReport2.png "Power BI Desktop")

3. お使いの **Common Data Service for Apps 環境の URL** を **[サーバー URL]** フィールドに貼り付け、**[OK]** をクリックします。 初めての場合は、PowerApps および Common Data Service for Apps に接続するときに使うものと同じ資格情報を使ってログインするよう求められます。

    ![Power BI Desktop](./media/data-platform-cds-powerbi-connector/CreateReport3.png "Power BI Desktop")

4. ナビゲーターに、環境で使用可能なすべてのエンティティが 3 つのフォルダーにグループ化されて表示されます。 **[Common Data Model]** フォルダーを展開します。

   * [Common Data Model] - ここには、Common Data Model の一部としてすべての環境で共通に使用できる標準的なエンティティが表示されます。
   * [Custom Entities] - ユーザーが自分の環境で作成したかそこにインポートしたエンティティです。
   * [System] - Common Data Model エンティティやカスタム エンティティを含む、環境内のすべてのエンティティが含まれます。

     ![Power BI Desktop](./media/data-platform-cds-powerbi-connector/CreateReport4.png "Power BI Desktop")

5. **[アカウント]** エンティティを選び、右側のウィンドウでデータのプレビューを確認して、**[読み込み]** をクリックします。

    ![Power BI Desktop](./media/data-platform-cds-powerbi-connector/CreateReport5.png "Power BI Desktop")

6. エンティティがレポートに読み込まれ、レポートの作成を始められるようになります。または、この手順を繰り返して、さらにエンティティを追加します。

    ![Power BI Desktop](./media/data-platform-cds-powerbi-connector/CreateReport6.png "Power BI Desktop")

7. [フィールド] パネルの **[名前]** フィールドをクリックして、新しい視覚エフェクトをレポート キャンバスに追加します。 この手順を繰り返したり、視覚エフェクトを変更したりして、レポートを作成できます。

    ![Power BI Desktop](./media/data-platform-cds-powerbi-connector/CreateReport7.png "Power BI Desktop")


## <a name="using-option-sets"></a>オプション セットの使用

オプション セットは、アプリやフロー内でユーザーに値のドロップダウン リストを提供するための、エンティティにおいて使用されます。 Power BI コネクタを使っているときは、オプション セット フィールドは一意値と表示値の両方を示す 2 つの列として表示されます。

たとえば、ApprovalStatus という名前のエンティティに対するオプション セットがある場合、Power BI には次のような 2 つのフィールドが表示されます。

* ApprovalStatus - オプション セット内の各項目の一意の整数値が表示されます。後で表示名を変更してもこの値には影響がないので、フィルターを適用するときに便利です。
* ApprovalStatus_display - 項目のわかりやすい表示名が示され、テーブルやグラフでオプションを表示するときに最もよく使われます。

    |ApproalStatus|ApprovalStatus_Display|
    |---------|---------|
    1|Submitted
    2|In Review
    3|Approved
    4|Rejected

## <a name="navigating-relationships"></a>リレーションシップのナビゲーション

Common Data Service for Apps 内のリレーションシップに対しては、PowerBI Desktop において GUID フィールドを使って 2 つのエンティティ間にリレーションシップを作成する必要があります。GUID は、他のフィールドとのあいまいさや重複がある場合に正しいレコードに対してリレーションシップが作成されるようにするため、システムによって生成される一意の識別子です。 Power BI Desktop でのリレーションシップの管理について詳しくは、[こちら](https://docs.microsoft.com/power-bi/desktop-create-and-manage-relationships)をご覧ください。

リレーションシップが自動的に作成されることもありますが、それでもレポートを作成するときに、正しいリレーションシップが確立されていることを確認します。

* エンティティの参照フィールドには、関連エンティティのレコードの GUID が含まれます。
* 関連エンティティには "<エンティティ名>id" という形式のフィールド (例: Accountid、MyCustomEntityid) があり、GUID が含まれます。
* PowerBI Desktop のリレーションシップの管理機能を使って、参照フィールドと関連エンティティの ID フィールドの間に、新しいリレーションシップを作成します。


## <a name="next-steps"></a>次の手順
* [エンティティのフィールドを管理する](data-platform-manage-fields.md)
* [エンティティ間のリレーションシップを定義する](data-platform-entity-lookup.md)


