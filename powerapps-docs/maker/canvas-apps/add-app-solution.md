---
title: ソリューションでキャンバス アプリの作成 |Microsoft Docs
description: PowerApps では、別の環境にアプリをデプロイできるようににソリューションでキャンバス アプリを作成します。
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
ms.openlocfilehash: dcb6a9c69e602b739d58afde2242d18b60e6f477
ms.sourcegitcommit: 5b2b70c3fc7bcba5647d505a79276bbaad31c610
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/22/2019
ms.locfileid: "58356818"
---
# <a name="create-a-canvas-app-from-within-a-solution"></a>ソリューション内からキャンバス アプリを作成します。

たとえば、別の環境にアプリをデプロイする場合は、ソリューションからのアプリを作成します。 ソリューションには、だけでなくアプリが、またカスタマイズされたエンティティ、オプション セット、およびその他のコンポーネントを含めることができます。 すぐに、アプリやその他のコンポーネントは、ソリューション内からを作成し、ソリューションをエクスポートして、別の環境にインポートすることのさまざまな方法で環境をカスタマイズできます。

ソリューションは、for Customer Engagement、Dynamics 365 と同じプラットフォームに基づいて構築されます。 詳細については、[ソリューションの概要](../common-data-service/solutions-overview.md)を参照してください。

## <a name="prerequisite"></a>前提条件

このトピックの手順を実行するには、Common Data Service データベースが格納されている環境を切り替える必要があります。

## <a name="create-a-solution"></a>ソリューションを作成する

アプリを作成するのには、またはアプリをリンクするのには、ソリューションが既にある場合は、この手順を省略できます。

1. [サインイン](https://web.powerapps.com?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc)PowerApps にし、必要に応じて、適切な環境に切り替えます。

    - ソリューション内からアプリを作成する場合は、Common Data Service データベースを含む任意の環境に切り替えます。
    - ソリューションに既存のアプリをリンクする場合は、そのアプリを含む環境に切り替えます。

1. 左側のナビゲーション バーで、選択**ソリューション**します。

    > [!div class="mx-imgBorder"]
    > ![ソリューションは、左側のナビゲーション バーでオプション](./media/add-app-solution/left-nav.png "左側のナビゲーション バーで、ソリューション オプション")

1. タイトル バーの下のバナーで**新しいソリューション**します。

    > [!div class="mx-imgBorder"]
    > ![新しいソリューションのオプションのバナーで](./media/add-app-solution/banner-new-solution.png "バナーで新規ソリューション オプション")

1. ウィンドウが表示されたら、表示名、発行元、およびソリューションのバージョンを指定します。

    > [!div class="mx-imgBorder"]
    > ![新しいソリューションのオプション](./media/add-app-solution/configure-new-solution.png "新しいソリューションのオプション")

    指定した表示名に基づいて自動的に (スペースなし) が付いた名前が生成されますが、する場合は、生成された名前をカスタマイズすることができます。 既定の発行者を指定するには、環境と**1.0**バージョンについては特定のニーズがこれらの領域にしていない場合。

1. 左上隅近く**を保存して閉じます**します。

    > [!div class="mx-imgBorder"]
    > ![新しいソリューションを保存](./media/add-app-solution/save-new-solution.png "新しいソリューションを保存")

## <a name="create-a-canvas-app-in-a-solution"></a>ソリューションでキャンバス アプリを作成します。

ソリューション内の空白のキャンバス アプリを作成することができます。 自動的に 3 画面アプリを生成したり、ソリューション内から、テンプレート、またはサンプル アプリをカスタマイズできません。

1. [サインイン](https://web.powerapps.com?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc)PowerApps にします。

1. 必要に応じて、キャンバス アプリを作成するソリューションが含まれる環境に切り替えます。

1. 左側のナビゲーション バーで、選択**ソリューション**します。

    > [!div class="mx-imgBorder"]
    > ![ソリューションは、左側のナビゲーション バーでオプション](./media/add-app-solution/left-nav.png "左側のナビゲーション バーで、ソリューション オプション")

1. ソリューションの一覧では、キャンバス アプリを作成するソリューションを選択します。

1. タイトル バーの下のバナーで**新規** > **アプリ** > **キャンバス アプリ**、し、アプリのフォーム ファクター (スマート フォンやタブレット) します。作成するには。

    > [!div class="mx-imgBorder"]
    > ![ソリューションでアプリを作成するためのオプション](./media/add-app-solution/new-option.png "ソリューションでアプリを作成するためのオプション")

    PowerApps Studio は、別のブラウザー タブで空白のキャンバスでが開きます。

1. アプリの作成 (または、少なくとも 1 つの変更を行う)、変更を保存します。

1. ソリューションを選択したブラウザー タブで、次のように選択します。**完了**、ソリューションのコンポーネントの一覧を更新します。

    > [!div class="mx-imgBorder"]
    > ![[完了] ボタン](./media/add-app-solution/done-button.png "[完了] ボタン")

    新しいアプリは、そのソリューションのコンポーネントの一覧に表示されます。 アプリに変更を保存する場合は、ソリューション内にあるバージョンに反映されます。

## <a name="link-an-existing-canvas-app-to-a-solution"></a>ソリューションに既存のキャンバス アプリをリンクします。

ソリューションにアプリをリンクする場合は、同じ環境である必要があります両方と、アプリする必要がありますから作成されたソリューション内で。

1. [サインイン](https://web.powerapps.com?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc)PowerApps にします。

1. 必要に応じて、アプリをリンクするソリューションが含まれる環境に切り替えます。

1. 左側のナビゲーション バーで、選択**ソリューション**します。

    > [!div class="mx-imgBorder"]
    > ![ソリューションは、左側のナビゲーション バーでオプション](./media/add-app-solution/left-nav.png "左側のナビゲーション バーで、ソリューション オプション")

1. ソリューションの一覧では、アプリをリンクするソリューションを選択します。

1. タイトル バーの下のバナーで**既存の追加** > **アプリ** > **キャンバス アプリ**します。

    > [!div class="mx-imgBorder"]
    > ![既存のアプリをリンクするためのオプションのバナー](./media/add-app-solution/add-existing.png "既存のアプリをリンクするためのオプションのバナー")

    この環境でのソリューション内で作成されたキャンバス アプリの一覧が表示されます。

1. アプリの一覧で、ソリューションにリンクしを選択するアプリを選択します。**追加**します。

    > [!div class="mx-imgBorder"]
    > ![[追加] ボタン](./media/add-app-solution/add-button.png "追加 ボタン")

## <a name="known-limitations"></a>既知の制限

既知の制限事項については、[ソリューションを使用して、PowerApps で](../common-data-service/use-solution-explorer.md#known-limitations)を参照してください。 

## <a name="next-steps"></a>次の手順

- 作成またはその他のアプリのリンクと[他のコンポーネント](../common-data-service/use-solution-explorer.md)エンティティ、フロー、およびソリューションのダッシュ ボードなど。
- [ソリューションをエクスポート](../common-data-service/import-update-export-solutions.md)AppSource で、別の環境にデプロイされなどようにします。
