---
title: PowerApps ポータルを使用した代替キーの定義 | MicrosoftDocs
description: PowerApps ポータルを使用して代替キーを定義する方法を説明します
ms.custom: ''
ms.date: 05/31/2018
ms.reviewer: ''
ms.service: crm-online
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
# <a name="define-alternate-keys-using-powerapps-portal"></a>PowerApps ポータルを使用した代替キーの定義

[PowerApps ポータル](https://web.powerapps.com/?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc)では、アプリ用 Common Data Service でエンティティの代替キーを表示および作成する簡単な方法が提供されます。

ポータルでは一般的なオプションのほどんとを構成できますが、特定のオプションはソリューション エクスプローラーを使用してのみ設定できます。 <br />詳細: 
- [レコードを参照する代替キーの定義](define-alternate-keys-reference-records.md)
- [ソリューション エクスプローラーを使用した代替キーの定義](define-alternate-keys-solution-explorer.md)

## <a name="view-alternate-keys"></a>代替キーを表示

1. [PowerApps ポータル](https://web.powerapps.com/?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc)から、**モデル駆動型**または**キャンバス**設計モードを選択します。
2. **データ** > **エンティティ**を選択し、表示するエンティティを選択します。
3. **キー**を選択すると、定義された代替キーのリストが表示されます。

    ![代替キーを表示](media/view-alternate-keys-portal.png)

## <a name="create-an-alternate-key"></a>代替キーの作成

1. [代替キーを表示](#view-alternate-keys)しているとき、**キーを追加**を選択します。
2. パネルを使用して**表示名**を設定し、代替キーの作成に使用するフィールドを選択します。

    **名前**フィールドは、表紙名に基づいて設定されます。

    ![代替キー定義の例](media/alternate-key-account-number-sic-code.png)

1. **完了**を選択してパネルを閉じます。
2. 代替キーを作成するには、**エンティティの保存**をクリックします。

> [!NOTE]
> 代替キーはすぐに使用できません。 エンティティを保存して代替キーをサポートするデータベースのインデックスを作成すると、システム ジョブが開始されます。

## <a name="delete-an-alternate-key"></a>代替キーの削除

[代替キーを表示](#view-alternate-keys)しているとき、削除するキーを選択し、コマンド バーから **Delete キー**を選択します。

### <a name="see-also"></a>関連項目

[レコードを参照する代替キーの定義](define-alternate-keys-reference-records.md)<br />
[ソリューション エクスプローラーを使用した代替キーの定義](define-alternate-keys-solution-explorer.md)<br />
[開発者向けドキュメント: エンティティの代替キーを定義](/dynamics365/customer-engagement/developer/define-alternate-keys-entity)
