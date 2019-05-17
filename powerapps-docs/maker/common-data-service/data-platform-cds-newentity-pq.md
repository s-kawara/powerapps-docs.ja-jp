---
title: Power Query を使用して Common Data Service でエンティティにデータを追加する | Microsoft Docs
description: 別のデータ ソースから Common Data Service で新規または既存のエンティティにデータを追加する Power Query の使用方法に関する詳細な手順。
author: mllopis
manager: kfile
ms.service: powerapps
ms.devlang: na
ms.topic: conceptual
ms.component: cds
ms.date: 03/21/2018
ms.author: millopis
search.audienceType:
  - maker
search.app:
  - PowerApps
  - D365CE
---

# <a name="add-data-to-an-entity-in-common-data-service-by-using-power-query"></a>Power Query を使用して Common Data Service でエンティティにデータを追加します
この手順では、[Common Data Service](data-platform-intro.md) でエンティティを作成し、Power Query を使用して OData フィードからのデータをそのエンティティに入力します。 同じ技術を使用してこれらのオンライン ソースおよび設置型ソースなどからデータを統合できます。

* SQL Server
* Salesforce
* IBM DB2
* アクセス
* Excel
* Web API
* OData フィード
* テキスト ファイル

新規または既存のエンティティへ読み込む前に、データをフィルター処理、変換、さらに結合できます。

PowerApps のライセンスがない場合、[無料のサインアップ](../signup-for-powerapps.md) ができます。

## <a name="prerequisites"></a>前提条件
このトピックに従って、エンティティを作成できるよう [環境](../canvas-apps/working-with-environments.md) を切替える必要があります。

## <a name="specify-the-source-data"></a>ソース データの指定

1. [PowerApps](https://web.powerapps.com/?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc) にサインインし、左端の近くにある**データ**の下矢印をクリックまたはタップします。

    ![PowerApps ホーム ページ](./media/data-platform-cds-newentity-pq/sign-in.png)

1. 表示される一覧で、**データ統合**をクリックまたはタップしてから、はウィンドウの右上隅の近くにある**新しいプロジェクト**をクリックまたはタップします。

1. データ ソースの一覧で、**OData** をクリックまたはタップします。

    ![OAuth コネクタを選択します](./media/data-platform-cds-newentity-pq/choose-odata.png)

1. **接続設定**で、この URL を入力または貼り付けてから、**次へ**を選択します。<br>
`http://services.odata.org/V4/Northwind/Northwind.svc/`

1. 表の一覧で、**顧客**チェック ボックスを選択し、**次へ**をクリックまたはタップします。

    ![顧客テーブルを選択します](./media/data-platform-cds-newentity-pq/select-table.png)

1. (任意) どの列を含めるかを選択する、1 つ以上の方法でテーブルを変換する、インデックスまたは条件付き列を追加する、またはその他の変更を加えることにより必要に応じてスキーマを変更します。

1. 右下隅で、**次へ**をクリックまたはタップします。

## <a name="specify-the-target-entity"></a>ターゲット エンティティの指定
1. **読み込み設定**で、**新しいエンティティへの読み込み**を選択します。

    ![新しいエンティティの名前を指定します](./media/data-platform-cds-newentity-pq/new-entity-name.png)

    新しいエンティティに別の名前または表示名を付けることができますが、このチュートリアルに正確に従って既定値のままにしておきます。

1. **プライマリ名フィールド**の一覧で、**ContactName** をクリックまたはタップしてから、右下隅にある**次へ**をクリックまたはタップします。

    異なるプライマリ名フィールドを指定する、作成するエンティティの各フィールドにソース テーブルの別の列をマップする、またはその両方ができます。 また、クエリ出力のテキスト列を Common Data Service の複数行テキストまたは単一行テキストの、どちらで作成するかも指定できます。 このチュートリアルに正確に従い、列マッピングを既定のままにしておきます。

1. **読み込み状態**が**完了済み**の場合は、右下隅にある**完了**を選択します。

1. **データ** (左端の近く) で、**エンティティ** を選択してデータベースでエンティティの一覧を表示します。

    ユーザー定義エンティティとして表示される OData フィードから作成した**顧客**エンティティ。

    ![標準およびユーザー定義のエンティティの一覧](./media/data-platform-cds-newentity-pq/entity-list.png)

> [!WARNING]
> 既存のエンティティにデータを追加するために Power Query を使用すると、そのエンティティのすべてのデータが上書きされます。

**既存のエンティティへの読み込み**を選択すると、**顧客**テーブルからデータを追加するエンティティを指定できます。 たとえば 、Common Data Service に付属する**取引先企業**エンティティにデータを追加できます。 **ソース列**で、**顧客**テーブルからの **ContactName** 列の次のデータが、**取引先企業**エンティティの**名前**列に追加されるように指定できます。

![新しいエンティティの名前を指定します](./media/data-platform-cds-newentity-pq/existing-entity.png)

この機能についてのお客様のフィードバックをいただけるのを大変楽しみにしております。 この機能についての [ご意見やフィードバックをお寄せください](https://powerusers.microsoft.com/t5/PowerApps-Community/ct-p/PowerApps1)。

[アクセス許可に関するエラー メッセージ](data-platform-cds-newentity-troubleshooting-mashup.md) 表示される場合は、管理者にお問い合わせください。
