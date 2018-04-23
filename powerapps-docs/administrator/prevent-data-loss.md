---
title: データ損失防止 (DLP) ポリシーの管理 | Microsoft Docs
description: PowerApps のデータ損失防止ポリシーを管理する方法のチュートリアル。
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
ms.openlocfilehash: f02e9023deb2bc0d11e9d94414f9e78651cab2b5
ms.sourcegitcommit: aa2d0166dccb38100183c093f293233b46f3669d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2018
---
# <a name="manage-data-loss-prevention-dlp-policies"></a>データ損失防止 (DLP) ポリシーの管理
組織のデータは、その成功に不可欠です。 そのデータは、意思決定のために容易に利用できる必要がありますが、アクセスすべきではないユーザーと共有されることがないように保護する必要があります。 PowerApps では、このデータを保護するために、共有できるコンシューマー コネクタ固有のビジネス データを定義したデータ損失防止 (DLP) ポリシーを作成して適用することができます。 たとえば、PowerApps を使用している組織で、SharePoint に保存されているビジネス データは Twitter フィードに自動的に発行したくないとします。

DLP ポリシーの作成、編集、または削除には、環境管理者または Azure Active Directory テナント管理者のアクセス許可が必要です。 詳細については、「[PowerApps での環境の管理](environments-administration.md)」を参照してください。

DLP ポリシーの作成手順については、「[Quickstart: Create a data loss prevention (DLP) policy](create-dlp-policy.md)」(クイック スタート: データ損失防止 (DLP) ポリシーを作成する) を参照してください。

## <a name="find-a-dlp-policy"></a>DLP ポリシーを検索する
1. [https://admin.poweraps.com]([https://admin.powerapps.com) で管理センターにサインインします。
2. ナビゲーション ウィンドウで、**[データ ポリシー]** をクリックまたはタップします。 ポリシー数が多い場合は、**[検索]** ボックスを使用して特定の DLP ポリシーを見つけます。

    ![](./media/prevent-data-loss/data-policies.png)

## <a name="edit-a-dlp-policy"></a>DLP ポリシーを編集する
1. データ損失防止ポリシーの一覧で、編集するポリシーの横にある鉛筆アイコンをクリックまたはタップします。

    ![サインイン](./media/prevent-data-loss/3.png)
2. 変更を加え、**[ポリシーを保存]** をクリックまたはタップします。

    > [!NOTE]
    > 環境 DLP ポリシーでは、テナント全体の DLP ポリシーを上書きできません。
    >
    >

    変更を確認するには、データ損失防止ポリシーの一覧で DLP ポリシーを見つけてクリックまたはタップし、そのプロパティを確認します。

## <a name="delete-a-dlp-policy"></a>DLP ポリシーを削除する
1. データ損失防止ポリシーの一覧で、削除するポリシーの横にあるごみ箱アイコンをクリックまたはタップします。

    ![サインイン](./media/prevent-data-loss/3-delete.png)
4. 確認のダイアログ ボックスで、**[削除]** をクリックまたはタップします。

    ポリシーが削除され、データ損失防止ポリシーの一覧に表示されなくなります。

## <a name="next-steps"></a>次の手順
* [環境に関する詳細](environments-administration.md)
* [Microsoft PowerApps の詳細](../maker/canvas-apps/getting-started.md)
