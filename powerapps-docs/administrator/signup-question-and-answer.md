---
title: 組織内のライセンスの管理 | Microsoft Docs
description: Office 365 テナントにおける PowerApps のライセンスと管理、ユーザーのサインアップについて多く寄せられる質問とその回答
author: jamesol-msft
manager: kfile
ms.service: powerapps
ms.component: pa-admin
ms.topic: conceptual
ms.date: 03/21/2018
ms.author: jamesol
ms.openlocfilehash: 8a734ef57a3820e38d52ad2bd87a2ab8979c0348
ms.sourcegitcommit: b3b6118790d6b7b4285dbcb5736e55f6e450125c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2018
---
# <a name="manage-powerapps-licenses-in-your-organization"></a>組織内の PowerApps ライセンスの管理
この記事では、組織内のユーザーが PowerApps を使用するためのアクセス方法と、PowerApps サービスへのアクセスの制御方法について説明します。

## <a name="sign-up-for-powerapps"></a>PowerApps のサインアップ
### <a name="what-is-powerapps"></a>PowerApps とは
Microsoft PowerApps を使うと、Windows、iOS、Android モバイル デバイス用のアプリケーションを作成することができます。 これらのアプリを使って、Twitter、Office 365、Dropbox、Excel などの広く普及している SaaS サービスへの接続を作成することができます。

### <a name="how-do-users-sign-up-for-powerapps"></a>PowerApps にユーザーがサインアップする方法を教えてください
組織内の個々のユーザーが選択できるサインアップ方法は、PowerApps プラン 2 の試用版のみです。PowerApps Web サイトから次の方法でサインアップできます。

##### <a name="option-1"></a>方法 1
[powerapps.microsoft.com](https://powerapps.microsoft.com) にアクセスして **[無料でサインアップ]** を選択し、[portal.office.com](https://portal.office.com/Start?sku=powerapps) を通じて PowerApps のサインアップ プロセスを行うことでサインアップできます。

##### <a name="option-2"></a>方法 2
[powerapps.microsoft.com](https://powerapps.microsoft.com) にアクセスして **[サインイン]** を選択し、各自の職場アカウントまたは学校アカウントでサインインして PowerApps の使用条件に同意すれば PowerApps プラン 2 の試用版にサインアップできます。    

皆さんの組織内のユーザーが PowerApps にサインアップすると、そのユーザーには PowerApps のライセンスが自動的に割り当てられます。

> [!NOTE]
> PowerApps 内から試用版ライセンスにサインアップするユーザーは、Office 365 管理ポータルに PowerApps プラン 2 試用版のユーザーとして表示されません (Office 365、Dynamics 365、または PowerApps に対する別のライセンスを所有していない場合)。

詳細については、「[PowerApps のセルフサービス サインアップ](../maker/signup-for-powerapps.md)」を参照してください。

### <a name="how-can-users-in-my-organization-gain-access-to-powerapps"></a>組織内のユーザーが PowerApps を利用するためにはどうすればよいですか
組織内のユーザーは、次の 3 とおりの方法で PowerApps を利用することができます。

* 「[PowerApps にユーザーがサインアップする方法を教えてください](#how-do-users-sign-up-for-powerapps)」セクションに記載したように、個々のユーザーは PowerApps プラン 2 の試用版にサインアップできます。
* 2 つ目は、Office 365 管理ポータル内から、ユーザーに PowerApps ライセンスを割り当てる方法です。
* 3 つ目は、ユーザーに割り当てられている Office 365 プランと Dynamics 365 プランに含まれている PowerApps サービスを利用する方法です。 PowerApps の機能が含まれている Office 365 プランと Dynamics 365 プランのリストについては、[PowerApps の価格ページ](https://powerapps.microsoft.com/pricing)を参照してください。

### <a name="can-i-block-users-in-my-organization-from-signing-up-for-powerapps"></a>組織内のユーザーに PowerApps へのサインアップを禁止することはできますか
「[PowerApps にユーザーがサインアップする方法を教えてください](#how-do-users-sign-up-for-powerapps)」セクションで概説したように、Microsoft PowerApps プラン 2 の機能は、30 日間誰でも試すことができ、費用も発生しません。  これはテナント内のすべてのユーザーが利用できる選択肢であり、管理者が無効にすることはできません。試用期限が切れた後は、PowerApps プラン 2 の機能をユーザーは利用できなくなります。  

Microsoft PowerApps プラン 2 の試用版を個人で 30 日間サインアップした場合に、管理者が組織内でそれをサポートの対象外としている場合、貴社に料金が発生することは決してありません。 Microsoft PowerApps に個人でサインアップする場合、これはあくまで、Microsoft から提供されている多くのパブリック クラウド サービス (Bing、Wunderlist、OneDrive、Outlook.com など) と同様、その人と Microsoft との直接の関係になります。どのような形であれ、サービスが貴社から提供されていることにはなりません。

また、Microsoft PowerApps 内で社外秘のデータの扱いに制限を設けたい場合、データ損失防止 (DLP) ポリシーを通じて実現できます。 詳細については、「[Data loss prevention (DLP) policies (データ損失防止 (DLP) ポリシー)](prevent-data-loss.md)」を参照してください。

## <a name="administration-of-powerapps"></a>PowerApps の管理
### <a name="why-has-the-powerapps-icon-appeared-in-the-office-365-app-launcher"></a>Office 365 アプリ起動ツールに PowerApps のアイコンが表示されているのはなぜですか
Microsoft PowerApps は Office 365 スイートの基本的な一部であり、既存の Office 365 SKU の一部としてのサービスとして有効にされます。 世界中のユーザーが Microsoft PowerApps を利用できるようになったことから、アプリ起動画面の [すべてのアプリ] に表示されるようになっています。 Office 365 のどの SKU に PowerApps が追加されたかについては、「[Licensing overview (ライセンスの概要)](pricing-billing-skus.md)」を参照してください。

PowerApps タイルを既定の [すべてのアプリ] から削除したい場合は、次のセクションを参照してください。

### <a name="how-do-i-remove-powerapps-from-existing-users"></a>PowerApps を既存のユーザーから削除する方法を教えてください
PowerApps プラン 1 または PowerApps プラン 2 のライセンスがユーザーに割り当てられている場合、次の手順で PowerApps のライセンスをユーザーから削除することができます。

1. [Office 365 管理ポータル](https://portal.microsoftonline.com/)に移動します。

2. 左側のナビゲーション バーで、**[ユーザー]**、**[アクティブ ユーザー]** の順に選択します。

3. ライセンスの削除対象となるユーザーを見つけて、その名前を選択します。

4. ユーザーの詳細ウィンドウの **[Product licenses (製品ライセンス)]** セクションで **[編集]** を選択します。

5. **[Microsoft PowerApps Plan 1]** または **[Microsoft PowerApps Plan 2]** というライセンスを見つけ、**[オフ]** に切り替えて **[保存]** を選択します。

    ![](./media/signup-question-and-answer/remove-license.png)

ユーザーが Office 365 や Dynamics 365 プランのライセンスを通じて PowerApps を利用できる場合、次の手順に従って、PowerApps サービスの利用を無効にすることができます。

1. [Office 365 管理ポータル](https://portal.microsoftonline.com/)に移動します。

2. 左側のナビゲーション バーで、**[ユーザー]**、**[アクティブ ユーザー]** の順に選択します。

3. アクセス権の削除対象となるユーザーを見つけて、その名前を選択します。

4. ユーザーの詳細ウィンドウの **[Product licenses (製品ライセンス)]** セクションで **[編集]** を選択します。

5. ユーザーの Office 365 ライセンスまたは Dynamics 365 ライセンスを展開し、**[PowerApps for Office 365]** または **[PowerApps for Dynamics 365]** というサービスへのアクセスを無効にして **[保存]** を選択します。

    ![](./media/signup-question-and-answer/remove-service-plan.png)

PowerShell を使ってライセンスを一括削除することもできます。 詳しい例については、「[Remove licenses from user accounts with Office 365 PowerShell (Office 365 PowerShell を使ってユーザー アカウントからライセンスを削除する)](https://technet.microsoft.com/library/dn771774.aspx)」を参照してください。   また、ライセンスに含まれているサービスを一括削除する方法は、「[Disable access to services with Office 365 PowerShell (Office 365 PowerShell でサービスへのアクセスを無効にする)](https://technet.microsoft.com/library/dn771769.aspx)」にも説明されています。

PowerApps のライセンスまたはサービスが削除された組織内のユーザーは、次の場所からも、PowerApps または Dynamics 365 のアイコンが削除されます。

* [Office.com](https://office.com)

    ![](./media/signup-question-and-answer/office-home.png)
* Office 365 アプリ起動ツールの "ワッフル"

    ![](./media/signup-question-and-answer/office-waffle.png)

### <a name="how-can-i-restrict-my-users-ability-to-access-my-organizations-business-data-using-powerapps"></a>ユーザーが PowerApps を使用して組織のビジネス データにアクセスするのを制限するにはどうすればよいですか
PowerApps では、次に示すようにビジネス データ用と非ビジネス データ用の領域を作成することができます。  これらのデータ損失防止ポリシーが実施された後は、ビジネス データと非ビジネス データを組み合わせた PowerApps を設計したり実行したりすることができないようになります。 詳細については、「[Data loss prevention (DLP) policies (データ損失防止 (DLP) ポリシー)](prevent-data-loss.md)」を参照してください。

![](./media/signup-question-and-answer/data-loss-prevention-policy.png)

### <a name="why-did-10000-licenses-for-microsoft-powerapps-show-up-in-my-office-365-tenant"></a>Office 365 テナントに表示される Microsoft PowerApps のライセンス数が 10,000 となっていますが、これはなぜですか
資格を満たした組織のユーザーには、Microsoft PowerApps プラン 2 を 30 日間試用することが認められています。また、これらの試用版ライセンスは、貴社のテナント内の新規 PowerApps ユーザー数の上限を表しています。 これらのライセンスに関して料金は発生しません。 Office 365 管理ポータルに PowerApps (試用版) ライセンス数の上限として 10,000 が表示される理由は、具体的に 2 つ考えられます。

* 2016 年 4 月から 2016 年 10 月の期間に実施された PowerApps パブリック プレビューに参加したユーザーがテナントに 1 人でもいる場合、"Microsoft PowerApps and Logic flows" として 10,000 ライセンスが表示されます。

    ![](./media/signup-question-and-answer/licenses_2.png)
* 「[PowerApps にサインアップする方法を教えてください](#how-do-users-sign-up-for-powerapps)」セクションで説明した最初の方法 (**方法 1**) に従って PowerApps プラン 2 の試用版にサインアップしたユーザーがテナントに 1 人でもいる場合、"Microsoft Power Apps & Flow" として 10,000 ライセンスが表示されます。

    ![](./media/signup-question-and-answer/licenses_1.png)

Office 365 管理ポータルから、ユーザーに追加でライセンスを割り当てることはできますが、これらは Microsoft PowerApps プラン 2 の試用版ライセンスであり、ユーザーに割り当ててから 30 日後に有効期限が切れることに注意してください。

### <a name="is-this-free-will-i-be-charged-for-these-licenses"></a>これは無料ですか。 これらのライセンスに料金は発生しますか
これらのライセンスは、貴社のユーザーが Microsoft PowerApps プラン 2 を 30 日間試すための無料試用版ライセンスです。

### <a name="how-will-this-change-the-way-i-manage-identities-for-users-in-my-organization-today"></a>現在管理している組織内のユーザーに関して、その ID の管理方法はどのように変わるのでしょうか
既存の Office 365 環境が貴社に存在し、組織内のすべてのユーザーが Office 365 アカウントを持っているのであれば、ID 管理に変更は生じません。

既存の Office 365 環境が貴社に存在するものの、Office 365 アカウントを持たないユーザーが組織内にいる場合は、Microsoft がテナントにユーザーを作成し、その職場または学校の電子メール アドレスに基づいてライセンスを割り当てます。 つまり、特定の時点で皆さんの管理下にあるユーザーの数は、組織内のユーザーがサービスにサインアップするごとに増えていくことになります。

ご利用の Office 365 環境が貴社の電子メール ドメインに接続されていなければ、ID の管理方法は変わりません。 ユーザーは新しいクラウド専用のユーザー ディレクトリに追加されることになります。管理者は、それらのユーザーをテナント管理者として引き継いで管理するかどうかを選ぶことができます。

### <a name="what-is-the-process-to-manage-a-tenant-created-by-microsoft-for-my-users"></a>Microsoft が私の管理下にあるユーザー用に作成したテナントは、どのようなプロセスで管理されますか
Microsoft によって作成されたテナントは、管理者が次の手順で要求し、管理することができます。

1. 管理対象となるテナント ドメインと同じ電子メール アドレス ドメインを使って PowerApps にサインアップし、テナントに参加します。 たとえば Microsoft によって作成されたテナントが contoso.com である場合、@contoso.com で終わる電子メール アドレスでそのテナントに参加します。
2. ドメイン所有権を証明することによって管理制御権を要求します。つまりテナントに参加したら、ドメインの所有権があることを証明することによって、自分自身を管理者ロールに昇格することができます。 これを行うには、次の手順に従います。
3. [https://portal.office.com](https://portal.office.com/Start?sku=powerapps) に移動します。
4. 左上隅のアプリ起動ツール アイコンを選択し、[管理者] を選択します。
5. **[Become the admin (管理者になる)]** ページの指示を読んで、**[Yes, I want to be the admin (はい。管理者になります)]** を選択します。  

> [!NOTE]
> このオプションが表示されない場合は、Office 365 管理者が既に存在します。

### <a name="if-i-have-multiple-domains-can-i-control-the-office-365-tenant-that-users-are-added-to"></a>複数のドメインがある場合、管理者として、ユーザーの追加先となる Office 365 テナントを制御することはできますか
何もしなければ、ユーザーの電子メール ドメインとサブドメインごとにテナントが作成されます。

すべてのユーザーを、その電子メール アドレスの拡張子に関係なく同じテナントに含める場合は、次の操作を行ってください。  

* 事前に対象テナントを作成するか、既存のテナントを使用します。 そのテナントに含める既存のドメインとサブドメインをすべて追加します。 以後、電子メール アドレスの末尾がこれらのドメインとサブドメインに該当するすべてのユーザーは、サインアップ時に自動的に対象テナントに追加されます。

> [!IMPORTANT]
> いったん作成されたテナント間でユーザーを自動的に移動するためのメカニズムは用意されていません。 単一の Office 365 テナントにドメインを追加する方法については、[ユーザーとドメインを Office 365 に追加する方法](https://support.office.com/article/Add-your-users-and-domain-to-Office-365-ffdb2216-330d-4d73-832b-3e31bcb5b2a7)に関するページを参照してください。
