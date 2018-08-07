---
title: データ損失防止 (DLP) ポリシーを作成する | Microsoft Docs
description: このクイック スタートでは、PowerApps でデータ損失防止 (DLP) ポリシーを作成する方法について説明します
author: jimholtz
ms.service: powerapps
ms.component: pa-admin
ms.topic: quickstart
ms.date: 03/30/2018
ms.author: jimholtz
ms.openlocfilehash: 49898aed97e2361704c88bcc1cd098a8fc0f101e
ms.sourcegitcommit: 2e7b621066cdc3e7be329d5213ecfee0b4223641
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/30/2018
ms.locfileid: "39349457"
---
# <a name="create-a-data-loss-prevention-dlp-policy"></a>データ損失防止 (DLP) ポリシーを作成する
PowerApps では、組織内のデータを保護するために、共有できるコンシューマー コネクタ固有のビジネス データを定義したポリシーを作成して適用することができます。 データの共有方法を定義するこれらのポリシーは、データ損失防止 (DLP) ポリシーと呼ばれます。 DLP ポリシーを使用すると、組織全体のデータの管理方法を統一し、重要なビジネス データがソーシャル メディア サイトなどのコネクタに誤って公開される問題を防ぐことができます。

このトピックでは、Common Data Service および SharePoint データベースに格納されているデータが Twitter に公開されないように防止する、単一環境用の DLP ポリシーの作成方法について説明します。

## <a name="prerequisites"></a>前提条件
この手順を実行するには、次の項目のいずれか **1 つ**が必要です。
* Azure Active Directory テナント管理者のアクセス許可
* Office 365 全体管理者のアクセス許可
* PowerApps 環境管理者のアクセス許可に加えて、PowerApps プラン 2、Microsoft Flow プラン 2、または [PowerApps プラン 2 試用版](https://web.powerapps.com/signup?redirect=marketing&email=)のライセンス

詳細については、「[PowerApps での環境の管理](environments-administration.md)」を参照してください。

## <a name="sign-in-to-the-powerapps-admin-center"></a>PowerApps 管理センターにサインインする
[https://admin.powerapps.com]([https://admin.powerapps.com) で管理センターにサインインします。

## <a name="create-a-dlp-policy"></a>DLP ポリシーを作成する
1. ナビゲーション ウィンドウで、**[データ ポリシー]**、**[新しいポリシー]** の順にクリックまたはタップします。

    ![](./media/create-dlp-policy/new-data-policy.png)
2. **[データ ポリシー名]** フィールドには、ポリシーが作成された日付と時刻に基づく名前が自動的に設定されています。 これを、**Secure Data Access for Contoso** に置き換えます。

    ![](./media/create-dlp-policy/policy-name.png)
3. **[環境]** タブのオプションは、環境管理者かテナント管理者かによって異なります。環境管理者の場合は、ドロップダウン リストから環境を選択し、**[続行]** をクリックまたはタップします。

    ![](./media/create-dlp-policy/select-environment.png)

    テナント管理者の場合は、1 つまたは複数の環境、またはテナント内のすべての環境 (試用版ライセンスを使って作成された環境を含む) に適用される DLP ポリシーを作成できます。 このトピックでは、**[選択した環境のみに適用]** をクリックまたはタップし、ドロップダウン リストから環境を選んで、**[続行]** をクリックまたはタップします。

    ![](./media/create-dlp-policy/select-environment-tenant.png)

    環境 DLP ポリシーではテナント全体の DLP ポリシーをオーバーライドできないことに注意してください。
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
このトピックでは、重要なビジネス データが誤って Twitter などのコネクタに公開されないように防止する、単一環境用の DLP ポリシーを作成する方法について説明しました。 DLP ポリシーの詳細については、管理方法に関する記事を参照してください。

> [!div class="nextstepaction"]
> [データ損失防止 (DLP) ポリシーの管理](prevent-data-loss.md)
