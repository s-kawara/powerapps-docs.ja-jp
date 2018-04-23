---
title: Power Query のトラブルシューティング | Microsoft Docs
description: Power Query を使用してアプリの Common Data Service にカスタム エンティティを作成する際の問題を解決する
services: ''
suite: powerapps
documentationcenter: na
author: mllopis
manager: kfile
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: millopis
ms.openlocfilehash: dafed76565a4bd3fb3e2822319d344f49376b4fc
ms.sourcegitcommit: aa2d0166dccb38100183c093f293233b46f3669d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2018
---
# <a name="troubleshooting-power-query"></a>Power Query のトラブルシューティング
Power Query を使用して外部ソースのデータを含むカスタム エンティティを作成すると、次のエラーが表示される場合があります。

`Your Azure Active Directory administrator has set a policy that prevents you from using this feature. Please contact your administrator, who can grant permissions for this feature on your behalf.`

このエラーは Power Query が PowerApps または Common Data Service の組織のデータにアクセスできない場合に表示されます。 この状況は、次の 2 つの状況で発生します。

* Azure Active Directory (AAD) テナント管理者が、ユーザーの代わりにアプリが会社のデータにアクセスすることにユーザーが同意する権限を許可していない。
* 管理対象外の Active Directory テナントを使用している。 管理対象外のテナントは、セルフ サービス サインアップ オファーを完了するために作成されたディレクトリであり、グローバル管理者は割り当てられていません。 このシナリオを修正するには、ユーザーは最初に管理対象のテナントに変換してから、次のセクションで説明するこの問題の 2 つのソリューションのいずれかに従う必要があります。

この問題を解決するには、AAD 管理者がこのトピックの後半にあるいずれかの手順に従う必要があります。

## <a name="allow-users-to-consent-to-apps-that-access-company-data"></a>アプリが会社のデータにアクセスすることをユーザーが同意できるようにする
次の方法よりこちらの方がおそらく簡単ですが、幅広いアクセスを許可することになります。

1. [https://portal.azure.com](https://portal.azure.com) で **Azure Active Directory** ブレードを開き、**[ユーザー設定]** を選択します。
1. **[ユーザーはアプリが自身の代わりに会社のデータにアクセスすることを許可できます]** の横にある **[はい]** をクリックしてから、**[保存]** をクリックします。

## <a name="allow-power-query-to-access-company-data"></a>Power Query が会社のデータにアクセスすることを許可する
もう 1 つのソリューションは、テナント管理者がテナント全体のアクセス許可を変更することなく Power Query が会社のデータにアクセスすることに同意することです。

1. [Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) をインストールします。
2. 次の PowerShell コマンドを実行します。
   * Login-AzureRmAccount (テナント管理者としてサイン インします)
   * New-AzureRmADServicePrincipal -ApplicationId f3b07414-6bf4-46e6-b63f-56941f3f4128

このアプローチの利点 (テナント全体へのソリューションとの違い) は、このソリューションは対象が絞られていることです。 **Power Query** サービス プリンシパルのみがプロビジョニングされ、テナントのその他のアクセス許可は変更されません。

