---
title: カスタム エンティティ作成のクイック スタート | Microsoft Docs
description: カスタム エンティティを別のエンティティから、または最初から作成するクイック スタートです。
services: powerapps
documentationcenter: na
author: clwesene
manager: kfile
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2018
ms.author: clwesene
ms.openlocfilehash: d26b7a086e75a52d9da3369196f59d3fb439f50b
ms.sourcegitcommit: 59785e9e82da8f5bd459dcb5da3d5c18064b0899
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/22/2018
---
# <a name="quickstart-create-a-custom-entity"></a>クイック スタート: カスタム エンティティを作成する
組織に固有のデータを格納するカスタム エンティティを作成することができます。 エンティティを参照するアプリを開発すると、そのデータを表示できるようになります。 エンティティの作成後、[そのフィールドを作成または編集](data-platform-manage-fields.md)したり、[エンティティ間のリレーションシップを構築](data-platform-entity-lookup.md)したりすることができます。

ここではカスタム エンティティを手動で作成する方法を示しますが、Power Query を使って既存のデータに基づくエンティティを作成することもできます。 詳しくは、[Power Query を使った新しいエンティティの作成](data-platform-cds-newentity-pq.md)に関するページをご覧ください。

> [!NOTE]
> エンティティを作成する前に、[エンティティのリファレンス](../../developer/common-data-service/reference/about-entity-reference.md)に関するページをご覧ください。 これらのエンティティには、アカウントや連絡先などの一般的なシナリオが含まれています。 これらのエンティティのいずれかが既に要件を満たしているか、わずかな変更のみで要件を満たす場合は、そのエンティティを使用することで時間を節約することができます。

## <a name="create-an-entity"></a>エンティティの作成
1. [powerapps.com](https://web.powerapps.com) で、**[データ]** セクションを展開し、左側のナビゲーション ウィンドウで **[エンティティ]** をクリックまたはタップします。

    ![エンティティの詳細](./media/data-platform-cds-create-entity/entitylist.png "エンティティの一覧")

2. コマンド バーの **[新しいエンティティ]** をクリックまたはタップします。
3. **[表示名]** フィールドに、後でこのエンティティを参照するときに簡単に認識できる名前を入力します。 この名前は、このエンティティを使って作成されるフォーム、グラフ、他のオブジェクトでも使われます。 設定されるフィールドが他にも 2 つあることがわかります。

    * [表示名の複数形] - この名前は、PowerApps または Flow からこのエンティティを操作するとき、および Common Data Service WebAPI からエンティティの名前として、使われます。 複数形の名前は自動的に生成されますが、変更してもかまいません。
    * [名前] - これはエンティティの固有の名前であり、特殊文字またはスペースを含むことはできず、一意である必要があります。 また、この名前にはユーザーが環境を作成するときに設定したプレフィックスが含まれます。これは、作成したエンティティをエクスポートし、競合するエンティティ名がある他の環境に確実にインポートできるようにするために使われます。 このプレフィックスは、Common Data Service の既定のソリューションの発行元でプレフィックスを更新することで変更できます。

    > [!NOTE]
    > **[表示名]** フィールドはいつでも更新でき、アプリでの表示が変わります。**[名前]** フィールドは、変更すると既存のアプリに影響するので、エンティティを保存した後では変更できません。

    ![新しいエンティティ](./media/data-platform-cds-create-entity/newentitypanel.png "[新しいエンティティ] パネル")

4. **[次へ]** をクリックすると、エンティティの詳細ページに移動します。 すべてのエンティティには既定で最初に 1 つのフィールド [プライマリ名] が作成されます。このフィールドは、このエンティティに対してルックアップが作成されるときに使われます。 一般に、エンティティに格納されているデータの名前または主な説明を格納するために使う必要があります。

    > [!NOTE]
    > **[プライマリ名]** フィールドの名前と表示名は、エンティティを初めて保存する前に更新できます。 たとえば、このフィールドを "プライマリ名" ではなく "受講者名" にすることができます。

    ![エンティティの詳細](./media/data-platform-cds-create-entity/newentitydetails.png "新しいエンティティの詳細")

5. 省略可能: **[フィールドの追加]** をクリックして、エンティティにテキスト フィールドを追加します。 [新しいフィールド] パネルで、フィールドの **[表示名]** を入力し、データ型を選びます。 詳細については、[エンティティのフィールドの管理](data-platform-manage-fields.md)に関するページをご覧ください。

    ![新しいフィールド](./media/data-platform-cds-create-entity/newfieldpanel-2.png "[新しいフィールド] パネル")


6. **[完了]** をクリックしてフィールドを追加し、ステップ 5 を繰り返して他のフィールドを追加します。
7. **[エンティティの保存]** をクリックしてエンティティを保存し、アプリで使えるようにします。

    作成したエンティティが、データベース内のエンティティの一覧に表示されます。 作成したエンティティを表示するには、コマンド バーのフィルターを [既定] から [カスタム] に変更します。

## <a name="system-fields"></a>システム フィールド
すべてのエンティティにはシステム フィールドがあります。 これらのフィールドは、読み取り専用です。 そのため、変更したり削除したりすることはできません。値を割り当てることもできません。 既定では、システム フィールドはエンティティに存在していてもフィールドの一覧に表示されません。 すべてのフィールドを表示するには、コマンド バーにあるフィルターを **[既定]** から **[すべて]** に変更します。

エンティティに関連するメタデータについて詳しくは、「[Entity metadata](../../developer/common-data-service/entity-metadata.md)」(エンティティ メタデータ) をご覧ください。

## <a name="next-steps"></a>次の手順
* [エンティティのフィールドを管理する](data-platform-manage-fields.md)
* [エンティティ間のリレーションシップを定義する](data-platform-entity-lookup.md)
* [Common Data Service データベースを使用してアプリを生成する](../canvas-apps/data-platform-create-app.md)
* [Common Data Service データベースを使用してアプリを最初から作成する](../canvas-apps/data-platform-create-app-scratch.md)

## <a name="privacy-notice"></a>プライバシーに関する声明
Microsoft PowerApps の Common Data Service では、Microsoft の診断システムにカスタム エンティティとフィールド名を収集して格納します。  収集した情報は、お客様向けの Common Data Service の改善に使用します。 作成者が作成するエンティティとフィールド名は、Microsoft PowerApps コミュニティ全体で共通するシナリオを理解したり、組織に関するスキーマなどの、サービスの標準エンティティの対象範囲のギャップを確認したりする場合に役立ちます。 このエンティティに関連するデータベース テーブルのデータに、Microsoft がアクセスまたは使用することはありません。また、データベースがプロビジョニングされているリージョン外にデータがレプリケートされることもありません。 ただし、カスタム エンティティとフィールド名はリージョン間でレプリケートされ、Microsoft のデータ保持ポリシーに基づいて削除される場合があります。 Microsoft はお客様のプライバシーを尊重いたします。詳細については、[Trust Center](https://www.microsoft.com/trustcenter/Privacy/default.aspx) を参照してください。

