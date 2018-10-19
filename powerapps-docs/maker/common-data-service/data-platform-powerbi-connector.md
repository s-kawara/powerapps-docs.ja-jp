---
title: PowerBI レポートの作成 | Microsoft Docs
description: アプリ コネクタ用 Common Data Service を使用する PowerBI Desktop からデータに接続しています。
author: clwesene
manager: kfile
ms.service: powerapps
ms.component: cds
ms.topic: conceptual
ms.date: 05/21/2018
ms.author: clwesene
search.audienceType:
  - maker
search.app:
  - PowerApps
  - D365CE
---
# <a name="create-a-power-bi-report"></a>Power BI レポートの作成
アプリ用 Common Data Service により、Power BI Desktop を使用するデータに直接接続してレポートを作成し、Power BI に公開することができます。 Power BI から、レポートのダッシュボードでの使用、他のユーザーへの共有、および Power BI モバイル アプリ上でのプラットフォーム間のアクセスができます。

![Power BI Desktop](./media/data-platform-cds-powerbi-connector/PBIDesktop.png "Power BI Desktop")

## <a name="prerequisites"></a>前提条件

アプリ用 Common Data Service により Power BI を使用するには、以下が必要です。

* Power BI Desktop をダウンロードしてインストールします。これはローカル コンピュータで実行する無料のアプリケーションです。 Power BI Desktop のダウンロードができます [こちら](https://powerbi.microsoft.com/desktop/)。
* ポータルにアクセスする作成者アクセス許可およびエンティティ内のデータにアクセスする読み取りアクセス許可付きアプリ環境用 Common Data Service。

## <a name="finding-your-common-data-service-for-apps-environment-url"></a>アプリ環境 URL 用 Common Data Service の検索

1. [PowerApps](https://web.powerapps.com/?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc) を開いて接続する環境を選択し、右上隅にある**設定の歯車**をクリックしてから、**高度なカスタマイズ**をクリックします。

    ![アプリ環境用 CDS](./media/data-platform-cds-powerbi-connector/CDSEnv1.png "アプリ環境用 CDS")

2. 開発者リソース セクションの下にある**リソース**をクリックして新しいタブを開きます。

    ![アプリ環境用 CDS](./media/data-platform-cds-powerbi-connector/CDSEnv2.png "アプリ環境用 CDS")

3. 新しいタブの URL のルートをコピーします。これは環境に対する一意の URL です。 URL は、**https://yourenvironmentid.crm.dynamics.com/** の形式になります。URL の残りをコピーしていないことを確認してください。 PowerBI レポートを作成する時に使用できるよう、他の便利な場所に保管してください。

    > [!div class="mx-imgBorder"] 
    > ![アプリ環境用 CDS](./media/data-platform-cds-powerbi-connector/CDSEnv3.png "アプリ環境用 CDS")

## <a name="connecting-to-common-data-service-for-apps-from-power-bi-desktop"></a>Power BI Desktop からアプリ用 Common Data Service へ接続

1. **Power BI Desktop** を起動します。初めての場合、ようこそ画面の表示か、または空のキャンバスへの移動かいずれかが行われます。**データの取得**をクリックして**詳細**を選択し、Power BI Desktop 用に使用可能なデータ ソースの詳細な一覧を開きます。

    ![Power BI Desktop](./media/data-platform-cds-powerbi-connector/CreateReport1.png "Power BI Desktop")

2. コネクタの一覧から、**オンライン サービス**および**アプリ用 Common Data Service (Beta 版)** をクリックします。 **接続** をクリックします。

    ![Power BI Desktop](./media/data-platform-cds-powerbi-connector/CreateReport2.png "Power BI Desktop")

3. **サーバー URL** フィールドに**アプリ環境 URL 用 Common Data Service** を貼り付け、**OK** をクリックします。 これが初めての場合、PowerApps およびアプリ用 Common Data Service に接続するために使用するのと同じ資格情報を使用してログインするよう求められます。

    ![Power BI Desktop](./media/data-platform-cds-powerbi-connector/CreateReport3.png "Power BI Desktop")

4. ナビゲーターは、3 つのフォルダーにグループ化された環境に対して使用可能なすべてのエンティティを表示します。 **共通データ モデル** フォルダーを展開します。

    * 共通データ モデル - 共通データ モデルの一部として一般的に使用される、すべての環境で使用可能な標準エンティティのことです。
    * ユーザー定義エンティティ - ユーザーの環境で作成またはインポートされたエンティティのことです。
    * システム - 共通データ モデルおよびユーザー定義エンティティを含め、ユーザーの環境におけるすべてのエンティティを含みます。

    ![Power BI Desktop](./media/data-platform-cds-powerbi-connector/CreateReport4.png "Power BI Desktop")

5. **取引先企業**エンティティを選択し、右ウィンドウでデータのプレビューを表示してから、**読み込み**をクリックします。

    ![Power BI Desktop](./media/data-platform-cds-powerbi-connector/CreateReport5.png "Power BI Desktop")

6. これでエンティティはレポートに読み込まれました。レポートの作成を開始するか、またはこのプロセスを繰り返してそのほかのエンティティを追加することができます。

    ![Power BI Desktop](./media/data-platform-cds-powerbi-connector/CreateReport6.png "Power BI Desktop")

7. フィールド パネルの**名前**フィールドをクリックして、レポートのキャンバスに新しいビジュアル化を追加します。 このプロセスを繰り返して、レポートを作成するためのビジュアル化を変更できるようになりました。

    ![Power BI Desktop](./media/data-platform-cds-powerbi-connector/CreateReport7.png "Power BI Desktop")


## <a name="using-option-sets"></a>オプション セットの使用

オプション セットは、アプリとフロー内でユーザーに値のドロップダウン リストを提供するためにエンティティで使用されます。 Power BI コネクタを使用している場合、オプション セット フィールドは 2 つの列として示され、一意の値と表示値の両方を表示します。

たとえば、ApprovalStatus というエンティティのオプション セットの場合、Power BI に 2 つのフィールドが表示されます。

* ApprovalStatus - オプション セットの各アイテムに対する一意の整数値を示します。フィルター適用時の補助であり、後で表示名を変更しても影響を受けません。
* ApprovalStatus_display - アイテムのフレンドリ表示名を示し、一般的にテーブルまたはグラフのオプションを表示する場合に使用されます。

    |ApproalStatus|ApprovalStatus_Display|
    |---------|---------|
    1|[提出済み]
    2|レビュー中
    3|承認済み
    4|拒否済み

## <a name="navigating-relationships"></a>ナビゲーションの関連付け

アプリ用 Common Data Service の関連付けには GUID フィールドを使用する 2 つのエンティティ間で、PowerBI Desktop 内での関連付けを作成する必要があります。これは他のフィールドとのあいまいさまたは重複が存在することのある作成レコードに対して関連付けが作成されていることを確認するために、システムが生成する一意の識別子です。 Power BI Desktop の関連付けの管理については、[こちら](https://docs.microsoft.com/power-bi/desktop-create-and-manage-relationships) をご覧ください。

一部の関連付けは自動的に作成されますが、レポートの作成時に正しい関連付けが確立されているかプレビューおよび確認を行うことができます。

* エンティティの検索フィールドには、関連エンティティのレコードの GUID が含まれます。
* 関連エンティティには、GUID を含む [EntityName]id 形式のフィールドがあります。たとえば、Accountid または MyCustomEntityid などです。
* PowerBI Desktop 関連付け管理機能を使用して、検索フィールドと関連エンティティの ID フィールド間で新しい関連付けを作成します。


## <a name="next-steps"></a>次のステップ
* [エンティティでのフィールドの管理](data-platform-manage-fields.md)
* [エンティティ間での関連付けの定義](data-platform-entity-lookup.md)


