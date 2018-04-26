---
title: 環境に応じた作業 | Microsoft Docs
description: 環境を切り替えて、ページ上の内容がどのように変わるかを理解しましょう。
documentationcenter: na
author: linhtranms
manager: kfile
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: conceptual
ms.component: canvas
ms.date: 10/14/2016
ms.author: litran
ms.openlocfilehash: fa1dcd264e99a2bea333d7b6aa0bbf2e04cd47e9
ms.sourcegitcommit: 8bd4c700969d0fd42950581e03fd5ccbb5273584
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="working-with-environments-and-microsoft-powerapps"></a>Microsoft PowerApps で環境を使用する
PowerApps では、異なる環境での作業が可能で、それらを簡単に切り替えることができます。 環境の概要については、[環境の概要](../../administrator/environments-overview.md) を参照してください。なぜ複数環境を使うのか、どのように環境の作成と管理を行えばよいか、を詳しく説明しています。 この記事では、環境に関する次のトピックを取り上げます。

* 環境を powerapps.com に切り替える方法
* 適切な環境でアプリを作成する方法
* 適切な環境でアプリを表示する方法

## <a name="switch-the-environment"></a>環境を切り替える
powerapps.com にサインアップした後の初めてのサインインでは、ほとんどの場合既定の環境が提供されます。 ページの右上隅で確認することができます。

![既定の環境](./media/working-with-environments/env-dropdown.png)

*既定の環境* はすべてのユーザーでアクセス可能です。 この環境でアプリの作成を開始し、他のユーザーとアプリを共有することができます。 [自分で作成](../../administrator/environments-administration.md) したもの、または他のユーザーによって作成されてアクセス権を持っているもの、など他の環境にアクセスすることもできます。 右上隅にある環境ドロップダウンをクリックし、別の環境を選択して、環境を切り替えることができます。 この例では、*既定の環境* から *環境 1* に切り替えています。

![環境の切り替え](./media/working-with-environments/switch-env.png)

別の環境 (環境 1 など) に切り替えると、その環境内で作成したアプリまたはアクセス権のあるアプリのすべてが表示されます。

## <a name="create-apps-in-the-right-environment"></a>適切な環境でアプリを作成する
アプリの作成は、アクセスがある既存の環境や、新しい環境で可能です。 ただし、独自の環境を作成するには、具体的なプランが必要です。 詳細については、[このトピック](../../administrator/pricing-billing-skus.md) を参照してください。 アプリを作成する前に、必ず **アプリに使用する正しい環境を選択しているかどうか確認**します。 そうしないと、環境間でのアプリの移行処理が必要になります。

1. [powerapps.com](http://web.powerapps.com) をお使いの場合は、アプリを作成したい環境を選択します。 *PowerApps Studio* または *web 対応の PowerApps Studio* をお使いの場合は、手順 4 に進みます。

2. **[+ New app]\(+ 新しいアプリ\)** を選択します。

3. **[PowerApps Studio を開く]** または **[Web 用の PowerApps Studio]** を選択します。

4. *PowerApps Studio* または web 対応の *PowerApps Studio* が開いたら、再び右上隅で環境を選択します。 この動作は今後改善していきますが、現在のリリースでは、新しい環境でアプリを作成するたびにこの選択の操作が必要です。

    ![Studio 環境の切り替え](./media/working-with-environments/studio-switch-env.PNG)

5. **[アカウント]** ページで、現在の環境名の横にある **[変更]**  を選択します。

    ![Studio 環境の切り替え](./media/working-with-environments/studio-env-dropdown.PNG)

6. アプリを作成する環境を選択します。

    ![Studio 環境の切り替え](./media/working-with-environments/studio-env-dropdown2.PNG)

7. **[新規]** を選択してアプリの作成を開始します。 これで、アプリは、手順 6 で選択した環境に保存されます。

    ![Studio 環境の切り替え](./media/working-with-environments/new-app.PNG)

## <a name="view-apps-in-the-right-environment"></a>適切な環境でアプリを作成する
[powerapps.com](http://web.powerapps.com)、PowerApps Studio for Windows、PowerApps Studio for web のいずれで作業していても、アプリや接続の一覧は、常に、ドロップダウン リストで選択されている環境に基づいてフィルター表示されます。 探しているアプリが表示されない場合は、正しい環境が選択されているか確認してください。

[powerapps.com](http://web.powerapps.com)環境に切り替えるには: 

![環境の切り替え](./media/working-with-environments/switch-env.png)

PowerApps Studio for Windows または PowerApps Studio for web で環境を切り替えるには:

![Studio 環境の切り替え](./media/working-with-environments/studio-switch-env.PNG)

環境の詳細については、 [この概要](../../administrator/environments-overview.md)を参照してください。
