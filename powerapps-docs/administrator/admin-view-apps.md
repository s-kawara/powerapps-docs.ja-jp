---
title: 環境内で作成したアプリの一覧をダウンロードするクイック スタート | Microsoft Docs
description: このクイック スタートでは、環境内で作成したアプリの一覧をダウンロードする方法について説明します。
author: jimholtz
ms.service: powerapps
ms.component: pa-admin
ms.topic: quickstart
ms.date: 03/21/2018
ms.author: jimh
ms.openlocfilehash: d9c379ca95bb299c56639bb01803f45c1744d8f2
ms.sourcegitcommit: 91a102426f1bc37504142cc756884f3670da5110
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/26/2018
ms.locfileid: "34552601"
---
# <a name="quickstart-download-a-list-of-apps-created-in-your-environments"></a>クイック スタート: 環境内で作成したアプリの一覧をダウンロードする
環境管理者の場合、自分が管理している環境で作成したアプリの一覧を表示およびダウンロードすることができます。 365 グローバル管理者または Azure Active Directory テナント管理者は、組織内のすべての環境で作成されたアプリの一覧を表示およびダウンロードできます。

このクイック スタートでは、1 つの環境で作成されたアプリの一覧を .csv ファイルにダウンロードし、その一覧を Excel で表示する方法について説明します。

## <a name="prerequisites"></a>前提条件
 このクイック スタートを実行するには、次の項目が必要です。
 * PowerApps プラン 2 または Microsoft Flow プラン 2 のライセンス。 また、[PowerApps プラン 2 無料試用版](https://web.powerapps.com/signup?redirect=marketing&email=)にサインアップすることもできます。
 * PowerApps 環境管理者、Office 365 グローバル管理者、または Azure Active Directory テナント管理者のアクセス許可。 詳細については、[PowerApps の環境の管理](environments-administration.md)に関するページを参照してください。

## <a name="sign-in-to-the-powerapps-admin-center"></a>PowerApps 管理センターにサインインする
[https://admin.powerapps.com]([https://admin.powerapps.com) で管理センターにサインインします。

## <a name="download-the-list-of-apps"></a>アプリの一覧をダウンロードする
1. ナビゲーション ウィンドウで、**[環境]** をクリックまたはタップしてから、アプリの一覧をダウンロードする環境をクリックまたはタップします。

    ![ファイルと共有](./media/admin-view-apps/environment.png)
2. **[リソース]** タブで、**[アプリ]**、**[アプリの一覧のダウンロード]** の順にクリックまたはタップします。

    ![ファイルと共有](./media/admin-view-apps/resources-app.png)

    アプリの一覧は .csv ファイルにダウンロードされます。 このプロセスには数分かかることがあります。 一覧が完全にダウンロードされるまでウィンドウを閉じないでください。閉じた場合、プロセスの再起動が必要になる可能性があります。

## <a name="view-the-list"></a>一覧を表示する
.csv ファイルが作成されたら、Excel で開きます。 一覧には、アプリの表示名、アプリの所有者、アプリがデータ ソースに接続するために使用されるコネクタなどの情報が含まれます。

![ファイルと共有](./media/admin-view-apps/excel-view.png)

## <a name="next-steps"></a>次の手順
このクイック スタートでは、組織内の環境で作成されたアプリの一覧をダウンロードおよび表示する方法について説明しました。 次は、組織内で作成されたアプリを管理する方法について説明します。

> [!div class="nextstepaction"]
> [組織で作成したアプリの管理](admin-manage-apps.md)
