---
title: アプリ用 Common Data Service で OData データ プロバイダーを使用する仮想エンティティのチュートリアル | MicrosoftDocs
description: 仮想エンティティで OData v4 データ プロバイダーを使用する方法について説明します
ms.custom: ''
ms.date: 06/04/2018
ms.reviewer: ''
ms.service: crm-online
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Dynamics 365 (online)
- Dynamics 365 Version 9.x
- powerapps
ms.assetid: ''
caps.latest.revision: 11
author: Mattp123
ms.author: matp
manager: kvivek
ms.openlocfilehash: ebdd8f80aad2d353d017626b7c403da93803c19b
ms.sourcegitcommit: aba996b1773ecdf62758e06b34eaf57bede29e08
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/08/2018
ms.locfileid: "39691597"
---
# <a name="virtual-entity-walkthrough-using-the-odata-v4-data-provider"></a>OData v4 データ プロバイダーを使用する仮想エンティティのチュートリアル

ご自分のモデル駆動型アプリ内の外部データ ソースまたは Dynamics 365 for Customer Engagement のサービスの分野からチケット情報にアクセスする必要があるとします。 この簡単なチュートリアルでは、OData Web サービスからランタイムでチケット データを取得する外部スキーマにマップされたフィールドを含む、仮想エンティティをモデル化します。

## <a name="data-source-details"></a>データ ソースに関する詳細

このチュートリアルに使用されるデータ ソースには OData v4 Web サービスが含まれるため、ご利用の環境に含まれる OData v4 データ プロバイダーを使用できます。

Web サービスの URL: `http://contosowebservice.azurewebsites.net/odata/` 

> [!IMPORTANT]
> このチュートリアルに使用される Web サービスの URL は、機能する Web サービスではありません。

このチュートリアルでは、次の 3 つのフィールドを含む仮想エンティティが 1 つ必要です。

|外部フィールド名 |外部データ型 |仮想エンティティ データ型 |目的 |
|---------|---------|---------|---------|
|TicketID |`Edm.Guid` |主キー |エンティティ用の主キー |
|Title  |`Edm.String` |1 行テキスト |チケットのタイトル |
|深刻度 |`Edm.Int32`| 整数 |チケットの重要度を示す 0 から 4 の数値 |

外部データ ソースの Ticket エンティティの OData メタデータ

```xml
<EntityType Name="Ticket">
  <Key>
    <PropertyRef Name="TicketID" />
  </Key>
  <Property Name="TicketID" Nullable="false" Type="Edm.Guid" />
  <Property Name="Title" Type="Edm.String" />
  <Property Name="Severity" Nullable="false" Type="Edm.Int32" />
</EntityType>
```

## <a name="create-the-data-source"></a>データ ソースの作成

OASIS Open Data Protocol (OData) のサンプル Web サービスを使用する OData v4 データ プロバイダー用にデータ ソースを作成します。

1. **[設定]** > **[管理]** > **[仮想エンティティ データ ソース]** の順に移動します。
1. **[新規]**、**[OData v4 Data Provider]\(OData v4 データ プロバイダー\)** の順に選択して、**[OK]** を選択します。
1. 次の情報を入力または選択します。

    |フィールド|値|
    |--|--|
    |**Name**|Contoso サンプル データ ソース|
    |**URL**|`http://contosowebservice.azurewebsites.net/odata` |
    |**タイムアウト**|30|
    |**インライン カウントを返す**|True|

その他のフィールドはそのままにして、**[保存して閉じる]** を選択します。

> [!TIP]
> 独自の Web サービスを使用している場合、ご利用の Web ブラウザーに貼り付けてその URL が有効であることを確認します。 

## <a name="open-solution-explorer"></a>ソリューション エクスプローラーを開く

作成するカスタム エンティティの名前には、カスタマイズのプレフィックスが含まれます。 これは、作業中のソリューション用のソリューション発行元に基づいて設定されます。 カスタマイズのプレフィックスが重要であれば、カスタマイズのプレフィックスがこのエンティティに必要なプレフィックスになる、アンマネージド ソリューションを使用していることを確認します。 詳細情報: [Change the solution publisher prefix](change-solution-publisher-prefix.md) (ソリューション発行元のプレフィックスを変更する) 

[!INCLUDE [cc_navigate-solution-from-powerapps-portal](../../includes/cc_navigate-solution-from-powerapps-portal.md)]


## <a name="create-the-virtual-entity"></a>仮想エンティティを作成する

1. ソリューション エクスプローラーの左側のナビゲーション ウィンドウで **[エンティティ]** を選んでから、メイン ウィンドウで **[新規]** を選びます。
2. **[エンティティ: 新規]** フォームで、**[仮想エンティティ]** オプションを選択して、次の情報を入力します。 

    |フィールド|値|
    |--|--|
    |**データ ソース**|Contoso サンプル データ ソース|
    |**表示名**|チケット|
    |**複数名**|チケット|
    |**Name**|new_ticket|
    |**外部名**|チケット|
    |**外部コレクション名**|チケット|
    |**メモ (添付ファイルを含む)**|選択済み|
    |**アクティビティ**|選択済み|

1. **[このエンティティが表示される領域]** の横で **[サービス]** を選択して、**[保存]** を選択します (しかし、エンティティ フォームは閉じないでください)。
    ![[チケット] のエンティティ定義](media/ticket-entity.png)

## <a name="create-the-fields-for-the-virtual-entity"></a>仮想エンティティのフィールドを作成する

**[エンティティ: チケット]** ページの左側のナビゲーション ウィンドウで、**[フィールド]** を選択します。 このチュートリアルの一部として、2 つの既存のフィールドを編集して、3 つ目のフィールドを追加します。

> [!IMPORTANT]
> 外部名は大文字と小文字を区別します。 ご自分の Web サービス メタデータを参照して、正しい名前を使用していることを確認します。
> Null 許容値の False は、属性が必要であることを示します。 主キー フィールドは、常にシステムに必要なことに注意してください。

1. **new_ticketid** フィールドを開いて、次の属性をここに示す値に変更します: **[外部名]**: TicketID ![[TicketID] フィールド](media/ticketid-field.png)
1. **[保存して閉じる]** を選びます。
1. **new_name** フィールドを開いて、次の属性にここに示す値を含むように変更します。
    - **[表示名]**: タイトル
    - **[外部名]**: Title ![[タイトル] フィールド](media/title-field.png)
1. **[保存して閉じる]** を選びます。
1. **[新規]** を選択して、**[Field: New for Ticket]\(フィールド: チケットの新規作成\)** ページで次の情報を入力します。

    |フィールド|値|
    |--|--|
    |**表示名**|深刻度|
    |**Name**|new_severity|
    |**外部名**|深刻度|
    |**フィールド要件**|必須項目|
    |**データ型**|整数|
    |**最小値**|0|
    |**最大値**|4|

  ![[重要度] フィールド](media/severity-field.png)
1. **[保存して閉じる]** を選びます。

## <a name="add-the-fields-to-the-main-form"></a>フィールドをメイン フォームに追加する

1. [チケット] エンティティ ウィンドウで **[フォーム]** を選択します。
1. メイン フォームを開いて、右側のウィンドウから **[重要度]** フィールドを **[タイトル]** フィールドの下の **[全般]** セクションにドラッグ アンド ドロップします。 
    ![メイン フォームに追加された [重要度] フィールド](media/drop-severity-field.png)
1. [チケット] エンティティ ウィンドウで **[保存して閉じる]** を選択します。

## <a name="configure-the-default-view"></a>既定のビューを構成する

1. ソリューション エクスプローラーの左側のウィンドウの **[Ticket entity]\(チケット エンティティ\)** の下で、**[ビュー]** を選択します。
1. **[すべてのチケット]** ビューを開きます。
1. **[タスク]** ウィンドウで **[列の追加]** を選択します。
    ![ビューに列を追加する](media/addcolumns.png)
1. **[重要度]**、**[OK]** の順に選択します。
1. **[ビュー: すべてのチケット]** ウィドウで **[保存して閉じる]** を選択します。
1. ソリューション エクスプローラー ウィンドウで、**[すべてのカスタマイズの​​公開]** を選択します。
    ![すべてのカスタマイズの​​公開](media/publishall.png)
1. すべてのカスタマイズが公開されたら、ソリューション エクスプローラー ウィンドウを閉じます。

## <a name="view-the-virtual-entity-in-action-with-dynamics-365-customer-engagement"></a>Dynamics 365 Customer Engagement で動作中の仮想エンティティを表示する

1. **[サービス]** > **[拡張機能]** > **[チケット]** の順に移動します。
    
    ![チケットの領域](media/ticket-area.png)

    **[すべてのチケット]** ビューが表示されます。 **[サービス]** 領域からエンティティを表示するには、ご利用のブラウザーを更新する必要があることに注意してください。

    ![[すべてのチケット] ビュー](media/all-tickets-view.png)
1. **[チケット]** レコードを開いて、指定されたレコードに **[タイトル]** と **[重要度]** フィールドを含むフォームを表示します。
    ![[チケット] レコード](media/ticket-record.png)

### <a name="see-also"></a>関連項目

[OData v4 データ プロバイダーの構成、要件、ベスト プラクティス](virtual-entity-odata-provider-requirements.md)<br />
[外部データ ソースからのデータを含むエンティティの作成と編集](create-edit-virtual-entities.md)
