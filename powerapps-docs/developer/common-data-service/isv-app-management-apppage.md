---
title: ISV Studioのアプリケーション ページ | Microsoft Docs
description: ISV Studioポータルが提供するアプリケーション ページの機能について説明します。
services: ''
suite: powerapps
documentationcenter: na
author: phecke
manager: kvivek
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: article
ms.reviewer: pehecke
ms.workload: na
ms.date: 07/11/2019
ms.author: prkoduku
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---

# <a name="the-app-page"></a>アプリケーション ページ

[!INCLUDE [cc-beta-prerelease-disclaimer](../../includes/cc-beta-prerelease-disclaimer.md)]

ユーザがアプリを選択すると、アプリの詳細ページに遷移し、特定のアプリでの複数のテナントを横断したインストール履歴を分析するビューが表示されます。 アプリに関する説明は [AppSource](https://appsource.microsoft.com/)を参照してください。

![アプリケーションの詳細ページ](media/isv-portal-apppage-appname.png)

アプリケーションの詳細ページには、以下のグラフとメトリックが表示されます。

## <a name="successful-package-installs-by-environment-type"></a>環境の種類に応じたパッケージのインストール

以下の円グラフは、インストール ベース全体における、選択されたアプリケーションの実稼働パッケージとサンドボックス パッケージのインストール比率を示しています。

グラフにカーソルを合わせると、以下の情報が表示されます:

1. 組織の種類 – 軸稼働環境、またはサンドボックス環境
2. 組織の種類に対するパッケージのインストール数

![環境の種類に応じたパッケージのインストール](media/isv-portal-apppage-graph1.png)

## <a name="package-install-attempts-by-tenant-last-28-days"></a>テナント別パッケージのインストール試行回数 (過去28日間)

以下の棒グラフは、過去28日間にテナントが選択したアプリケーションのパッケージのインストールに成功した数と失敗した数を示しています。

グラフ上のいずれかの部分にカーソルを合わせると、以下の情報が表示されます:

1. テナント名称とテナント ID
2. テナントにおけるパッケージのインストール状況 (成功件数と失敗件数)
3. テナントへのパッケージのインストール試行回数

![テナント別パッケージのインストール試行回数 (過去28日間)](media/isv-portal-apppage-graph2.png)

## <a name="successful-package-installs-by-location-of-tenants"></a>テナントの場所別のパッケージのインストールの成功数

以下の地図は、アプリのテナント別の地理的分布を示しています。

地図上のいずれかの領域にカーソルを合わせると、次の情報が表示されます:

1. 場所
2. 選択した場所のパッケージ インストール数

![テナントの場所別のパッケージのインストール数](media/isv-portal-apppage-graph3.png)

## <a name="successful-package-and-version-installs-by-tenant"></a>テナントによるパッケージおよびバージョンのインストールの成功

以下の棒グラフでは、パッケージ固有の名前を表示しており、ドロップダウン メニューで選択したアプリのバージョンが表示されます。 既定ではすべてのパッケージが選択され、インストールされているすべてのパッケージのすべてのバージョン (テナントごと) がグラフに表示されます。 1つまたは複数のパッケージおよびバージョンを選択して、さらなるスライシングとダイシングをすることができます。 パッケージを選択すると、 バージョンのドロップダウンが更新され、選択したパッケージに対応したバージョンが表示されます。

グラフ上のいずれかの部分にカーソルを合わせると、以下の情報が表示されます:

1. テナント名称とテナント ID
2. パッケージのバージョン
3. 選択したテナント内のバージョンのパッケージのインストール数


![テナントごとのパッケージとバージョンのインストール](media/isv-portal-apppage-graph4.png)

### <a name="see-also"></a>関連項目

[Power Platform ISV Studioの概要](isv-app-management.md)  
[ホーム ページ](isv-app-management-homepage.md)  
[テナント ページ](isv-app-management-tenantpage.md)
