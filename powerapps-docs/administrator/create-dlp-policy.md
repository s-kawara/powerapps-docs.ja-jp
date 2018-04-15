---
title: データ損失防止 (DLP) ポリシーを作成するクイック スタート | Microsoft Docs
description: このクイック スタートでは、PowerApps でデータ損失防止 (DLP) ポリシーを作成する方法について説明します
services: powerapps
suite: powerapps
documentationcenter: na
author: SKjerland
manager: kfile
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/21/2018
ms.author: sharik
ms.openlocfilehash: 651510bbe4ed71dbdb267ebee04e10ea13d36e15
ms.sourcegitcommit: 59785e9e82da8f5bd459dcb5da3d5c18064b0899
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/22/2018
---
# <a name="quickstart-create-a-data-loss-prevention-dlp-policy"></a>クイック スタート: データ損失防止 (DLP) ポリシーを作成する
PowerApps では、組織内のデータを保護するために、共有できるコンシューマー コネクタ固有のビジネス データを定義したポリシーを作成して適用することができます。 データの共有方法を定義するこれらのポリシーは、データ損失防止 (DLP) ポリシーと呼ばれます。 DLP ポリシーを使用すると、組織全体のデータの管理方法を統一し、重要なビジネス データがソーシャル メディア サイトなどのコネクタに誤って公開される問題を防ぐことができます。

このクイック スタートでは、Common Data Service および SharePoint データベースに格納されているデータが Twitter に公開されないように防止する DLP ポリシーの作成方法について説明します。

## <a name="prerequisites"></a>前提条件
このクイック スタートを実行するには、次の項目が必要です。
* PowerApps プラン 2 または Flow プラン 2 のいずれか。 また、[PowerApps プラン 2 無料試用版](https://web.powerapps.com/signup?redirect=marketing&email=)にサインアップすることもできます。
* PowerApps 環境管理者または Azure Active Directory テナント管理者のアクセス許可、および少なくとも 1 つの環境へのアクセス許可。 詳細については、[PowerApps の環境の管理](environments-administration.md)に関するページを参照してください。

## <a name="sign-in-to-the-powerapps-admin-center"></a>PowerApps 管理センターにサインインする
[https://admin.powerapps.com]([https://admin.powerapps.com) で管理センターにサインインします。

## <a name="create-a-dlp-policy"></a>DLP ポリシーを作成する
1. ナビゲーション ウィンドウで、**[データ ポリシー]**、**[新しいポリシー]** の順にクリックまたはタップします。

    ![](./media/create-dlp-policy/new-data-policy.png)
2. データ ポリシー名に「**Secure Data Access for Contoso**」と入力します。
3. **[環境]** タブで、ドロップダウン リストから環境を選択し、**[続行]** をクリックまたはタップします。

    ![](./media/create-dlp-policy/select-environment.png)
4. **[データ グループ]** タブの **[Business data only]\(ビジネス データのみ\)** で、**[追加]** をクリックまたはタップします。

    ![](./media/create-dlp-policy/data-groups.png)
5. **[コネクタの追加]** ウィンドウで、**[Common Data Service]** と **[SharePoint]** を選択します (必要に応じて下にスクロールするか、検索します)。次に **[コネクタの追加]** をクリックまたはタップし、**[Business data only]\(ビジネス データのみ\)** データ グループに追加します。

    ![](./media/create-dlp-policy/add-connectors.png)

    コネクタは一度に 1 つのデータ グループにのみ存在することができます。既定では、**[No business data allowed]\(ビジネス データは禁止\)** グループに追加されます。 Common Data Service と SharePoint を **[Business data only]\(ビジネス データのみ\)** グループに移動すると、ユーザーはこれらの 2 つのコネクタを、**[No business data allowed]\(ビジネス データは禁止\)** グループのいずれかのコネクタと組み合わせたフローとアプリを作成できなくなります。
6. **[ポリシーの保存]** をクリックします。

    ![](./media/create-dlp-policy/save-policy.png)

Secure Data Access for Contoso ポリシーが作成され、データ損失防止ポリシーの一覧に表示されます。 Twitter コネクタは **[No business data allowed]\(ビジネス データは禁止\)** データ グループ内にあるため、このポリシーで Common Data Service と SharePoint が Twitter とデータを共有しないようにします。

管理者は DLP ポリシーの一覧を組織と共有して、ユーザーがアプリを作成する前にポリシーを認識できるようにすることをお勧めします。

## <a name="next-steps"></a>次の手順
このクイック スタートでは、重要なビジネス データが誤って Twitter などのコネクタに公開されないように防止する DLP ポリシーを作成する方法について説明しました。 DLP ポリシーの詳細については、管理方法に関する記事を参照してください。

> [!div class="nextstepaction"]
> [データ損失防止 (DLP) ポリシーの管理](prevent-data-loss.md)
