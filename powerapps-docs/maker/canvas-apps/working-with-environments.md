---
title: 環境に応じた作業 | Microsoft Docs
description: 環境を切り替えて、ページ上の内容がどのように変わるかを理解しましょう。
author: linhtranms
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: anneta
ms.date: 10/14/2016
ms.author: litran
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: c4e02adfdd5c1c4e49bb1a605ccfff463369f750
ms.sourcegitcommit: 429b83aaa5a91d5868e1fbc169bed1bac0c709ea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/24/2018
ms.locfileid: "42835292"
---
# <a name="working-with-environments-and-microsoft-powerapps"></a>Microsoft PowerApps で環境を使用する
PowerApps では、異なる環境での作業が可能で、それらを簡単に切り替えることができます。 環境の概要については、[環境の概要](../../administrator/environments-overview.md) を参照してください。なぜ複数環境を使うのか、どのように環境の作成と管理を行えばよいか、を詳しく説明しています。 この記事では、環境に関する次のトピックを取り上げます。

* 環境を powerapps.com に切り替える方法
* 適切な環境でアプリを作成する方法
* 適切な環境でアプリを表示する方法

## <a name="switch-the-environment"></a>環境を切り替える
powerapps.com にサインアップした後の初めてのサインインでは、ほとんどの場合既定の環境が提供されます。 ページの右上隅で確認することができます。

![既定の環境](./media/working-with-environments/env-dropdown.png)

*既定の環境* はすべてのユーザーでアクセス可能です。 この環境でアプリの作成を開始し、他のユーザーとアプリを共有することができます。 [自分で作成](../../administrator/environments-administration.md) したもの、または他のユーザーによって作成されてアクセス権を持っているもの、など他の環境にアクセスすることもできます。 右上隅にある環境ドロップダウンをクリックし、別の環境を選択して、環境を切り替えることができます。 この例は、*既定の環境* から*環境 1* への切り替えを示しています。

![環境の切り替え](./media/working-with-environments/switch-env.png)

別の環境 (環境 1 など) に切り替えると、その環境内で作成したアプリまたはアクセス権のあるアプリのすべてが表示されます。

## <a name="create-apps-in-the-right-environment"></a>適切な環境でアプリを作成する
ご自分で作成する環境、またはアクセス権が付与されている環境でアプリを作成することができます。 ただし、独自の環境を作成するには、[具体的なプラン](../../administrator/pricing-billing-skus.md)が必要です。 アプリを作成する前に、必ず **アプリに使用する正しい環境を選択しているかどうか確認**します。 そうしないと、環境間でのアプリの移行処理が必要になります。

適切な環境でアプリを作成するには、次のいずれかの操作を行います。

- PowerApps Studio が開いていない場合は、[サインイン](http://web.powerapps.com?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc)し、アプリを作成する環境を選択します。次に、左端近くにある **[アプリ]** を選択し、**[アプリの作成]** を選びます。

- PowerApps Studio が開いたら、再び右上隅で環境を選択します。

5. **[アカウント]** ページで、現在の環境名の横にある **[変更]**  を選択します。

6. アプリを作成する環境を選択します。

    ![Studio 環境の切り替え](./media/working-with-environments/studio-env-dropdown2.PNG)

7. **[新規]** を選択してアプリの作成を開始します。 これで、アプリは、手順 6 で選択した環境に保存されます。

    ![Studio 環境の切り替え](./media/working-with-environments/new-app.PNG)

## <a name="view-apps-in-the-right-environment"></a>適切な環境でアプリを作成する
[powerapps.com](http://web.powerapps.com?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc) と PowerApps Studio のどちらで作業しているかに関係なく、アプリや接続などの一覧は常に、ドロップダウン リストで選択されている環境に基づいてフィルター表示されます。 探しているアプリが表示されない場合は、正しい環境が選択されているか確認してください。

環境の詳細については、 [この概要](../../administrator/environments-overview.md)を参照してください。
