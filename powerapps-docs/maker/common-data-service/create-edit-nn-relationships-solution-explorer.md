---
title: 'ソリューション エクスプローラーを使用して Common Data Service で N:N (多対多) のエンティティ関係を作成する | MicrosoftDocs'
description: 'N:N (多対多) の関連付けを作成する方法を学習する'
ms.custom: ''
ms.date: 05/29/2018
ms.reviewer: ''
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
  - Dynamics 365 Version 9.x
  - powerapps
author: Mattp123
ms.author: matp
manager: kvivek
search.audienceType:
  - maker
search.app:
  - PowerApps
  - D365CE
---

# <a name="create-nn-many-to-many-entity-relationships-in-common-data-service-using-solution-explorer"></a>ソリューション エクスプローラーを使用して Common Data Service で N:N (多対多) のエンティティ関係を作成する

ソリューション エクスプローラーは Common Data Serviceの N:N (多対多) を作成、編集することができます。

[PowerApps ポータル](https://web.powerapps.com/?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc)では一般的なオプションのほどんとを構成できますが、特定のオプションはソリューション エクスプローラーを使用してのみ設定できます。 詳細:
- [多対多 (N:N) のエンティティの関連付けを作成する](create-edit-nn-relationships.md)
- [PowerApps ポータルを使用して Common Data Service に多対多のエンティティー リレーションシップを作成する](create-edit-nn-relationships-portal.md)

  
## <a name="open-solution-explorer"></a>ソリューション エクスプローラーを開きます

作成するユーザー定義関連付けの名前の一部はカスタマイズの接頭辞です。 これは、作業中のソリューションの発行者に基づいて設定されます。 カスタマイズの接頭辞に注意を払う場合は、カスタマイズの接頭辞がこのエンティティに対して必要な接頭辞であるアンマネージド ソリューションで作業するようにします。 詳細: [ソリューション発行者の接頭辞を変更する](change-solution-publisher-prefix.md) 

[!INCLUDE [cc_navigate-solution-from-powerapps-portal](../../includes/cc_navigate-solution-from-powerapps-portal.md)]

## <a name="view-entity-relationships"></a>エンティティの関連付けを表示する

ソリューション エクスプローラーで、**エンティティ** を展開し、エンティティを選択します。 そのエンティティ内で、**N:N の関連付け**を選択します。

![N:N エンティティの関連付けの表示](media/view-nn-entity-relationships-solution-explorer.png)

## <a name="create-relationships"></a>関連付けを作成する

[エンティティの関連付けを表示](#view-entity-relationships)しているときに、コマンド バーから**新しい多対多関連付け**を選択します。

> [!NOTE]
> コマンドを使用できない場合は、エンティティには、ユーザー定義の関連付けを作成する権限がありません。

![新しい多対多の関連付けフォーム](media/new-nn-entity-relationship-form-solution-explorer.png)

**エンティティの名前**フィールドの**その他のエンティティ**グループで、関連付けを作成するエンティティを選択します。 これにより、**名前**および**関連付けのエンティティの名前**フィールドが**関連付けの定義**グループに設定されます。

![エンティティの関連付けの保存ボタン](media/save-entity-icon-solution-explorer.png)をクリックすると、エンティティを保存して編集を続けることができます。 詳細情報: [関連付けの編集](#edit-relationships)

> [!NOTE]
> **名前**または**関連付けのエンティティの名前**の値が既にシステムに存在する場合、保存するとエラーが表示されます。 一意になるように値を編集して再試行します。

## <a name="edit-relationships"></a>関連付けの編集

[エンティティの関連付けを表示](#view-entity-relationships)しているときに、編集するエンティティを選択します。 

> [!NOTE]
> 管理ソリューションの発行者は、ソリューションの一部である関連付けのカスタマイズを回避できます。

次のエンティティの関連付けプロパティを、関連付けを作成してから編集できます。

> [!IMPORTANT]
> これらのプロパティを編集した後は、モデル駆動型アプリで有効になる前にカスタマイズを公開する必要があります。

### <a name="edit-display-options"></a>表示オプションの編集

**現在のエンティティ**と**その他のエンティティ**の両方で、モデル駆動型アプリケーションの関連エンティティの表示方法をコントロールする表示オプションフィールドを編集できます。

|フィールド|説明|
|--|--|
|**表示オプション**|関連エンティティの一覧を表示する方法。 詳細情報: [表示オプション](#display-options)|
|**カスタム ラベル**|**表示オプション** として **カスタム ラベルを使用する** を選択した場合に、複数名の代わりに使用するローカライズ可能なテキストを指定します。|
|**表示領域**|この一覧を表示するために使用できるグループの 1 つを選択します。 使用可能なオプションは **詳細** (*共通* グループ用)、**マーケティング**、**営業**、および **サービス** です。 |
|**表示順序**|ナビゲーション アイテムが選択した表示領域のどこに含まれるかを制御します。 指定できる値の範囲は 10,000 から始まります。 値の小さいナビゲーション ウィンドウ項目は、値の大きい他の関係よりも上に表示されます。|

<!-- TODO: Not sure whether Display Area or Display Order are still used anymore. Might only be used in the Outlook client?-->

#### <a name="display-options"></a>表示オプション

これらは、使用可能な表示オプションです。

|オプション|説明|
|--|--|
|**表示しない**|この関連付けの関連エンティティを表示しません。|
|**カスタム ラベルを使用する**|このオプションを選択すると、**カスタム ラベル** フィールドが有効になり、複数名の代わりに使用されるローカライズ可能なテキストを指定できます。|
|**複数形の名前を使用する**|関連するエンティティに定義した複数形の表示名を使用します。|

### <a name="searchable"></a>[検索可能]

モデル駆動型アプリで関連付けを**高度な検索**から非表示にするには、**検索可能**フィールドを**いいえ**に設定します。

## <a name="delete-relationships"></a>関連付けの削除

[エンティティの関連付けを表示](#view-entity-relationships)している間、削除するエンティティの関連付けを選択し、![削除コマンド](media/delete.gif) コマンドをクリックします。

関連付けを削除すると、作成した関連付けエンティティも削除されます。 関連付けを使用してエンティティを接続するすべてのデータが失われます。

### <a name="see-also"></a>関連項目

[多対多 (N:N) のエンティティの関連付けを作成する](create-edit-nn-relationships.md)<br />
[PowerApps ポータルを使用して Common Data Service に多対多のエンティティー リレーションシップを作成する](create-edit-nn-relationships-portal.md)<br />
[1:N (一対多) または N:1 (多対一) のエンティティの作成および編集](create-edit-1n-relationships.md)
