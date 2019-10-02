---
title: ソリューションにキャンバスアプリを作成する |Microsoft Docs
description: PowerApps では、別の環境にアプリを配置できるように、ソリューションにキャンバスアプリを作成します。
author: AFTOwen
manager: kvivek
ms.service: powerapps
ms.topic: article
ms.custom: canvas
ms.reviewer: ''
ms.date: 10/23/2018
ms.author: anneta
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 3703fc5e36b38c7894300bc2074453716ddd9946
ms.sourcegitcommit: 60fd1792430b9f3da08ec161cb2277506d795e3a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2019
ms.locfileid: "71705085"
---
# <a name="create-a-canvas-app-from-within-a-solution"></a>ソリューション内からキャンバスアプリを作成する

たとえば、アプリを別の環境にデプロイする場合は、ソリューション内からアプリを作成します。 ソリューションには、アプリだけでなく、カスタマイズされたエンティティ、オプションセット、およびその他のコンポーネントも含めることができます。 ソリューション内からアプリやその他のコンポーネントを作成し、ソリューションをエクスポートして、別の環境にインポートすることで、さまざまな方法で環境をすばやくカスタマイズできます。

ソリューションの詳細については、「[ソリューションの概要](../common-data-service/solutions-overview.md)」を参照してください。

## <a name="prerequisite"></a>前提条件

このトピックの手順を実行するには、Common Data Service データベースを含む環境に切り替える必要があります。

## <a name="create-a-solution"></a>ソリューションを作成する

アプリを作成する、またはアプリをリンクするソリューションが既にある場合は、この手順を省略できます。

1. PowerApps に[サインイン](https://web.powerapps.com?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc)し、必要に応じて適切な環境に切り替えます。

    - ソリューション内からアプリを作成する場合は、Common Data Service データベースを含む任意の環境に切り替えます。
    - 既存のアプリをソリューションにリンクする場合は、そのアプリを含む環境に切り替えます。

1. 左側のナビゲーションバーで、 **[ソリューション]** を選択します。

    > [!div class="mx-imgBorder"]
    > 左側のナビゲーションバーの左側のナビゲーションバー(./media/add-app-solution/left-nav.png "ソリューションオプション")の![[ソリューション] オプション]

1. タイトルバーの下のバナーで、 **[新しいソリューション]** を選択します。

    > [!div class="mx-imgBorder"]
    > バナーの [(./media/add-app-solution/banner-new-solution.png "新しいソリューション] オプション")の![[新規ソリューション] オプション]

1. 表示されるウィンドウで、ソリューションの表示名、発行元、およびバージョンを指定します。

    > [!div class="mx-imgBorder"]
    > (./media/add-app-solution/configure-new-solution.png "新しいソリューションの")![新しいソリューションオプションのオプション]

    指定した表示名に基づいて (スペースなしの) 名前が自動的に生成されますが、必要に応じて生成された名前をカスタマイズできます。 環境に合わせて既定のパブリッシャーを指定できます。また、これらの領域に特定のニーズがない場合は、 **1.0**のバージョンを指定できます。

1. 左上隅の近くにある **[保存して閉じる]** を選択します。

    > [!div class="mx-imgBorder"]
    > ![新しいソリューションを保存]する(./media/add-app-solution/save-new-solution.png "新しいソリューションを保存する")

## <a name="create-a-canvas-app-in-a-solution"></a>ソリューションにキャンバスアプリを作成する

ソリューション内から空のキャンバスアプリを作成できます。 3画面アプリを自動的に生成したり、ソリューション内からテンプレートやサンプルアプリをカスタマイズしたりすることはできません。

1. PowerApps に[サインイン](https://web.powerapps.com?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc)します。

1. 必要に応じて、キャンバスアプリを作成するソリューションを含む環境に切り替えます。

1. 左側のナビゲーションバーで、 **[ソリューション]** を選択します。

    > [!div class="mx-imgBorder"]
    > 左側のナビゲーションバーの左側のナビゲーションバー(./media/add-app-solution/left-nav.png "ソリューションオプション")の![[ソリューション] オプション]

1. ソリューションの一覧で、キャンバスアプリを作成するソリューションを選択します。

1. タイトルバーの下のバナーで、[**新規** > **アプリ** > **キャンバスアプリ**] を選択し、作成するアプリのフォームファクター (電話またはタブレット) を選択します。

    > [!div class="mx-imgBorder"]
    > ソリューション(./media/add-app-solution/new-option.png "にアプリを作成するため")の![ソリューションオプションでアプリを作成するオプション]

    PowerApps Studio、別のブラウザータブに空白のキャンバスが表示されます。

1. アプリを作成し (または、少なくとも1つの変更を加え)、変更を保存します。

1. ソリューションを選択した ブラウザー タブで、**完了** を選択してソリューション内のコンポーネントの一覧を更新します。

    > [!div class="mx-imgBorder"]
    > 完了![ボタン]の(./media/add-app-solution/done-button.png "完了ボタン")

    新しいアプリが、そのソリューションのコンポーネントの一覧に表示されます。 アプリに変更を保存すると、ソリューション内のバージョンに反映されます。

## <a name="link-an-existing-canvas-app-to-a-solution"></a>既存のキャンバスアプリをソリューションにリンクする

アプリをソリューションにリンクする場合は、両方が同じ環境に存在し、アプリがソリューション内から作成されている必要があります。

1. PowerApps に[サインイン](https://web.powerapps.com?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc)します。

1. 必要に応じて、アプリをリンクするソリューションを含む環境に切り替えます。

1. 左側のナビゲーションバーで、 **[ソリューション]** を選択します。

    > [!div class="mx-imgBorder"]
    > 左側のナビゲーションバーの左側のナビゲーションバー(./media/add-app-solution/left-nav.png "ソリューションオプション")の![[ソリューション] オプション]

1. ソリューションの一覧で、アプリをリンクするソリューションを選択します。

1. タイトルバーの下のバナーで、[**既存**の @no__t の追加]-1**アプリ** > **キャンバスアプリ**を選択します。

    > [!div class="mx-imgBorder"]
    > 既存のアプリをリンクするために既存のアプリケーション(./media/add-app-solution/add-existing.png "バナーオプション")を![リンクするバナーオプション]

    この環境でソリューション内に作成されたキャンバスアプリの一覧が表示されます。

1. アプリの一覧で、ソリューションにリンクするアプリを選択し、 **[追加]** を選択します。

    > [!div class="mx-imgBorder"]
    > ![ボタン](./media/add-app-solution/add-button.png "の追加ボタン")を追加する

## <a name="known-limitations"></a>既知の制限

既知の制限事項については、「 [PowerApps でのソリューションの使用](../common-data-service/use-solution-explorer.md#known-limitations)」を参照してください。 

## <a name="next-steps"></a>次の手順

- 他のアプリや[その他のコンポーネント](../common-data-service/use-solution-explorer.md)(エンティティ、フロー、ダッシュボードなど) を作成するか、ソリューションにリンクします。
- [ソリューションをエクスポート](../common-data-service/import-update-export-solutions.md)して、別の環境、appsource、などにデプロイできるようにします。
