---
title: テナント内のアクティブ ユーザーの一覧をダウンロードする | Microsoft Docs
description: このクイック スタートでは、テナント内のアクティブ ユーザーの一覧をダウンロードする方法について説明します。
author: jimholtz
ms.service: powerapps
ms.component: pa-admin
ms.topic: quickstart
ms.date: 03/21/2018
ms.author: jimholtz
search.audienceType:
- admin
search.app:
- D365CE
- PowerApps
- Powerplatform
ms.openlocfilehash: 41f557b7b4def385a505e3bc3047354add81955e
ms.sourcegitcommit: 429b83aaa5a91d5868e1fbc169bed1bac0c709ea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/24/2018
ms.locfileid: "42832450"
---
# <a name="download-a-list-of-active-users-in-your-tenant"></a>テナント内のアクティブ ユーザーの一覧をダウンロードする
365 グローバル管理者または Azure Active Directory テナント管理者の場合は、テナント内のアクティブ ユーザーの一覧をダウンロードし、PowerApps、Microsoft Flow、またはその両方にアクセスしたユーザーだけでなく、それらのユーザーに割り当てられたライセンスを確認することができます。

このトピックでは、アクティブ ユーザーの一覧を .csv ファイルにダウンロードし、その一覧を Excel で表示する方法について説明します。

この手順を実行するには、Office 365 グローバル管理者または Azure Active Directory テナント管理者のアクセス許可が必要です。

## <a name="sign-in-to-the-powerapps-admin-center"></a>PowerApps 管理センターにサインインする
[https://admin.powerapps.com]([https://admin.powerapps.com) で管理センターにサインインします。

## <a name="download-the-list-of-users"></a>ユーザーの一覧をダウンロードする
ナビゲーション ウィンドウで、**[ユーザー ライセンス]**、**[アクティブなユーザー ライセンスの一覧をダウンロードする]** の順にクリックまたはタップします。

![ファイルと共有](./media/admin-view-user-licenses/download-list.png)

ユーザーの一覧は .csv ファイルにダウンロードされます。 このプロセスには数分かかることがあります。 一覧が完全にダウンロードされるまでウィンドウを閉じないでください。閉じた場合、プロセスの再起動が必要になる可能性があります。

## <a name="view-the-list"></a>一覧を表示する
.csv ファイルが作成されたら、Excel で開きます。 一覧には、各ユーザーの名前、メール アドレス、ライセンスの種類、その他の情報などが含まれています。

製品に 1 回以上アクセスしたユーザーは、*アクティブ ユーザー*と見なされます。 これはアクティブ ユーザーの一覧なので、PowerApp と Microsoft Flow のライセンスを所有していても一度もアクセスしたことがないユーザーは含まれていません。 [Office 365 管理センター](https://support.office.com/article/Assign-or-remove-licenses-for-Office-365-for-business-997596b5-4173-4627-b915-36abac6786dc)から、すべてのユーザー ライセンスを表示できます。

次の例は、PowerApps と Microsoft Flow の両方のライセンスを所有している 2 人のユーザーを示しています。 Jane Doe は Office 365 のサブスクリプションでアクセスしており、John Doe は各製品の試用版のライセンスを取得済みです。

![ファイルと共有](./media/admin-view-user-licenses/table2.png)

ユーザーが組織を去った場合は、一覧の **[ユーザー名]** 列や **[電子メール アドレス]** 列に **[不明]** と表示されます。 一覧に **[不明]** と表示されているが誰も組織から去ってない場合は、数分待ってから再び一覧をダウンロードします。

ユーザー ライセンスを追加するには、[Office 365 管理センター](https://support.office.com/article/Assign-or-remove-licenses-for-Office-365-for-business-997596b5-4173-4627-b915-36abac6786dc)を開きます。

## <a name="next-steps"></a>次の手順
このトピックでは、テナント内のアクティブ ユーザーの一覧をダウンロードして表示する方法について説明しました。 環境内で作成されたアプリの一覧をダウンロードして表示する方法については、次のトピックを参照してください。

> [!div class="nextstepaction"]
> [環境内で作成したアプリの一覧をダウンロードする](admin-view-apps.md)
