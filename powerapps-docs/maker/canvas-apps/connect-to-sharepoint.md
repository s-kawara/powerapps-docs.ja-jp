---
title: PowerApps から SharePoint への接続を作成する | Microsoft Docs
description: アプリを自動的に生成したりゼロから構築したりするときに使用する SharePoint 接続を powerapps.com から作成します。
author: AFTOwen
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: ''
ms.date: 09/03/2016
ms.author: anneta
ms.openlocfilehash: 0e0b98277548d188071bcd29b9e3168de5818321
ms.sourcegitcommit: 0e9af8cace2bdc04750f4c5a70a3c4af8e3d2292
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/22/2018
ms.locfileid: "39195866"
---
# <a name="create-a-connection-to-sharepoint-from-powerapps"></a>PowerApps から SharePoint への接続を作成する
アプリを自動的に生成したりゼロから構築したりすることができるように、SharePoint Online またはオンプレミス SharePoint への接続を作成しましょう。

PowerApps の基本的な事柄については、「[PowerApps の概要](getting-started.md)」を参照してください。

この記事の執筆時点の PowerApps では、カスタム リストはサポートされていますが、ライブラリはサポートされていません。 さらに、**選択**や**画像**など、数種類の列でデータを表示できます。ただし、このデータは更新できません。 詳細については、「[Known issues (既知の問題)](connections/connection-sharepoint-online.md#known-issues)」を参照してください。

## <a name="specify-a-sharepoint-connection"></a>SharePoint 接続の指定
1. まだサインアップが済んでいない場合は、[PowerApps にサインアップ](../signup-for-powerapps.md)します。

2. サインアップに使用した資格情報で [powerapps.com](https://web.powerapps.com?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc) にサインインします。

3. 左側のナビゲーション バーで、**[Mangage (管理)]** をクリックまたはタップし、**[Connections (接続)]** をクリックまたはタップします。

    ![[ファイル] メニューの [新規] オプション](./media/connect-to-sharepoint/manage-connections.png)

4. 右上隅にある **[New connection (新しい接続)]** をクリックまたはタップします。

    ![[New connection (新しい接続)] ボタン](./media/connect-to-sharepoint/new-connection.png)

5. 接続の一覧で **[SharePoint]** をクリックまたはタップします。

    ![SharePoint 接続の追加](./media/connect-to-sharepoint/add-sp-portal.png)

6. 次のいずれかの手順に従います。各手順については、このトピックの中で後述します。

   * [SharePoint Online サイトに接続する](connect-to-sharepoint.md#connect-to-a-sharepoint-online-site)。
   * [オンプレミス SharePoint サイトに接続する](connect-to-sharepoint.md#connect-to-an-on-premises-sharepoint-site)。

## <a name="connect-to-a-sharepoint-online-site"></a>SharePoint Online サイトに接続する
1. **[Connect directly (cloud services) (直接接続 (クラウド サービス))]** をクリックまたはタップし、**[Add connection (接続の追加)]** をクリックまたはタップします。

    ![SharePoint Online を選択](./media/connect-to-sharepoint/choose-online.png)

2. このトピックの最後にある「[次の手順](connect-to-sharepoint.md#next-steps)」に進みます。

## <a name="connect-to-an-on-premises-sharepoint-site"></a>オンプレミス SharePoint サイトに接続する
1. **[Connect using on-premises data gateway (オンプレミスのデータ ゲートウェイを使用して接続)]** をクリックまたはタップします。

    ![オンプレミスの SharePoint を選択](./media/connect-to-sharepoint/choose-onprem.png)

    > [!NOTE]
   > ゲートウェイとオンプレミス接続は、ユーザーの[既定の環境](working-with-environments.md)でのみ作成し、使用できます。

2. ユーザー名とパスワードを指定します。

    資格情報にドメイン名が含まれる場合は、*<ドメイン>\<エイリアス>* 形式で指定してください。

    ![資格情報を指定](./media/connect-to-sharepoint/specify-credentials.png)

3. オンプレミスのデータ ゲートウェイがインストールされていない場合は、[ゲートウェイをインストール](gateway-reference.md)し、アイコンをクリックまたはタップしてゲートウェイの一覧を最新の情報に更新します。

    ![ゲートウェイのインストール](./media/connect-to-sharepoint/install-gateway.png)

4. **[Choose a gateway (ゲートウェイを選択する)]** で、使用するゲートウェイをクリックまたはタップし、**[Add connection (接続の追加)]** をクリックまたはタップします。

    ![ゲートウェイを選択](./media/connect-to-sharepoint/choose-gateway.png)

## <a name="next-steps"></a>次の手順
* 指定したリストに基づいて[アプリを自動的に生成](app-from-sharepoint.md)する。 生成されたアプリには、レコードの閲覧用、単一レコードに関する詳細の表示用、レコードの作成/更新用の 3 つの画面が既定で存在します。
* [アプリをゼロから作成する](get-started-create-from-blank.md)。 このトピックは Excel 向けに作成されていますが、SharePoint の場合も基本的な手順は同じです。
