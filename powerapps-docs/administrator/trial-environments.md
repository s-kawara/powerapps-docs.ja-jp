---
title: 試用版環境 | Microsoft Docs
description: PowerApps プレビュー プログラムで機能を先行試用する
author: manasmams
manager: kvivek
ms.service: powerapps
ms.component: pa-admin
ms.topic: conceptual
ms.date: 01/09/2019
ms.author: manasma
search.audienceType:
- admin
search.app:
- D365CE
- PowerApps
- Powerplatform
ms.openlocfilehash: bd05c4c1251058d464034de71d9b1c287e714190
ms.sourcegitcommit: 170deba334c922157bbb826c795bed3fa858b85e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/10/2019
ms.locfileid: "54196142"
---
# <a name="about-trial-environments"></a>試用版環境について

現在のところ、Common Data Service (CDS) for Apps 環境として試用版環境または運用環境を作成できます。 Dynamics 365 for Customer Engagement アプリを無料で試す場合、試用版環境が便利です。 試用版環境は 30 日後に期限切れとなります。

**[環境]** ページを開くと、自分に与えられている環境の種類や試用版環境の有効期限を確認できます。

> [!div class="mx-imgBorder"] 
> ![PowerApps 環境](media/powerapps-environments75b.png "PowerApps 環境")

## <a name="convert-a-trial-environment-to-production"></a>試用版環境を運用環境に切り替える

試用版環境を使用しているとき、30 日以上保持したいリソースが作成された場合、試用版を運用環境に切り替えます。

運用環境に切り替えるには、次の条件を満たす必要があります。

**適切な PowerApps プラン**。 PowerApps プラン 2 など、運用環境を作成できるプラン。 運用環境が含まれる PowerApps プランの詳細については、「[チームに適したプランを選ぶ](https://powerapps.microsoft.com/pricing/)」を参照してください。 ご利用の PowerApps プランを確認する方法については、「[プランはどのような方法で確認できますか](#how-do-i-identify-my-plans)」を参照してください。
**利用できる運用クォータ**。 ご利用のプランで作成できる運用環境の数が決まっています。 たとえば、PowerApps プラン 2 の場合、実稼働環境を 2 つ作成できます。 運用環境を 2 つ既に作成している場合、1 つ削除しない限り、新しく作成できません。 詳細については、「[環境の作成](environments-overview.md#creating-an-environment)」を参照してください。

次の手順で試用版環境を運用環境に切り替えます。

1. [https://admin.powerapps.com/environments](https://admin.powerapps.com/environments) に移動し、管理者としてサインインします。
 
2. **[環境]** ページを開き、運用環境に切り替える試用版環境を選択します。

    > [!div class="mx-imgBorder"] 
    > ![試用版環境の選択](media/powerapps-environments75b-select-trial.png "試用版環境の選択")

3. **[詳細]** タブで **[変換]** を選択します。

    > [!div class="mx-imgBorder"] 
    > ![[変換] を選択する](media/powerapps-trial-select-convert.png "[変換] を選択する")

4. **[確定]** を選択します。

    > [!div class="mx-imgBorder"] 
    > ![[確定] を選択する](media/powerapps-trial-select-confirm.png "[確定] を選択する")

環境にデータベースが含まれる場合、運用環境への切り替えには数時間かかることがあります。 **[詳細]** タブの通知で進捗状況を監視できます。

  > [!div class="mx-imgBorder"] 
  > ![変換開始](media/powerapps-trial-conversion-started.png "変換開始")

## <a name="frequently-asked-questions"></a>よく寄せられる質問

### <a name="who-can-convert-a-trial-environment-to-a-production-environment"></a>試用版環境を運用環境に切り替えることができるのは誰ですか。

試用版環境を運用環境に切り替えるには、次の条件を満たす必要があります。

**適切な PowerApps プランを持っている**。 PowerApps プラン 2 など、運用環境を作成できるプランが必要です。 運用環境が含まれる PowerApps プランの詳細については、「[チームに適したプランを選ぶ](https://powerapps.microsoft.com/pricing/)」を参照してください。 ご利用の PowerApps プランを確認する方法については、「[プランはどのような方法で確認できますか](#how-do-i-identify-my-plans)」を参照してください。
**利用できる運用クォータを持っている**。 ご利用のプランで作成できる運用環境の数が決まっています。 たとえば、PowerApps プラン 2 の場合、実稼働環境を 2 つ作成できます。 2 つ既に作成している場合、1 つ削除しない限り、新しく作成できません。

### <a name="what-if-i-dont-have-available-quota-for-production-environments"></a>運用環境に利用できるクォータがない場合はどうすればよいですか。

Office 365 グローバル管理者か Azure Active Directory (Azure AD) テナント管理者に次を要請してください。
- PowerApps プラン 2 をあなたに割り当てる。 
- 利用できる運用環境クォータが与えられている別のユーザーを見つける。

PowerApps プランを購入することもできます。

### <a name="can-every-office-365-global-admin-or-azure-ad-tenant-admin-convert-a-trial-environment-to-a-production-environment"></a>Office 365 グローバル管理者か Azure AD テナント管理者であれば、誰でも試用版環境を運用環境に切り替えることができますか。

いいえ。 グローバル管理者や Azure AD テナントの管理者が試用版環境を運用環境に切り替えるには、運用環境に利用できるクォータを必要とします。

### <a name="is-there-a-way-to-recover-a-deleted-trial-environment"></a>削除した試用版環境を回復する方法はありますか。

削除した試用版環境の回復は保証できませんが、削除から 7 日以内であれば最善を尽くします。 環境のデータベースを回復することはできませんが、(PowerApps で作成された) アプリやフローは回復できます。

### <a name="how-can-i-retain-my-data-and-resources-if-i-dont-have-a-way-to-convert-the-trial-environment-to-a-production-environment"></a>試用版環境を運用環境に切り替える手段がないとき、データやリソースを保持する方法はありますか。

データやリソースは別の環境にエクスポートできます。 長期間保持するなら、(PowerApps Community Plan で) 運用環境か個別の環境を作成し、その環境にリソースをエクスポートすることをお勧めします。 

リソースをエクスポートする際のガイドラインは次のようになります。

|環境内のリソースの種類  |エクスポート方法  |
|---------|---------|
|アプリ (キャンバスとモデル駆動型) とフロー     |[パッケージング](environment-and-tenant-migration.md)を使用し、1 つの環境からアプリとフローをエクスポートできます。         |
|データベースのデータ (Common Data Service (CDS) for Apps 環境)     |次の選択肢があります。<br/><ul><li>[Excel にエクスポート](../user/export-data-excel.md)し、データを保存します。 別の環境に[データをインポート](../user/import-data.md)できます。</li><br/><li>[Data Integrator サービス](data-integrator.md)と API を使用し、別の環境にデータをエクスポートできます。</li></ul> |

環境データベースでアクティビティが 30 日間なかった場合、Microsoft は試用版環境を削除します。

### <a name="how-can-i-create-a-production-or-an-individual-environment"></a>運用環境または個別の環境はどのような方法で作成できますか。

運用環境を作成できる PowerApps プランが必要です。 詳細については、「[環境の作成](environments-overview.md#creating-an-environment)」を参照してください。

[PowerApps Community Plan](https://powerapps.microsoft.com/communityplan/) に新規登録することで個別の環境を作成できます。 個別の環境でアプリを共有する場合、個人使用のみが許可されるという制約があることにご留意ください。

### <a name="how-do-i-identify-my-plans"></a>プランはどのような方法で確認できますか。

ご利用のプランを確認するには、PowerApps サイトの右上隅にある**歯車**アイコンを選択し、**[プラン]** を選択します。

> [!div class="mx-imgBorder"] 
> ![プランの選択](media/powerapps-plans.png "プランの選択")

### <a name="see-also"></a>関連項目
[PowerApps での環境の管理](environments-administration.md)<br/>
[環境の概要](environments-overview.md)<br/>
[チームに適したプランを選びます](https://powerapps.microsoft.com/pricing/)<br/>
[ライセンスの概要](pricing-billing-skus.md)<br/>
