---
title: コネクタの概要 | Microsoft Docs
description: アプリの構築に使用できるすべての接続の概要
documentationcenter: ''
author: lancedMicrosoft
manager: kfile
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: conceptual
ms.component: canvas
ms.date: 08/28/2017
ms.author: lanced
ms.openlocfilehash: baa4c71efb54cea6f04cd45b895009a3c3ce17c7
ms.sourcegitcommit: 79b8842fb0f766a0476dae9a537a342c8d81d3b3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/07/2018
ms.locfileid: "37899297"
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
Microsoft のすべてのコネクタを次の表に掲載します。 各コネクタの詳細については、[Microsoft のコネクタのリファレンス](https://docs.microsoft.com/connectors/) ページをご覧ください。 Premium コネクタを使用するには、PowerApps Plan 1 または Plan 2 が必要です。 詳細については、[PowerApps のプラン](https://powerapps.microsoft.com/pricing/)に関するページをご覧ください。

| &nbsp; | &nbsp; |
| --- | --- |
| 10to8 Appointment Scheduling<br>Act!<br>Adobe Creative Cloud ![Premium コネクタ](./media/connections-list/premium.png)<br>Adobe Sign<br>Amazon Redshift ![Premium コネクタ](./media/connections-list/premium.png)<br>Apache Impala ![Premium コネクタ](./media/connections-list/premium.png)<br>AppFigures<br>Approvals<br>Asana<br>AWeber ![Premium コネクタ](./media/connections-list/premium.png)<br>Azure AD<br>Azure Application Insights<br>Azure Automation<br>Azure Blob Storage<br>Azure Cosmos DB<br>Azure Data Lake<br>Azure Event Grid<br>Azure Event Grid Publish<br>Azure File Storage<br>Azure Log Analytics<br>Azure Log Analytics Data Collector<br>Azure キュー<br>Azure Resource Manager<br>Azure Table Storage<br>Basecamp 2<br>Basecamp 3<br>Benchmark Email ![Premium コネクタ](./media/connections-list/premium.png)<br>Bing Maps<br>Bing Search<br>Bitbucket ![Premium コネクタ](./media/connections-list/premium.png)<br>Bitly<br>Bizzy (H3 Solutions, Inc.)<br>Blogger<br>Box<br>bttn<br>Buffer<br>Calendly ![Premium コネクタ](./media/connections-list/premium.png)<br>Campfire<br>Capsule CRM ![Premium コネクタ](./media/connections-list/premium.png)<br>Chatter ![Premium コネクタ](./media/connections-list/premium.png)<br>Cognito Forms<br>Common Data Service ![Premium コネクタ](./media/connections-list/premium.png)<br>Computer Vision API<br>Content Conversion<br>Content Moderator<br>DB2 ![Premium コネクタ](./media/connections-list/premium.png)<br>Disqus<br>DocFusion365 – SP ![Premium コネクタ](./media/connections-list/premium.png)<br>DocuSign ![Premium コネクタ](./media/connections-list/premium.png)<br>Dropbox<br>Dynamics 365<br>Dynamics 365 for Financials<br>Dynamics for Operations<br>Dynamics NAV<br>Easy Redmine ![Premium コネクタ](./media/connections-list/premium.png)<br>Elastic Forms<br>Event Hubs<br>Eventbrite ![Premium コネクタ](./media/connections-list/premium.png)<br>Excel<br>Face API<br>Facebook<br>ファイル システム<br>Flic<br>FlowForma ![Premium コネクタ](./media/connections-list/premium.png)<br>FreshBooks ![Premium コネクタ](./media/connections-list/premium.png)<br>Freshdesk<br>Freshservice ![Premium コネクタ](./media/connections-list/premium.png)<br>FTP<br>GitHub<br>Gmail<br>Google Calendar<br>Google Contacts<br>Google ドライブ<br>Google シート<br>Google Tasks<br>GoToMeeting ![Premium コネクタ](./media/connections-list/premium.png)<br>GoToTraining ![Premium コネクタ](./media/connections-list/premium.png)<br>GoToWebinar ![Premium コネクタ](./media/connections-list/premium.png)<br>Harvest ![Premium コネクタ](./media/connections-list/premium.png)<br>HelloSign ![Premium コネクタ](./media/connections-list/premium.png)<br>HipChat<br>HTTP with Azure AD ![Premium コネクタ](./media/connections-list/premium.png)<br>Informix ![Premium コネクタ](./media/connections-list/premium.png)<br>Infusionsoft ![Premium コネクタ](./media/connections-list/premium.png) |Inoreader<br>Insightly<br>Instagram<br>Instapaper<br>Intercom<br>JIRA ![Premium コネクタ](./media/connections-list/premium.png)<br>JotForm ![Premium コネクタ](./media/connections-list/premium.png)<br>LeanKit ![Premium コネクタ](./media/connections-list/premium.png)<br>LinkedIn<br>LiveChat ![Premium コネクタ](./media/connections-list/premium.png)<br>LUIS<br>メール<br>MailChimp ![Premium コネクタ](./media/connections-list/premium.png)<br>Mandrill ![Premium コネクタ](./media/connections-list/premium.png)<br>M<br>Microsoft Forms<br>Microsoft StaffHub<br>Microsoft Teams<br>Microsoft Translator<br>MSN Weather<br>Muhimbi PDF<br>MySQL ![Premium コネクタ](./media/connections-list/premium.png)<br>Nexmo ![Premium コネクタ](./media/connections-list/premium.png)<br>通知<br>Office 365 Bookings<br>Office 365 グループ<br>Office 365 Outlook<br>Office 365 Users<br>Office 365 ビデオ<br>OneDrive<br>OneDrive for Business<br>OneNote (ビジネス)<br>Oracle Database ![Premium コネクタ](./media/connections-list/premium.png)<br>Outlook Customer Manager<br>Outlook Tasks<br>Outlook.com<br>PagerDuty<br>Parserr<br>Paylocity ![Premium コネクタ](./media/connections-list/premium.png)<br>Pinterest<br>Pipedrive ![Premium コネクタ](./media/connections-list/premium.png)<br>Pitney Bowes Data Validation ![Premium コネクタ](./media/connections-list/premium.png)<br>Pivotal Tracker<br>Planner<br>Plivo ![Premium コネクタ](./media/connections-list/premium.png)<br>PostgreSQL ![Premium コネクタ](./media/connections-list/premium.png)<br>Power BI<br>PowerApps Notification ![Premium コネクタ](./media/connections-list/premium.png)<br>Project Online<br>Redmine<br>RSS<br>Salesforce ![Premium コネクタ](./media/connections-list/premium.png)<br>SendGrid<br>Service Bus<br>SFTP<br>SharePoint<br>Skype for Business<br>Slack<br>SmartSheet<br>SMTP<br>SparkPost<br>SQL Server<br>Stripe ![Premium コネクタ](./media/connections-list/premium.png)<br>SurveyMonkey ![Premium コネクタ](./media/connections-list/premium.png)<br>Teamwork Projects ![Premium コネクタ](./media/connections-list/premium.png)<br>Teradata ![Premium コネクタ](./media/connections-list/premium.png)<br>テキスト分析<br>Todoist<br>Toodledo<br>Trello<br>Twilio<br>Twitter<br>TypeForm<br>UserVoice ![Premium コネクタ](./media/connections-list/premium.png)<br>Video Indexer<br>Vimeo<br>Visual Studio Team Services<br>WebMerge<br>WordPress<br>Wunderlist<br>Yammer<br>YouTube<br>Zendesk ![Premium コネクタ](./media/connections-list/premium.png) |

特定のコネクタについて質問がある場合は、[PowerApps フォーラム](https://powerusers.microsoft.com/t5/PowerApps-Community/ct-p/PowerApps1)をご利用ください。 新しいコネクタのアイデアや改善のご提案がある場合は、[PowerApps Ideas](https://powerusers.microsoft.com/t5/PowerApps-Ideas/idb-p/PowerAppsIdeas) をご利用ください。
