---
title: キャンバス アプリへのデータ接続の追加 | Microsoft Docs
description: 既存のキャンバス アプリや空のアプリにデータ接続を追加できます
author: lancedMicrosoft
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: anneta
ms.date: 04/06/2018
ms.author: lanced
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 15f3f38dd4812ffcbebeeaab4d301f715c97e1d1
ms.sourcegitcommit: be110258910aa097b0065da1ee4ea1c40b7e1334
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/20/2019
ms.locfileid: "65922540"
---
# <a name="add-a-data-connection-to-a-canvas-app-in-powerapps"></a>PowerApps でキャンバス アプリにデータ接続を追加する

PowerApps で、既存のキャンバス アプリまたはゼロから作成するアプリにデータ接続を追加します。 アプリは、SharePoint、Common Data Service、Salesforce、OneDrive に接続できるまたは[他の多くのデータ ソース](connections-list.md)します。

この記事の後に来る[次のステップ](#next-steps)は、以下に示す例のように、接続したデータ ソースのデータをアプリで表示および管理することです。

* OneDrive に接続し、アプリ内で Excel ブックのデータを管理する。
* Twilio に接続し、アプリから SMS メッセージを送信する。
* Common Data Service に接続し、アプリからエンティティを更新します。
* SQL Server に接続し、アプリからテーブルを更新する。

## <a name="prerequisites"></a>前提条件

PowerApps に[サインアップ](../signup-for-powerapps.md)し、サインアップに使用したのと同じ資格情報を入力して[サインイン](http://web.powerapps.com?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc)します。

## <a name="open-a-blank-app"></a>空のアプリを開く

1. **ホーム**] タブで [**空白からのキャンバス アプリ**します。

1. アプリの名前を指定し、**作成**です。

1. **[PowerApps Studio へようこそ]** ダイアログ ボックスが表示されたら、**[スキップ]** を選択します。

## <a name="add-data-source"></a>データ ソースの追加

1. 中央のウィンドウで次のように選択します。**データへの接続**を開く、**データ**ウィンドウ。

    これが既存のアプリ画面にコントロールが既に含まれている場合は、**ビュー** > **データソース**同じウィンドウを開きます。

1. 選択**データ ソースの追加**します。

1. 接続の一覧には、希望する方が含まれている場合は、アプリに追加することを選択します。 それ以外の場合、次のステップに進んでください。

    ![既存の接続を選択します。](./media/add-data-connection/choose-existing-connection.png)

1. 選択**新しい接続**接続の一覧を表示します。

    ![接続の追加](./media/add-data-connection/add-connection.png)

1. 検索バーで、入力または目的の接続の最初の数文字を貼り付けるし、が表示されたら、接続を選択します。

    ![接続の検索](./media/add-data-connection/search-connections.png)

1. **[作成]** を選択して、接続の作成とアプリへの追加の両方を行います。

    **Office 365 Outlook** などのコネクタでは、追加の手順を実行しなくても、すぐにデータを表示できます。 コネクタによっては、資格情報の入力や、特定のデータ セットの指定などの手順が要求されることがあります。 たとえば、[SharePoint](connections/connection-sharepoint-online.md) と [SQL Server](connections/connection-azure-sqldatabase.md) では、使用する前に追加情報の入力を求められます。 [Common Data Service](connections/connection-common-data-service.md)エンティティを選択する前に環境を変更することができます。

## <a name="identify-or-change-a-data-source"></a>データ ソースの特定または変更
アプリを更新する際、ギャラリー、フォーム、または別のコントロールに表示されるデータ ソースを特定または変更する必要があることがあります。 たとえば、そのユーザーがそれ以外の場合に作成されたアプリを更新するか、前に作成したデータ ソースを識別する必要があります。

1. ギャラリーを特定するか、データ ソースを変更するなど、コントロールを選択します。

    右側のウィンドウの **[プロパティ]** タブにデータ ソース名が表示されます。

    ![特定の接続](./media/add-data-connection/identify-connection.png)

1. データ ソースに関する詳細情報を表示または変更するには、その名前の横にある下矢印を選択します。

    詳細については、現在のデータ ソースは表示され、選択するか、別のソースを作成することができます。

    ![接続を変更します。](./media/add-data-connection/change-connection.png)

## <a name="next-steps"></a>次の手順

* Excel、SharePoint、Common Data Service、または SQL Server などのソースでデータを表示および更新[ギャラリーを追加](add-gallery.md)、および[フォームを追加](add-form.md)します。
* [Office 365 Outlook](connections/connection-office365-outlook.md)、[Twitter](connections/connection-twitter.md)、[Microsoft Translator](connections/connection-microsoft-translator.md) などのソースの場合は、各コネクタに用意された機能を使用して表示や更新を行います。
