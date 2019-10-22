---
title: ISV Studioのテナント ページ | Microsoft Docs
description: ISV Studioポータルが提供するテナント ページの機能について説明します。
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

# <a name="the-tenant-page"></a>テナント ページ

[!INCLUDE [cc-beta-prerelease-disclaimer](../../includes/cc-beta-prerelease-disclaimer.md)]

テナントのインストール履歴を表示するには、ISVはホームページの **上位のテナント** ビューに切り替え、テナントを選択します。

![テナントのインストール履歴](media/isv-portal-homepage-tenantpivot.png)

テナント ページには、以下のグラフとメトリックが表示されます:

![テナント ページ](media/isv-portal-tenantpage.png)

## <a name="successfully-installed-apps"></a>正常にインストールされたアプリ

以下の円グラフでは、選択したテナントのすべての環境における ISV アプリの分布を示しています。

グラフ上のいずれかの項目にカーソルを合わせると、以下の情報が表示されます:

1. アプリ名
2. 選択したテナント内のアプリのインストール数

![正常にインストールされたアプリ](media/isv-portal-tenantpage-graph1.png)

## <a name="successful-production-vs-sandbox-package-installs-by-environment"></a>運用環境とサンドボックス環境別の成功インストール数

以下の棒グラフでは、選択したテナントにおける 運用環境とサンドボックス環境の ISV アプリのインストールを視覚化したものです。 プライバシー上の理由により、この時点では環境名を表示することができません。

グラフ上のいずれかの部分にカーソルを合わせると、以下の情報が表示されます:

1. 環境 ID
2. 環境の種類 (運用環境またはサンドボックス環境)
3. 環境におけるパッケージのインストール数

![環境の種類に応じたパッケージのインストール](media/isv-portal-tenantpage-graph2.png)

## <a name="successful-package-installs-by-environment-location"></a>環境の場所別の成功したパッケージのインストール

以下の地図では、環境の場所別にインストールされたISVパッケージの地理上の分布を示しています。

地図上のいずれかの地域にカーソルを合わせると、以下の情報が表示されます:

1. 場所
2. 選択した場所のパッケージ インストール数

![環境の場所別のパッケージのインストール](media/isv-portal-tenantpage-graph3.png)

## <a name="successful-app-package-and-version-installs-by-environment"></a>環境ごとのアプリケーション パッケージとバージョンの成功したインストール

以下の縦棒グラフには、ドロップダウン メニューにて選択されたアプリ名称、パッケージ固有の名称、選択されたテナントのバージョンを視覚化しています。 すべてのアプリケーションは既定で選択され、ISV は1つ または複数のアプリケーション、パッケージ、バージョンを選択することで、さらに詳細な情報を表示することができます。 アプリを選択すると、 **パッケージ** のドロップダウンリストが更新され、選択したAppに対応したパッケージが表示されます。 パッケージを選択すると、  **バージョン** のドロップダウンが更新され、選択したパッケージに対応したバージョンが表示されます。

グラフ上のいずれかの部分にカーソルを合わせると、以下の情報が表示されます:

1. 環境 ID
2. パッケージのバージョン
3. 環境におけるバージョンのパッケージのインストール数

![環境ごとのパッケージとバージョンのインストール](media/isv-portal-tenantpage-graph4.png)

### <a name="see-also"></a>関連項目

[Power Platform ISV Studioの概要](isv-app-management.md)  
[ホーム ページ](isv-app-management-homepage.md)  
[アプリ ページ](isv-app-management-apppage.md)
