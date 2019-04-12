---
title: PowerApps ポータルを使用して Common Data Service で多対多のエンティティの関連付けを作成する | MicrosoftDocs
description: 'N:N (多対多) の関連付けを作成する方法を学習する'
ms.custom: ''
ms.date: 06/11/2018
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

# <a name="create-many-to-many-entity-relationships-in-common-data-service-using-powerapps-portal"></a>PowerApps ポータルを使用して Common Data Service で多対多のエンティティ関係を作成する

[PowerApps ポータル](https://web.powerapps.com/?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc) では Common Data Service の多対多のエンティティの関連付けを簡単に作成および編集できます。

ポータルでは一般的なオプションのほどんとを構成できますが、特定のオプションはソリューション エクスプローラーを使用してのみ設定できます。 詳細: 
- [N:N (多対多) のエンティティの関連付けを作成する](create-edit-nn-relationships.md)
- [ソリューション エクスプローラーを使用して Common Data Service で N:N (多対多) のエンティティ関係を作成する](create-edit-nn-relationships-solution-explorer.md)

## <a name="view-many-to-many-entity-relationships"></a>多対多のエンティティの関連付けを表示する

1. [PowerApps ポータル](https://web.powerapps.com/?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc)から、**モデル駆動型**または**キャンバス**設計モードを選択します。
2. **データ** > **エンティティ** を選択し、表示する関連付けを持つエンティティを選択します。
3. **関連付け** タブでは、次のビューを選択できます。 

 |ビュー|説明|
 |--|--|
 |**すべて**| エンティティのすべての関連付けを表示する|
 |**ユーザー定義**|エンティティのカスタム関連付けのみを表示する|
 |**既定**|エンティティの標準関連付けのみを表示する|
<!-- TODO: What is the actual difference between All and Default? -->

![アカウント エンティティの関連付け](media/view-account-relationships-portal.png)

多対多の関連付けには**多対多**の**関連付けの種類**があります。

> [!NOTE]
> 表示するエンティティには、**多対多**の関連付けがない場合があります。

## <a name="create-relationships"></a>関連付けを作成する

[エンティティの関連付けを表示](#view-many-to-many-entity-relationships)しているときに、コマンド バーで**関連付けを追加**を選択し、**多対多**を選択します。

![関連付けの種類を選択する](media/add-relationship-menu-portal.png)

**多対多**ウィンドウで、現在のエンティティに関連付けするエンティティを選択します。

![選択した取引先のエンティティを使用した多対多のパネル](media/many-to-many-panel-1.png)

**関連付けの名前** および **関連付けのエンティティの名前**フィールドを表示するために、**そのほかのオプション**を選択します。

![そのほかのオプションを選択した多対多のパネル](media/many-to-many-panel-2.png)

これらのフィールドの値は、選択されたエンティティに基づいて自動的に生成されます。

> [!NOTE]
> 同じ 2 種類のエンティティに複数の**多対多**の関連付けを作成する場合は、生成した**関連付けの名前**および**関連付けのエンティティの名前**フィールドを編集して一意になるようにします。

**多対多**パネルを閉じるには、**OK** を選択します。 関連付けは、エンティティへの変更を保存すると作成されます。 

保存すると、[PowerApps ポータル](https://web.powerapps.com/?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc)を使用して変更することはできません。 モデル駆動型アプリの関連付けのプロパティを編集するには、[ソリューション エクスプローラー](create-edit-nn-relationships-solution-explorer.md)を使用します。

## <a name="delete-relationships"></a>関連付けの削除

[エンティティの関連付けを表示](#view-many-to-many-entity-relationships)しているときに、削除する関連付けを選択します。

![エンティティの関連付けを削除する](media/delete-entity-relationship-portal.png)

省略記号 (**...**) を選択するときに、コマンド バーまたは行ショートカット メニューの **関連付けの削除** コマンドを使用することができます。

多対多の関連付けを削除すると、作成した関連付けのエンティティも削除されます。 関連付けを使用してエンティティを接続するすべてのデータが失われます。

### <a name="see-also"></a>関連項目

[N:N (多対多) のエンティティの関連付けを作成する](create-edit-nn-relationships.md)<br />
[ソリューション エクスプローラーを使用して Common Data Service で N:N (多対多) のエンティティ関係を作成する](create-edit-nn-relationships-solution-explorer.md)
