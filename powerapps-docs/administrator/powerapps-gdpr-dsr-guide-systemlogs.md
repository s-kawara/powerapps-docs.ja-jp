---
title: PowerApps、Microsoft Flow、Common Data Service (CDS) for Apps でのシステムで生成されたログに対する DSR 要求への対応 | Microsoft Docs
description: PowerApps、Microsoft Flow、Common Data Service (CDS) for Apps でシステムによって生成されたログに対する DSR 要求に対応する手順を説明します
author: jamesol-msft
manager: kfile
ms.service: powerapps
ms.component: pa-admin
ms.topic: conceptual
ms.date: 04/23/2018
ms.author: jamesol
ms.openlocfilehash: 970cf64f9312e1d9f820671d313ee497f3e27b61
ms.sourcegitcommit: b3b6118790d6b7b4285dbcb5736e55f6e450125c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2018
---
# <a name="responding-to-dsr-requests-for-system-generated-logs-in-powerapps-microsoft-flow-and-common-data-service-for-apps"></a>PowerApps、Microsoft Flow、Common Data Service for Apps でのシステムで生成されたログに対する DSR 要求への対応
Microsoft は、欧州連合 (EU) の一般データ保護規制 (GDPR) による "*個人データ*" の広義な定義の下、"個人データ" とみなされる可能性のあるシステムで生成されたログへのアクセス、エクスポート、削除のための機能を提供します。 GDPR の下で個人データとみなされる可能性のあるシステムで生成されたログの例は、次のとおりです。
* 製品およびサービス使用状況データ (ユーザー アクティビティ ログなど)
* ユーザーの検索要求とクエリのデータ
* システム機能、またはユーザーや他のシステムによるやり取りの生成物として、製品およびサービスによって生成されるデータ

システムで生成されたログのデータの制限または修正のための機能はサポートされていないことに注意してください。 システムで生成されたログのデータは、Microsoft クラウド内で実行される実際のアクションで構成され、診断データ (そうしたデータへの変更を含む) によってアクションの履歴レコードが侵害され、不正アクセスやセキュリティ上のリスクが高まる可能性があります。

## <a name="accessing-and-exporting-system-generated-logs"></a>システムで生成されたログへのアクセスとエクスポート
管理者は、PowerApps、Microsoft Flow、および Common Data Service (CDS) for Apps サービスとアプリケーションのユーザーの使用に関連するシステムで生成されたログにアクセスできます。

システムで生成されたログにアクセスしてエクスポートするには、次のようにします。

1. [Microsoft Service Trust Portal](https://servicetrust.microsoft.com/) に移動し、Office 365 全体管理者の資格情報を使ってサインインします。

2. ページの上部の **[プライバシー]** ドロップダウン リストから **[Data Subject Request]\(データ主体要求\)** を選択します。

3. **[Data Subject Request]\(データ主体要求\)** ページの **[System Generated Logs]\(システムで生成されたログ\)** で **[データ ログのエクスポート]** を選択します。 [データ ログのエクスポート] により、組織が送信したデータ エクスポート要求の一覧が表示されます。

4. 特定のユーザーに対する新しい要求を作成するには、**[Create Export Data Request]\(データ エクスポート要求の作成\)** をクリックします。

    新しい要求を作成した後、要求が **[データ ログのエクスポート]** に一覧表示され、ここでその状態を追跡できます。 要求が完了した後、リンクをクリックしてシステムで生成されたログにアクセスできます。これは、要求の作成後 30 日間、組織の Azure Storage の場所にエクスポートされます。 データは一般的なコンピューターが判読できるファイル形式 (XML、CSV、JSON など) で保存されます。 Azure アカウントや Azure Storage の場所がない場合、データ ログのエクスポート ツールによってシステムで生成されたログをエクスポートできるように、組織用の Azure アカウントまたは Azure Storage の場所を作成する必要があります。 詳細については、「[Microsoft Azure Storage の概要](https://docs.microsoft.com/azure/storage/common/storage-introduction)」を参照してください。

次の表には、システムで生成されたログへのアクセスとエクスポートについてまとめられています。

| 質問 | 回答 |
| --- | --- |
| Microsoft データ ログのエクスポート ツールが要求を完了するのにかかる時間を教えてください。 |    これには、いくつかの要因が影響します。 ほとんどの場合、1 日または 2 日で終了しますが、最大で 30 日かかる場合もあります。
| どのような形式で出力されますか。 | XML、CSV、JSON などのコンピューターが判読できる、構造化されたファイル形式で出力されます。
| データ ログのエクスポート ツールへのアクセス権を持ち、システムで生成されたログへのアクセス要求を送信する権利を持つユーザーは誰ですか。 | Office 365 グローバル管理者は、GDPR ログ マネージャー ツールにアクセスできます。
| データ ログのエクスポート ツールによって返されるデータを教えてください。 | データ ログのエクスポート ツールによって、Microsoft が格納するシステムで生成されたログが返されます。 エクスポートされたデータの対象範囲は、Office 365、Azure、Dynamics、PowerApps、Microsoft Flow、CDS for Apps などさまざまな Microsoft サービスに及びます。
| データはどのようにユーザーに返されますか。 |   データは、組織の Azure Storage の場所にエクスポートされます。このデータをユーザーにどのように表示する/戻すかは、組織内の管理者によって決定されます。
| システムで生成されたログのデータはどのように表示されますか。 |  JSON 形式でシステムによって生成されたログ レコードの例: <br> [{ <br>"DateTime": "2017-04- 28T12:09:29-07:00",  <br> "AppName": "SharePoint", <br> "Action": "OpenFile", "IP": "154.192.13.131", <br> "DevicePlatform": "Windows 1.0.1607" <br>}]

> [!NOTE]
>  セキュリティと監査の観点から、個人情報の整合性を維持するため、一部の機能ではシステム生成ログをエクスポートまたは削除できません。
>
>

## <a name="deleting-system-generated-logs"></a>システムで生成されたログの削除
アクセス要求を使用して取得されたシステムで生成されたログを削除するには、ユーザーをそのサービスから削除し、そのユーザーの Azure Active Directory アカウントを完全に削除する必要があります。 ユーザーを完全に削除する方法については、[Office 365 Service Trust Portal](https://servicetrust.microsoft.com/ViewPage/GDPRDSR) にある *Azure でのデータ主体要求 GDPR に関するドキュメント*の**ユーザーの削除**に関するセクションをご覧ください。 ユーザー アカウントを完全に削除すると元に戻すことができないことに注意してください。

ユーザー アカウントを完全に削除すると、PowerApps、Microsoft Flow、および CDS for Apps サービス用にシステムで生成されたログからユーザーのデータが 30 日後に削除されます。