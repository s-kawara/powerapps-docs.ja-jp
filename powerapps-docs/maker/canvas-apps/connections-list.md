---
title: コネクタの概要 | Microsoft Docs
description: アプリの構築に使用できるすべての接続の概要
author: lancedMicrosoft
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: anneta
ms.date: 08/28/2017
ms.author: lanced
ms.openlocfilehash: 15da6ed2ce6b44c17645ac11d1b049b95e157703
ms.sourcegitcommit: 47be38a23c96ba7478fd777065f5db41181af40b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/20/2018
ms.locfileid: "39164750"
---
# <a name="overview-of-connectors-for-powerapps"></a>PowerApps 用のコネクタの概要
データは、PowerApps でビルドするものを含め、ほとんどのアプリの中核にあります。 *データ ソース*に格納されたデータは、*接続*を作成することでアプリに取り込まれます。 接続は特定の*コネクタ*を使用してデータ ソースと通信します。 PowerApps には SharePoint、SQL Server、Office 365、Salesforce、Twitter などの一般的なサービスやオンプレミスのデータ ソースのためのコネクタがあります。 アプリへのデータの追加を開始するには、「[PowerApps でデータ接続を追加する](add-data-connection.md)」を参照してください。

次の表には特に一般的なコネクタに関する詳細情報へのリンクが含まれています。 すべてのコネクタの一覧については、「[すべてのコネクタ](#all-connectors)」をご覧ください。

| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |
| --- | --- | --- | --- | --- |
| ![Common Data Service](./media/connections-list/cdm.png) |[**Common Data Service**](../common-data-service/data-platform-intro.md) |&nbsp; |![Office 365 Outlook](./media/connections-list/office365.png) |[**Office 365 Outlook**](connections/connection-office365-outlook.md) |
| ![SharePoint](./media/connections-list/sharepoint.png) |[**SharePoint**](connections/connection-sharepoint-online.md) |&nbsp; |![Excel](./media/connections-list/excel.png) |[**Excel**](connections/connection-excel.md) |
| ![SQL Server](./media/connections-list/sql.png) |[**SQL Server**](connections/connection-azure-sqldatabase.md) |&nbsp; |![OneDrive for Business](./media/connections-list/onedrive.png) |[**OneDrive for Business**](connections/cloud-storage-blob-connections.md) |
| ![Dynamics 365](./media/connections-list/dynamics-365.png) |[**Dynamics 365**](connections/connection-dynamics-crmonline.md) |&nbsp; |![OneDrive](./media/connections-list/onedrive.png) |[**OneDrive**](connections/cloud-storage-blob-connections.md) |
| ![Office 365 Users](./media/connections-list/office365.png) |[**Office 365 Users**](connections/connection-office365-users.md) |&nbsp; |![Dropbox](./media/connections-list/dropbox.png) |[**Dropbox**](connections/cloud-storage-blob-connections.md) |

## <a name="types-of-connectors"></a>コネクタの種類
PowerApps には、上に挙げたような*標準コネクタ*と、*カスタム コネクタ*の 2 種類のコネクタがあります。 PowerApps が標準コネクタでサポートするデータ ソースに接続する場合は、そのコネクタを使用してください。 自分で構築したサービスなど、別のソースに接続する必要がある場合は、「[Microsoft Flow でカスタム コネクタを登録して使用する](../canvas-apps/register-custom-api.md)」を参照してください。

接続しているデータ ソースの種類と、そのデータ ソースがデータをどのように返すかに応じて、標準コネクタの動作は異なります。

* 一部のコネクタは、SharePoint、SQL Server、Excel など、表形式のデータ ソースで動作します。 これらのデータ ソースを使用すると、データは表として PowerApps に返されます。 PowerApps はデータとの対話に [Patch()](functions/function-patch.md)、 [Collect()](functions/function-clear-collect-clearcollect.md)、 [Update()](functions/function-update-updateif.md) などの関数を使用します。 表形式のデータもフォームやギャラリーで簡単に使用できます。表のフィールドはギャラリーやフォームのフィールドとして表示されます。 詳細については、次の記事を参照してください。

    [PowerApps のデータ ソースについて](working-with-data-sources.md)

    [Excel データからアプリを生成する](get-started-create-from-data.md)

    [アプリを最初から作成する](get-started-create-from-blank.md)

    > [!NOTE]
  > Excel のデータに接続するには、ブックを OneDrive のようなクラウド ストレージ サービスでホストする必要があります。 詳細については、「[クラウド ストレージ接続](connections/cloud-storage-blob-connections.md)」を参照してください。

* その他のコネクタは、Twitter、Facebook、Office 365 Outlook などの関数ベースのデータ ソースで動作します。 これらのデータ ソースを使用すると、データは基になるサービスでの特定の関数の呼び出しに基づいてデータが PowerApps に返されます。 たとえば、Twitter コネクタで `Twitter.MyFollowers()` を呼び出すと、フォロワーのリストが返されます。 フォームまたはギャラリーでもこのデータを使用できますが、表形式のデータに比べて必要な作業が少し増えます。 詳細については、「[Twitter](connections/connection-twitter.md)」を参照してください。

## <a name="all-connectors"></a>すべてのコネクタ
すべてのコネクタの一覧については、「[コネクタ](https://docs.microsoft.com/connectors/)」を参照してください。 Premium コネクタを使用するには、PowerApps Plan 1 または Plan 2 が必要です。 詳細については、[PowerApps のプラン](https://powerapps.microsoft.com/pricing/)に関するページをご覧ください。


特定のコネクタについて質問がある場合は、[PowerApps フォーラム](https://powerusers.microsoft.com/t5/PowerApps-Community/ct-p/PowerApps1)をご利用ください。 新しいコネクタのアイデアや改善のご提案がある場合は、[PowerApps Ideas](https://powerusers.microsoft.com/t5/PowerApps-Ideas/idb-p/PowerAppsIdeas) をご利用ください。
