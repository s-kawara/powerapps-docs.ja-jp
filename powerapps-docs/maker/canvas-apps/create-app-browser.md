---
title: Web ブラウザーでのアプリの作成と編集 | Microsoft Docs
description: Web 用の PowerApps Studio を使用して、ブラウザーでアプリを作成し、編集します。
author: AFTOwen
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: ''
ms.date: 03/08/2018
ms.author: anneta
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 8948076f104f32af605ba123d9a500dcb07692ea
ms.sourcegitcommit: 429b83aaa5a91d5868e1fbc169bed1bac0c709ea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/24/2018
ms.locfileid: "42862935"
---
# <a name="create-or-edit-apps-in-powerapps-studio-for-web"></a>Web 用の PowerApps Studio でのアプリの作成または編集
Windows または他のプラットフォームのブラウザー ウィンドウで開く Web 用の PowerApps Studio で、アプリの作成と編集を行います。

## <a name="prerequisites"></a>前提条件
* PowerApps に[サインアップ](../signup-for-powerapps.md)。
* [サポート対象のブラウザー](limits-and-config.md#supported-browsers-for-powerapps-studio)を使用していることを確認します。

## <a name="open-powerapps-studio-for-web"></a>Web 用の PowerApps Studio を開く
1. [powerapps.com](http://go.microsoft.com/fwlink/p/?LinkId=708209) にサインインします。
2. 左下隅で **[新しいアプリ]** をクリックまたはタップします。

    ![左側のナビゲーション バーの新しいアプリ](./media/create-app-browser/left-nav.png)

Web 用の PowerApps Studio がブラウザーの新しいタブで開き、PowerApps Studio for Windows と同じ方法でアプリの作成と編集を行うことができます。

## <a name="known-limitations"></a>既知の制限
1. **接続を作成する。**

    サービス認証が必要なデータソースへの[接続を作成する](add-manage-connections.md)には、[powerapps.com](https://web.powerapps.com?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc) で行ってから、Web 用の PowerApps Studio でアプリに[その接続を追加](add-data-connection.md)します。
2. **ローカルのアプリを編集して保存する**。

    最良の結果を得るには、PowerApps Studio for Windows を使用してローカルのアプリを編集し、保存します。 ブラウザーではローカルのアプリに変更を保存することはできません。開いたファイルを置き換える代わりに新しいファイルを保存する必要があります。
3. **シグナル関数を使用する。**

    **[Acceleration および Compass](functions/signals.md)** 関数は、公開されたアプリでは正確な値を返しますが、ブラウザーでアプリを作成または変更している場合にはゼロ値を返します。
4. **データをエクスポートおよびインポートする。**

    発行されたアプリでは[データをエクスポートおよびインポート](controls/control-export-import.md)できますが、ブラウザーでアプリを作成または変更している場合はできません。
5. **2 つのセッション間でコントロールをコピーする。**

    Web 用の PowerApps Studio のセッション間ではコントロールをコピーできません。

## <a name="next-steps"></a>次の手順
* [Excel](get-started-create-from-data.md) や [SharePoint](app-from-sharepoint.md) などのデータからアプリを自動的に生成します。
* [コントロールを追加してそのプロパティを設定](add-configure-controls.md)する方法を確認します。アプリの体裁と動作は、そのプロパティによって決まります。
* [アプリを最初から作成](get-started-create-from-blank.md)します。
