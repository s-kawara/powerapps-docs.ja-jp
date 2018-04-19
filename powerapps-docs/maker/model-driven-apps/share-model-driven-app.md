---
title: PowerApps でのモデル駆動型アプリの共有のチュートリアル | Microsoft Docs
description: このチュートリアルでは、モデル駆動型アプリを共有する方法について説明します
services: ''
suite: powerapps
documentationcenter: ''
author: Mattp123
manager: brycho
editor: ''
tags: ''
ms.service: powerapps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/21/2018
ms.author: matp
ms.openlocfilehash: 4f971668b506776cfd1a9cce2f61d591a4a0db5e
ms.sourcegitcommit: d7ed5144f96d1ecc17084c30ed0e2ba3c6b03c26
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/19/2018
---
# <a name="tutorial-share-a-model-driven-app-with-powerapps"></a>チュートリアル: PowerApps でモデル駆動型アプリを共有する

[!INCLUDE [powerapps](../../includes/powerapps.md)] アプリは、共有にロール ベースのセキュリティを使います。 ロール ベースのセキュリティの基本概念は、セキュリティ ロールにはアプリ内で実行できるアクションのセットを定義する権限が含まれる、というものです。 アプリのすべてのユーザーは、1 つまたは複数の定義済みロールまたはカスタム ロールに割り当てられる必要があります。 または、ロールをチームに割り当てることもできます。 ユーザーまたはチームがこのようなロールの 1 つに割り当てられると、その個人またはチーム メンバーには、そのロールに関連付けられた権限のセットが付与されます。 

このチュートリアルでは、他のユーザーが使用できるようにモデル駆動型アプリを共有するためのタスクを実行します。 次の方法を説明します。
- カスタム セキュリティ ロールを作成する
- カスタム セキュリティ ロールにユーザーを割り当てる
- セキュリティ ロールをアプリに割り当てる

> [!IMPORTANT]
> [!INCLUDE [cc-preview-features-definition](../../includes/cc-preview-features-definition.md)]

## <a name="prerequisites"></a>前提条件
アプリを共有するには、[!INCLUDE [powerapps](../../includes/powerapps.md)] の環境管理者ロールまたはシステム管理者ロールを持っている必要があります。 

## <a name="sign-in-to-powerapps"></a>PowerApps へのサインイン
[PowerApps](https://powerapps.microsoft.com/) にサインインします。 まだ [!INCLUDE [powerapps](../../includes/powerapps.md)] アカウントを持っていない場合は、**[GET STARTED FREE]** リンクを選びます。

## <a name="share-an-app"></a>アプリを共有する 
このチュートリアルで使う Contoso という会社は、犬や猫を対象とするペット美容室ビジネスを展開しています。 ペット美容室ビジネスを追跡するためのカスタム エンティティを含むアプリは、既に作成されて公開されています。 現在は、ペット美容室のスタッフが使用できるように、アプリを共有する必要があります。 アプリを共有するには、管理者またはアプリ作成者が 1 つまたは複数のセキュリティ ロールをユーザーとアプリに割り当てます。 

## <a name="create-or-configure-a-security-role"></a>セキュリティ ロールを作成または構成する
[!INCLUDE [powerapps](../../includes/powerapps.md)] 環境には、アプリの使用に必要な最小限のビジネス データへのアクセスを提供するというセキュリティのベスト プラクティス目標に一致するようにアクセス レベルが定義されている一般的なユーザー タスクを反映する[定義済みのセキュリティ ロール](#about-predefined-security-roles)が含まれます。 Contoso のペット美容室アプリはカスタム エンティティに基づくことに注意してください。 エンティティがカスタムであるため、ユーザーに適用する前に権限を明示的に指定する必要があります。 これを行うには、次のいずれかを選びます。
- 既存の定義済みセキュリティ ロールを拡張し、ユーザー定義エンティティに基づくレコードに対する権限が含まれるようにします。 
- アプリのユーザーに対する権限を管理するためのカスタム セキュリティ ロールを作成します。 

ペット美容室レコードを保持する環境は、Contoso のビジネスが実行する他のアプリにも使われるため、ペット美容室アプリに固有のカスタム セキュリティ ロールを作成します。 さらに、2 つの異なるアクセス権限のセットが必要です。
- トリマーは読むこと、更新すること、他のレコードを添付することだけが必要なので、そのセキュリティ ロールは読み取り、書き込み、追加の権限を持っています。 
- ペット美容室のスケジュール担当者は、ペット美容テクニシャンが持つすべての権限に加えて、作成、追加、削除、共有を行うことができる必要があるので、そのセキュリティ ロールは、作成、読み取り、書き込み、追加、削除、割り当て、共有の権限を持っています。

アクセスとスコープの権限のについて詳しくは、「[セキュリティ ロール](https://docs.microsoft.com/dynamics365/customer-engagement/admin/security-roles-privileges#security-roles)」をご覧ください。

## <a name="create-a-custom-security-role"></a>カスタム セキュリティ ロールを作成する
1. [!INCLUDE [powerapps](../../includes/powerapps.md)] サイトで、**[モデル駆動]** > **[アプリ]** > **...**> **[Share link]\(リンクを共有\)** の順に選びます。
2. **[このアプリを共有する]** ダイアログの **[セキュリティ ロールを作成する]** で **[Security Setting]\(セキュリティの設定\)** を選びます。
3. **[設定]** ページで **[新規]** を選びます。  

4. セキュリティ ロール デザイナーから、読み取り、書き込み、削除などのアクションと、そのアクションを実行するスコープを選択します。 スコープは、ユーザーが特定のアクションを実行できる環境階層内の深さや高さを決定します。 **[ロール名]** ボックスに「*Pet Grooming Technicians*」と入力します。
5. **[Custom Entities]\(カスタム エンティティ\)** タブを選び、使うカスタム エンティティを探します。 この例では、"**Pet**" という名前のカスタム エンティティを使います。 
6. "**Pet**" 行で、**[読み取り]、[書き込み]、[追加]** の各権限を 4 回選んで、組織のスコープをグローバル ![組織のグローバル スコープ](media/share-model-driven-app/organizational-scope-privilege.png) にします。
![新しいセキュリティ ロール](media/share-model-driven-app/custom-security-role.png)
7. ペット美容室アプリにはアカウント エンティティとのリレーションシップもあるので、**[Core Records]\(コア レコード\)** タブを選び、"**Account**" 行で **[読み取り]** を 4 回選んで、組織のスコープをグローバル ![組織のグローバル スコープ](media/share-model-driven-app/organizational-scope-privilege.png) にします。 
8. **[保存して閉じる]** を選びます。 
9. セキュリティ ロール デザイナーで、**[ロール名]** ボックスに「*Pet Grooming Schedulers*」と入力します。 
10. **[Custom Entities]\(カスタム エンティティ\)** タブを選び、"**Pet**" エンティティを探します。 
11. "**Pet**" 行で、**[作成]、[読み取り]、[書き込み]、[削除]、[追加]、[追加先]、[割り当て]、[共有]** の各権限を 4 回選んで、組織のスコープをグローバル ![組織のグローバル スコープ](media/share-model-driven-app/organizational-scope-privilege.png) にします。
12. ペット美容室アプリにはアカウント エンティティとのリレーションシップもあり、スケジュール担当者はアカウント レコードを作成および編集できる必要があるので、**[Core Records]\(コア レコード\)** タブを選び、"**Account**" 行で以下の権限を 4 回選んで、組織のスコープをグローバル ![組織のグローバル スコープ](media/share-model-driven-app/organizational-scope-privilege.png) にします。 
    **[作成]、[読み取り]、[書き込み]、[削除]、[追加]、[追加先]、[割り当て]、[共有]**
13. **[保存して閉じる]** を選びます。

## <a name="assign-security-roles-to-users"></a>ユーザーにセキュリティ ロールを割り当てる
セキュリティ ロールは、一連のアクセス レベルとアクセス許可を使用してデータへのユーザーのアクセスを制御します。 アクセス レベルと、特定のセキュリティ ロールに含まれているアクセス許可を組み合わせて、ユーザーのデータの閲覧とそのデータのユーザー操作に対して制限を設定します。

### <a name="assign-a-security-role-to-pet-grooming-technicians"></a>トリマーにセキュリティ ロールを割り当てる
1. **[このアプリを共有する]** ダイアログの **[ユーザーをセキュリティ ロールに割り当てる]** で **[Security Users]\(セキュリティ ユーザー\)** を選びます。
2. 表示される一覧で、トリマーを選びます。
3. **[ロールの管理]** を選びます。

    ![ロールの管理](media/share-model-driven-app/select-users-for-security-roles.png)

4. **[ユーザー ロールの管理]** ダイアログ ボックスで、前に作成した "**Pet Grooming Technicians**" セキュリティ ロールを選び、**[OK]** を選びます。

### <a name="assign-a-security-role-to-pet-grooming-schedulers"></a>スケジュール担当者にセキュリティ ロールを割り当てる
1. **[このアプリを共有する]** ダイアログの **[ユーザーをセキュリティ ロールに割り当てる]** で **[Security Users]\(セキュリティ ユーザー\)** を選びます。
2. 表示される一覧で、スケジュール担当者を選びます。
3. **[ロールの管理]** を選びます。
4. **[ユーザー ロールの管理]** ダイアログ ボックスで、前に作成した "**Pet Grooming Schedulers**" セキュリティ ロールを選び、**[OK]** を選びます。


## <a name="add-security-roles-to-the-app"></a>アプリにセキュリティ ロールを追加する
次に、1 つまたは複数のセキュリティ ロールをアプリに割り当てる必要があります。 ユーザーは、割り当てられているセキュリティ ロールに基づいてアプリにアクセスできます。
1. **[このアプリを共有する]**ダイアログ ボックスで、**[セキュリティ ロールをアプリに追加する]** を選んで、**[マイ アプリ]** を選びます。
2. Contoso Pet Grooming アプリのアプリ タイルの右下隅で、**[その他のオプション] (...)** を選んでから、**[ロールの管理]** を選びます。

    ![アプリのロールを管理する](media/share-model-driven-app/manage-roles.png)

4. **[ロール]** セクションでは、アプリへのアクセスをすべてのセキュリティ ロールまたは選んだロールのどちらに許可するかを選ぶことができます。 前に作成した "**Pet Grooming Schedulers**" および "**Pet Grooming Technicians**" ロールを選びます。

    ![アプリのセキュリティ ロールを選ぶ](media/share-model-driven-app/app-security-roles.png)

5. **[保存]** を選択します。
 
## <a name="share-the-link-to-your-app"></a>アプリへのリンクを共有する
1. **[このアプリを共有する]** ダイアログ ボックスで、**[アプリへのリンクをユーザーと直接共有する]** の下に表示されている URL をコピーします。
 
2. **[閉じる]** を選びます。
3. ユーザーがアクセスできる場所にアプリの URL を貼り付けます (SharePoint サイトへの掲示や、メールでの送信など)。

![リンクを共有する](media/share-model-driven-app/share-model-driven-URL.PNG)

アプリの URL は、アプリ デザイナーの **[プロパティ]** タブでも確認できます。 
    
![アプリの URL のコピー](media/share-model-driven-app/app-designer-copy-web-url.png)

## <a name="about-predefined-security-roles"></a>定義済みのセキュリティ ロールについて
これらの定義済みロールは、[!INCLUDE [powerapps](../../includes/powerapps.md)] 環境で利用できます。


|セキュリティ ロール  |*権限  |説明 |
|---------|---------|---------|
|環境作成者     |  なし       | アプリ、接続、カスタム API、ゲートウェイ、および Microsoft Flow を使用するフローなど、環境に関連付けられた新しいリソースを作成できます。 ただし、環境内のデータにアクセスする権限はありません。 詳細情報: [Environments overview](https://powerapps.microsoft.com/blog/powerapps-environments/) (環境の概要)        |
|システム管理者     |  作成、読み取り、書き込み、削除、カスタマイズ、セキュリティ ロール       | セキュリティ ロールの作成、変更、割り当てなど、環境のカスタマイズまたは管理の完全なアクセス許可を持っています。 環境内のすべてのデータを表示できます。 詳細情報: [カスタマイズに必要な特権](https://docs.microsoft.com/dynamics365/customer-engagement/customize/privileges-required-customization)        |
|システム カスタマイザー     | 作成 (自己)、読み取り (自己)、書き込み (自己)、削除 (自己)、カスタマイズ         | 環境をカスタマイズする完全なアクセス許可を持っています。 ただし、自身が作成した環境エンティティのレコードのみを表示できます。 詳細情報: [カスタマイズに必要な特権](https://docs.microsoft.com/dynamics365/customer-engagement/customize/privileges-required-customization)        |
|Common Data Service ユーザー     |  読み取り、作成 (自己)、書き込み (自己)、削除 (自己)       | 環境内でアプリを実行し、自分が所有するレコードについて共通タスクを実行できます。        |
|デリゲート     | 別のユーザーの代理で実行する        | 別のユーザーとしてコードを実行したり、偽装したりすることができます。  通常、別のセキュリティ ロールと併用してレコードへのアクセスを許可します。 詳細情報: [もう一方のユーザーの偽装](https://docs.microsoft.com/dynamics365/customer-engagement/developer/org-service/impersonate-another-user)        |

* 権限は、特記されていない限り、グローバル スコープです。

## <a name="next-steps"></a>次の手順
[クイック スタート: モバイル デバイスでモデル駆動型アプリを実行する](../../user/run-app-client-model-driven.md)



