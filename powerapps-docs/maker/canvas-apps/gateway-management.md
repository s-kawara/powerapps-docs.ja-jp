---
title: キャンバス アプリ用のオンプレミス データ ゲートウェイを管理する | Microsoft Docs
description: オンプレミス データ ゲートウェイとその接続の管理
author: archnair
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: anneta
ms.date: 10/30/2016
ms.author: archanan
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 85806799a5f5ea91a4671a27e71cf95daabcd01a
ms.sourcegitcommit: 4042388fa5e7ef50bc59f9e35df330613fea29ae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61553568"
---
# <a name="manage-an-on-premises-data-gateway-in-powerapps"></a>PowerApps でのオンプレミス データ ゲートウェイの管理
オンプレミスの SQL Server データベース、オンプレミスの SharePoint サイトなど、クラウドに存在しないデータ ソースと PowerApps で構築されたキャンバス アプリとの間でデータをすばやく安全に転送するためには、オンプレミス データ ゲートウェイをインストールします。 管理者権限があるすべてのゲートウェイを表示し、それらの権限と接続を管理することができます。

ゲートウェイを使用すると、次の接続を介して、オンプレミス データに接続できます。

* SharePoint
* SQL Server
* Oracle
* Informix
* ファイル システム
* DB2

## <a name="prerequisites"></a>前提条件
* PowerApps の[サインアップ](../signup-for-powerapps.md)に使用したユーザー名とパスワード。
* ゲートウェイの管理者アクセス許可。 (ゲートウェイをインストールしたユーザーには、ゲートウェイごとにこれらのアクセス許可が既定で割り当てられます。また、他のゲートウェイの管理者から、そのゲートウェイの管理者アクセス許可を付与してもらうこともできます。)
* オンプレミス ゲートウェイを使用したオンプレミス データへのアクセスをサポートするライセンス。 詳細については、[料金に関するページ](https://powerapps.microsoft.com/pricing/)の「Connectivity (接続)」セクションを参照してください。
* ゲートウェイとオンプレミス接続は、ユーザーの[既定の環境](working-with-environments.md)でのみ作成し、使用できます。

## <a name="install-a-gateway"></a>ゲートウェイのインストール
1. [powerapps.com](https://web.powerapps.com?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc) の左側のナビゲーション バーで、**[ゲートウェイ]** をクリックまたはタップします。

    ![左側のナビゲーション バーのゲートウェイ](./media/gateway-management/manage-gateway.png)

2. ゲートウェイの管理者権限がない場合は、[[Install a gateway now (ゲートウェイをインストールする)]](http://go.microsoft.com/fwlink/?LinkID=820931) (または右上隅の **[新しいゲートウェイ]**) をクリックまたはタップし、表示されるウィザードの指示に従います。

    ![ゲートウェイのインストール](./media/gateway-management/no-gateway-installed.png)

    ゲートウェイのインストール方法について詳しくは、「[オンプレミス データ ゲートウェイについて](gateway-reference.md)」を参照してください。

## <a name="view-and-manage-gateway-permissions"></a>ゲートウェイ アクセス許可の表示と管理
1. [powerapps.com](https://web.powerapps.com?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc) の左側のナビゲーション バーで、**[ゲートウェイ]** をクリックまたはタップし、ゲートウェイをクリックまたはタップします。

2. **[ユーザー]** をクリックまたはタップしてユーザーまたはグループを指定し、権限レベルを指定してゲートウェイにユーザーを追加します。

   * **使用できる**:ユーザー アプリとフローを使用するゲートウェイの接続を作成することができますが、ゲートウェイを共有することはできません。 このアクセス許可は、アプリを実行するが共有しないユーザーに対して使用します。
   * **使用し、共有できる**:アプリとフローを使用するゲートウェイの接続を作成してアプリを共有する場合、ゲートウェイが自動的に共有できるユーザーのユーザー。 このアクセス許可は、他のユーザーまたは組織とアプリを共有する必要があるユーザーに対して使用します。
   * **管理者**:ユーザーを追加、アクセス許可の設定、すべての利用可能なデータ ソースへの接続を作成、ゲートウェイを削除するなど、ゲートウェイのフル コントロールを持つ管理者です。

**[使用可能]** と **[使用と共有が可能]** のアクセス許可レベルについては、ユーザーがゲートウェイを経由して接続できるデータ ソースを選択します。

## <a name="view-and-manage-gateway-connections"></a>ゲートウェイ接続の表示と管理
1. [powerapps.com](https://web.powerapps.com?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc) の左側のナビゲーション バーで、**[ゲートウェイ]** をクリックまたはタップし、ゲートウェイをクリックまたはタップします。

2. **[接続]** をクリックまたはタップし、詳細の表示、設定の編集、または接続の削除を行います。

3. 接続を共有するには、**[共有]** をクリックまたはタップしてユーザーを追加または削除します。

    > [!NOTE]
   > 共有できる接続の種類は一部 (SQL Server など) に限定されています。 詳しくは、「[Share app resources (アプリ リソースの共有)](share-app-resources.md)」をご覧ください。

接続を管理する方法について詳しくは、「[PowerApps で接続を管理する](add-manage-connections.md)」を参照してください。

## <a name="troubleshooting-and-advanced-configuration"></a>トラブルシューティングと高度な構成
ゲートウェイに関する問題のトラブルシューティングや、ネットワークのゲートウェイ サービスの構成の詳細については、「[Microsoft PowerApps のオンプレミス データ ゲートウェイについて](gateway-reference.md)」を参照してください。

## <a name="next-steps"></a>次の手順
* [SQL Server](connections/connection-azure-sqldatabase.md) や [SharePoint](connections/connection-sharepoint-online.md) などのオンプレミス データ ソースに接続するアプリを作成する
* オンプレミス データ ソースに接続する[アプリを共有する](share-app.md)。
