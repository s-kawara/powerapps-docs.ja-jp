---
title: トラブルシューティング - このデータベースの Mashup を作成または取得できない | Microsoft Docs
description: CDS と Power Query を使用してカスタム エンティティを作成するときの問題を、管理者が AAD の制限を変更することで解決します。
services: ''
suite: powerapps
documentationcenter: na
author: mllopis
manager: kfend
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: millopis
ms.openlocfilehash: 919d88309f4f9bc0e73f63ab5fd5401194a2f264
ms.sourcegitcommit: 59785e9e82da8f5bd459dcb5da3d5c18064b0899
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/22/2018
---
# <a name="troubleshooting---unable-to-create-or-retrieve-a-mashup-for-this-database"></a>トラブルシューティング - このデータベースの Mashup を作成または取得できない
**データの新しいエンティティ (Technical Preview)** の機能を使用するときに、次のようなエラーが発生する場合があります。

    *Unable to create or retrieve a mashup for the current database*

これは、**Power Query** を使用する外部データ ソースのデータに基づいた **Common Data Service (CDS)** で*カスタム エンティティ*を作成する機能を利用する時に発生する可能性があります。 **Power Query** が **PowerApps または CDS** の組織のデータにアクセスできないときに、このエラーがトリガーされます。 これが発生する可能性があるシナリオは、2 つあります。

* **Azure Active Directory** (AAD) テナント管理者が、ユーザーの代わりにアプリが会社のデータにアクセスすることにユーザーが同意する権限を許可していない。
* 管理対象外の Active Directory テナントを使用している。 管理対象外のテナントは、セルフ サービス サインアップ オファーを完了するために作成されたディレクトリであり、グローバル管理者は割り当てられていません。 このシナリオを修正するには、ユーザーは*最初に*管理対象のテナントに変換してから、次のセクションで説明するこの問題の 2 つのソリューションのいずれかに従う必要があります。

上記で説明した問題を解決する方法は、2 つあります。

* AAD の管理者に依頼して、会社のデータにアプリがアクセスすることをユーザーが承認することを許可する手順を実行する
* AAD の管理者に依頼して、**Power Query** がデータにアクセスすることを許可する

次に、これらのソリューションに必要な各手順について説明します。

## <a name="allowing-users-to-give-apps-consent-to-access-company-data"></a>会社のデータにアプリがアクセスすることをユーザーが承認することを許可する

AAD テナントの管理者に連絡して、次の手順を実行して、会社のデータにアプリがアクセスすることをユーザーが承認できるようにしてもらいます。

1. [https://portal.azure.com](https://portal.azure.com) にアクセスします
2. **Azure Active Directory** ブレードを開きます。
3. **[ユーザー設定]** を選択します。
4. **[ユーザーはアプリが自身の代わりに会社のデータにアクセスすることを許可できます]** の横にある **[はい]** をクリックしてから、**[保存]** をクリックします。
5. そのプロセスが完了すると、問題は解決されます。

これがおそらく最も簡単な方法ですが、次のオプションよりも幅広いアクセスを許可することになります。

## <a name="allowing-power-query-to-access-company-data"></a>Power Query が会社のデータにアクセスすることを許可する
もう 1 つのソリューションは、テナント管理者がテナント全体のアクセス許可を変更することなく **Power Query** が会社のデータにアクセスすることに同意することです。 テナント管理者に依頼して、以下の手順を実行してください。

1. [Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) のインストール
2. 次の PowerShell コマンドを実行します。
   * Login-AzureRmAccount (テナント管理者としてサイン インします)
   * New-AzureRmADServicePrincipal -ApplicationId f3b07414-6bf4-46e6-b63f-56941f3f4128

このアプローチの利点 (テナント全体へのソリューションとの違い) は、このソリューションは対象が絞られていることです。 **Power Query** サービス プリンシパルのみがプロビジョニングされ、テナントのその他のアクセス許可は変更されません。

