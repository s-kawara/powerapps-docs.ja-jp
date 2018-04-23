---
title: Common Data Service データベースの作成 | Microsoft Docs
description: Common Data Service データベースを作成します。
services: powerapps
documentationcenter: na
author: manasmams
manager: kfend
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/21/2018
ms.author: manasma
ms.openlocfilehash: 68ce23ae4b4a961a69cc60173b4f98ec18f05dd2
ms.sourcegitcommit: aa2d0166dccb38100183c093f293233b46f3669d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2018
---
# <a name="create-a-common-data-service-database"></a>Common Data Service データベースの作成
データベースの作成とアプリの構築には、Common Data Service をデータ ストアとして使用できます。 独自のカスタム エンティティを作成することも、事前定義されたエンティティを使用することもできます。 データベースを作成するには、まず環境を作成するか、**環境管理者**として既存の環境に割り当てられる必要があります。さらに、適切なライセンスが割り当てられている必要があります。 Common Data Service を使用するためのプランの購入については、[価格に関する情報](pricing-billing-skus.md)を参照してください。

データベースを作成するにはさまざまな方法があります。

* PowerApps 管理センターで作成する
* powerapps.com の **[エンティティ]** ウィンドウで作成する

## <a name="create-a-database-in-the-admin-center"></a>管理センターでのデータベースの作成
1. [管理センター](https://admin.powerapps.com)で、左側のナビゲーション ウィンドウの **[環境]** をクリックします。
    
2. データベースを作成する環境を選択します。
    
    ![](./media/create-database/environment-list-new.png)

3. **[詳細]** タブの **[データベースの作成]** をクリックします。 
    
    ![](./media/create-database/Create-DB-From-Details.png)

4. 通貨と言語を選択してデータベースの作成を続行します。 
    
    ![](./media/create-database/DB-Choose-options.png)



## <a name="create-a-database-in-the-entities-pane-of-powerappscom"></a>powerapps.com の [エンティティ] ウィンドウでのデータベースの作成
1. [powerapps.com](https://web.powerapps.com) で、**[データ]** セクションを展開し、左側のナビゲーション ウィンドウで **[エンティティ]** をクリックまたはタップします。

2. **[データベースの作成]** をクリックしてデータベースを作成します。

    ![](./media/create-database/Create-DB-From-Entities.png)


## <a name="security-model-for-the-databases"></a>データベースのセキュリティ モデル
データベースが作成されると、環境ロールが割り当てられているユーザーは、その特権を引き続き維持します。  
    **環境管理者**ロールが割り当てられていたユーザーには、**システム管理者**ロールが割り当てられます。 **環境作成者**が割り当てられていたユーザーは、引き続き同じロールを持ちます。

事前に定義されたロールに追加のユーザーを割り当てることができます。また、[ユーザー定義ロール][1]を作成することもできます。 詳細については、[データベース セキュリティ](database-security.md)に関するページを参照してください。

> [!NOTE]
> データベースの作成時に、環境管理者ロールまたは環境作成者ロールが割り当てられたセキュリティ グループは使用されなくなります。 現在、データベースでのアクセス許可の割り当ては AAD セキュリティ グループをサポートしていません。


## <a name="license-and-security-permissions"></a>ライセンスとセキュリティ アクセス許可
データベースを作成するには、選択した環境の管理者であり、適切なライセンスが割り当てられている必要があります。 そのような環境では、**[セキュリティ]** タブを使用して、他のユーザーのセキュリティ アクセス許可をさらに構成できます。詳細については、「[Configure database security (データベース セキュリティの構成)](database-security.md)」と「[Security model (セキュリティ モデル)](https://docs.microsoft.c../maker/common-data-service/entity-reference/security-model)」を参照してください。

## <a name="privacy-notice"></a>プライバシーに関する声明
Microsoft PowerApps の Common Data Service では、Microsoft の診断システムにカスタム エンティティとフィールド名を収集して格納します。  収集した情報は、お客様向けの Common Data Service の改善に使用します。 作成者が作成するエンティティとフィールド名は、Microsoft PowerApps コミュニティ全体で共通するシナリオを理解したり、組織に関するスキーマなどの、サービスの標準エンティティの対象範囲のギャップを確認したりする場合に役立ちます。 このエンティティに関連するデータベース テーブルのデータに、Microsoft がアクセスまたは使用することはありません。また、データベースがプロビジョニングされているリージョン外にデータがレプリケートされることもありません。 ただし、カスタム エンティティとフィールド名はリージョン間でレプリケートされ、Microsoft のデータ保持ポリシーに基づいて削除される場合があります。 Microsoft はお客様のプライバシーを尊重いたします。詳細については、[Trust Center](https://www.microsoft.com/trustcenter/Privacy/default.aspx) を参照してください。


<!--Reference links in article-->
[1]: https://technet.microsoft.com/library/dn531130.aspx
