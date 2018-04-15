---
title: 環境の管理 | Microsoft Docs
description: 環境の作成、名前の変更、削除、セキュリティなどを含む、PowerApps での環境の管理
services: powerapps
suite: powerapps
documentationcenter: na
author: manasmams
manager: kfile
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/21/2018
ms.author: manasma
ms.openlocfilehash: 0a6080b7ceb14de14b7ad6ae2f851843bac0c73b
ms.sourcegitcommit: 59785e9e82da8f5bd459dcb5da3d5c18064b0899
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/22/2018
---
# <a name="administer-environments-in-powerapps"></a>PowerApps での環境の管理
[PowerApps 管理センター][1]では、作成した環境、および環境管理者ロールまたはシステム管理者ロールが付与されている環境を管理します。 管理センターから、次の管理操作を実行できます。

* 環境を作成する。
* 環境の名前を変更する。
* Environment Admin ロールまたは Environment Maker ロールのいずれかからユーザーまたはグループを追加または削除する。
* 環境に Common Data Service データベースをプロビジョニングする。
* データ損失防止ポリシーを設定する。
* データベースのセキュリティ ポリシーを設定する (オープン ポリシーまたは制限付きポリシー)。
* Azure AD テナントのグローバル管理者ロールのメンバー (Office 365 のグローバル管理者を含む) も、テナントに作成したすべての環境を管理し、テナント全体のポリシーを設定できます。

## <a name="access-the-powerapps-admin-center"></a>PowerApps 管理センターにアクセスする
PowerApps 管理センターにアクセスするには、次のいずれかを行います。

* [admin.powerapps.com][1] に直接アクセスする。

* [powerapps.com][2] に移動してから、ナビゲーション ヘッダーで歯車アイコンを選択する。

    ![](./media/environment-admin/powerapps-gear-dropdown.png)

PowerApps 管理センターで環境を管理するには、次のロールのいずれかが必要です。

* 環境の環境管理者ロールまたはシステム管理者ロール

* Azure AD または Office 365 テナントのグローバル管理者ロール

また、管理センターにアクセスするには PowerApps プラン 2 または Flow プラン 2 が必要です。 詳細については、[PowerApps の価格に関するページ][3]を参照してください。

> [!IMPORTANT]
> PowerApps 管理センターで行う変更はすべて[フロー管理センター][4]に影響し、その反対も同様です。

## <a name="create-an-environment"></a>環境の作成
環境を作成する方法については、「[クイック スタート: 環境を作成する](create-environment.md)」を参照してください。

## <a name="view-your-environments"></a>環境を表示する
管理センターを開くと、既定で [環境] タブが表示され、お客様が環境管理者である環境が (下図のように) すべて一覧表示されます。

![](./media/environment-admin/environment-list-new.png)

お客様が Azure AD のグローバル管理者ロールのメンバーまたは Office 365 テナントである場合、自動的にテナント内でユーザーが作成したすべての環境の環境管理者となるため、これらの環境がすべて表示されます。

## <a name="rename-your-environment"></a>環境の名前を変更する
1. [PowerApps 管理センター][1]を開き、一覧から名前を変更する環境を検索して、その環境をクリックまたはタップします。

    ![](./media/environment-admin/environment-list-updated3.png)
 
2. **[詳細]** をクリックまたはタップします。

    ![](./media/environment-admin/environment-rename-details-2.png)
3. **[名前]** テキスト ボックスで、新しい名前を入力してから **[保存]** をクリックまたはタップします。

    ![](./media/environment-admin/environment-rename-2.png)

    環境でデータベースを作成した場合、このオプションは表示されません。 Dynamics 365 管理センターで、**[詳細]** タブのリンクをクリックして、環境の名前を変更することができます。

    ![](./media/environment-admin/Delete-D365AdminCenter.png)


## <a name="delete-your-environment"></a>環境を削除する
1. [PowerApps 管理センター][1]で、削除する環境をクリックまたはタップします。

    ![](./media/environment-admin/environment-list-updated3.png)
2. **[詳細]** をクリックまたはタップします。

    ![](./media/environment-admin/environment-rename-details-2.png)
3. **[環境の削除]** をクリックまたはタップして、環境を削除します。

    ![](./media/environment-admin/delete-environment-2.png)


## <a name="create-a-common-data-service-database-for-an-environment"></a>環境に Common Data Service データベースを作成する
環境にデータベースがない場合、環境管理者は次の手順に従って、[PowerApps 管理センター][1]でデータベースを作成できます。 PowerApps プラン 2 のライセンスを持つユーザーのみが Common Data Service データベースを作成できます。

1. 環境のテーブルで、環境を選択します。

    ![](./media/environment-admin/choose-environment-updated.png)
2. **[詳細]** タブを選択します。
3. **[データベースの作成]** を選択します。

    ![](./media/environment-admin/Create-DB-From-Details.png)


データベースを作成したら、セキュリティ モデルを選択します。 詳細については、「[Configure database security (データベース セキュリティの構成)](database-security.md)」を参照してください。

## <a name="manage-security-for-your-environments"></a>環境のセキュリティを管理する

### <a name="environment-permissions"></a>環境のアクセス許可
環境では、Azure AD テナント内のユーザーはすべてその環境のユーザーです。 ただし、より高い特権のロールを割り当てるには、ユーザーを特定の環境ロールに追加する必要があります。 環境には、環境内でのアクセス許可を提供する 2 つの組み込みの役割があります。

* **環境管理者**ロール (または**システム管理者**ロール) は、環境に対して、以下を含むすべての管理操作を実行できます。
    * 環境管理者ロールまたは環境作成者ロールのいずれかからユーザーを追加または削除する。

    * 環境に Common Data Service データベースをプロビジョニングする。

    * 環境内で作成されたすべてのリソースを表示し、管理する。

    * データ損失防止ポリシーを設定する。 詳細については、[データ損失防止ポリシー](prevent-data-loss.md)に関するページを参照してください。

  > [!NOTE]
  > 環境にデータベースが含まれている場合は、**環境管理者**ロールではなく、**システム管理者**ロールをユーザーに割り当てる必要があります。

* **Environment Maker** ロールは、アプリ、接続、カスタム コネクタ、ゲートウェイ、および Microsoft Flow を使用するフローなど、環境内のリソースを作成できます。 環境作成者は、環境で構築したアプリを組織内の他のユーザーに配布することもできます。 個々 のユーザー、セキュリティ グループ、または組織内のすべてのユーザーとアプリを共有できます。 詳細については、[PowerApps でのアプリの共有](../maker/canvas-apps/share-app.md)に関するページを参照してください。

環境ロールにユーザーまたはセキュリティ グループを割り当てるために、環境管理者は次の手順を [PowerApps 管理センター][1]で実行できます。

1. 環境のテーブルで、環境を選択します。

    ![](./media/environment-admin/choose-environment-updated.png)
2. **[セキュリティ]** タブを選択します。
3. 環境でデータベースが作成されていない場合は、次の手順を実行します。

    a. **環境管理者**ロールまたは**環境作成者**ロールのいずれかを選択します。

    ![](./media/environment-admin/choose-environment-role.png)

    b. Azure Active Directory 内の 1 人以上のユーザーまたは 1 つ以上のセキュリティ グループの名前を指定します。または、組織全体を追加することを指定します。

    ![](./media/environment-admin/enter-name.png)

    c. **[保存]** を選択して環境ロールに対して割り当てを更新します。

4. 環境でデータベースが作成されている場合は、次の手順を実行します。

    a. Dynamics 365 の環境ロールを管理するリンクをクリックします。

    ![](./media/environment-admin/Security-Link-D365.png)

    b. 環境 / インスタンス内のユーザーの一覧からユーザーを選択します。

    ![](./media/environment-admin/D365-Select-User.png)

    c. ロールをユーザーに割り当てます。

    ![](./media/environment-admin/D365-Assign-Role.png)

    d. **[OK]** を選択して、環境ロールへの割り当てを更新します。


> [!NOTE]
> これらの環境のロールに割り当てられているユーザーまたはグループには、環境のデータベース (存在する場合) へのアクセス権が自動的に付与されるわけではありません。データベース所有者が個別にアクセス権を付与する必要があります。 詳細については、「[Configure database security (データベース セキュリティの構成)](database-security.md)」を参照してください。  
>
>

### <a name="database-security"></a>データベース セキュリティ
データベース スキーマを作成および変更し、環境内でプロビジョニングされてデータベース内で格納されているデータに接続するための機能は、データベースのユーザー ロールとアクセス許可セットによって制御されます。 環境のデータベース向けのユーザー ロールおよびアクセス許可セットは、**[セキュリティ]** タブの **[ユーザー ロール]** セクションおよび **[アクセス許可セット]** セクションから管理できます。詳細については、「[Configure database security (データベース セキュリティの構成)](database-security.md)」を参照してください。

![](./media/environment-admin/D365-Assign-Role.png)

## <a name="data-policies"></a>データ ポリシー
アクセス権のない対象ユーザーと共有されないように、組織のデータを保護する必要があります。 このデータを保護するために、どのコンシューマー サービス/コネクタ固有のビジネス データを共有できるかを定義するポリシーを作成して適用することができます。 データの共有方法を定義するポリシーは、データ損失防止 (DLP) ポリシーと呼ばれます。 環境の DLP ポリシーは、[PowerApps 管理センター][1]の **[データ ポリシー]** セクションで管理できます。  詳細については、[データ損失防止ポリシー](prevent-data-loss.md)に関するページを参照してください。

![](./media/environment-admin/data-policies.png)

## <a name="frequently-asked-questions"></a>よく寄せられる質問
### <a name="how-many-environments-can-i-create"></a>環境はいくつ作成できますか。
各ユーザーは、ライセンスに応じて、最大で 2 つの試用環境と 2 つの運用環境を作成することができます。

### <a name="how-many-databases-can-i-provision"></a>データベースはいくつプロビジョニングできますか。
各ユーザーは、ライセンスに応じて、2 つの試用環境と 2 つの運用環境でデータベースをプロビジョニングできます。 これらの環境では、ユーザーは**環境管理者**である必要があります。

### <a name="can-i-rename-an-environment"></a>環境の名前は変更できますか。
はい、この機能は、PowerApps 管理センターから使用できます。 詳細については、[環境の管理](environments-administration.md#rename-your-environment)に関するページをご覧ください。

### <a name="can-i-delete-an-environment"></a>環境を削除することはできますか。
はい、この機能は、PowerApps 管理センターから使用できます。 詳細については、[環境の管理](environments-administration.md#delete-your-environment)に関するページをご覧ください。

### <a name="as-an-environment-admin-can-i-view-and-manage-all-resources-apps-flows-apis-etc-for-an-environment"></a>環境管理者として、環境のすべてのリソース (アプリ、フロー、API など) を表示および管理することはできますか。
はい、アプリと環境のフローを表示する機能は、PowerApps 管理センターから使用できます。 詳細については、[アプリの表示](admin-view-apps.md)に関するページをご覧ください。

### <a name="which-license-includes-common-data-service"></a>Common Data Service は、どのライセンスに含まれますか。
PowerApps プラン 2 に含まれます。  このライセンスを含むすべてのプランに関する詳細については、[PowerApps の価格ページ][3]を参照してください。

<!--Reference links in article-->
[1]: https://admin.powerapps.com
[2]: https://web.powerapps.com
[3]: https://powerapps.microsoft.com/pricing/
[4]: https://admin.flow.microsoft.com
