---
title: モデル駆動型サンプル アプリ
description: モデル駆動型サンプル アプリを取得、カスタマイズ、削除する方法を理解できます。
documentationcenter: na
author: mr-dang-msft
manager: kvivek
ms.service: powerapps
ms.devlang: na
ms.topic: conceptual
ms.component: model
ms.date: 03/08/2018
ms.author: brdang
search.audienceType:
  - maker
search.app:
  - PowerApps
  - D365CE
---

# <a name="model-driven-sample-apps"></a>モデル駆動型サンプル アプリ

[powerapps.com](https://powerapps.com) で、サンプル アプリを使ってデザインの可能性について調べ、独自のアプリの開発時に適用できる概念を知ります。 各サンプル アプリは、実際のシナリオを示すために架空のデータを使用します。 

詳しくは、各サンプル アプリに固有のドキュメントをご覧ください。 

![資金調達サンプル アプリ](media/overview-model-driven-samples/fundraiser-app1.png)


## <a name="get-sample-apps"></a>サンプル アプリの入手

モデル駆動型サンプル アプリ再生または編集するには、アプリをまず Common Data Service データベースでプロビジョニングする必要があります。 まず、試用環境およびデータベースを作成し、必ず **サンプル アプリとデータを含める** をオンにしてください。

![データベースの作成](media/overview-model-driven-samples/create-database1.png)


> [!IMPORTANT]
> このオプションは、データベースに使用可能なすべてのサンプル アプリをインストールします。 サンプル アプリは、学習およびデモ用であるため、運用データベースにインストールしないことをお勧めします。 

## <a name="customize-a-sample-app"></a>サンプル アプリのカスタマイズ

1. [powerapps.com](https://powerapps.com) へのサインイン  

    

2. **作成**ページから、サンプル アプリの上にマウス カーソルを置き、**このアプリを作成**をクリックします。

![モデル サンプル アプリ](media/overview-model-driven-samples/model-driven-create-page-sample.png)

3. アプリ デザイナーが開き、アプリをカスタマイズするための複数のオプションが表示されます。 
4. 追加のカスタマイズ オプションの場合、ポータルの左側のナビゲーションから **詳細設定** をクリックします。

## <a name="remove-sample-apps-and-data"></a>サンプル アプリおよびデータの削除 
- サンプル アプリを削除するには、対応する[管理ソリューション](https://docs.microsoft.com/dynamics365/customer-engagement/developer/uninstall-delete-solution)を削除する必要があります。 
- ソリューションを削除すると、アプリのユーザー定義エンティティに固有のサンプル データも削除されます。
- カスタマイズがサンプル アプリに行われた場合、[依存関係](https://docs.microsoft.com/dynamics365/customer-engagement/developer/dependency-tracking-solution-components)が存在することがあります。ソリューションを削除する前に削除する必要があります。

### <a name="steps"></a>手順
1. [PowerApps 管理ポータル](https://admin.powerapps.com)にログインします。

2. 環境を選択します。

3. **Dynamics 365 Administration Center** をクリックします 

    ![Dynamics 365 管理センター](media/overview-model-driven-samples/admin-center.png)

4. 一覧からデータベースを選択し、**開く** をクリックします。

    ![データベースの選択](media/overview-model-driven-samples/select-database.png)

5. **設定/ソリューション** に移動します。

6. 削除するアプリのソリューションを選択し、**削除** をクリックします。

    ![ソリューションの削除](media/overview-model-driven-samples/delete-solution.png)

*または、作成者ポータルで**詳細設定**をクリックすることで、ソリューションの一覧に移動し、URL の .dynamics.com/ より後の部分をすべて削除します*

> [!IMPORTANT]
> 影響を認識している場合以外は他のシステム ソリューションを削除しないでください。

## <a name="install-or-uninstall-sample-data"></a>サンプル データのインストールまたはアンインストール
1. 手順 1 ～ 4 に従います。
2. **設定/データ管理/サンプル データ** に移動します。
3. サンプル データがインストールされている場合、削除するオプションを使用できます。 それ以外の場合、インストールするオプションを使用できます。 

    ![サンプル データの削除](media/overview-model-driven-samples/remove-sample-data.png)




