---
title: ISV Studio のホームページ | Microsoft Docs
description: ISV Studioポータルが提供するホームページの機能について説明します。
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

# <a name="the-home-page"></a>ホームページ

[!INCLUDE [cc-beta-prerelease-disclaimer](../../includes/cc-beta-prerelease-disclaimer.md)]

ISV Studioにログインすると、 *ホーム* ページと呼ばれるランディング ページが表示されます。 このページの目的を解説するウェルカム メッセージが表示されます。

ユーザーが複数の発行者に関連付けられている場合は、すべての発行者が表示され、既定で最初の発行者が選択されます。 このページのすべてのメトリックは、選択した発行者に特化したものです。 別の発行者に切り替えることで、その発行者に対応するメトリックを表示することができます。

![ホーム ページ](media/isv-portal-homepage.png)

ホームページのサマリー セクションには、以下のグラフとメトリックが表示されます

## <a name="successful-app-package-installs-by-tenant"></a>テナントによるアプリ パッケージのインストールの成功

最初のグラフでは、公開されたアプリとアプリのパッケージがインストールされているテナントが可視化され、パッケージがインストールされた件数に基づいて降順に表示されます。

グラフのテナント タイルにカーソルを合わせると、以下の情報が表示されます:

1. アプリの名称
2. テナント名称とテナント ID
3. テナント内でのアプリのパッケージインストール数

![テナント別パッケージのインストール](media/isv-portal-homepage-graph1.png)

## <a name="package-install-attempts-by-app-last-28-days"></a>アプリ別パッケージのインストール試行回数 (過去28日間)

この棒グラフでは、公開されたアプリケーションの数と、過去28日間のすべての運用環境でのインストールの成功数と失敗数を視覚化します。

グラフ上のアプリにカーソルを合わせると、以下の情報が表示されます:

1. アプリの名称
2. パッケージのインストール状況 (成功件数と失敗件数)
3. パッケージのインストール試行回数

![アプリ別パッケージのインストール試行回数 (過去28日間)](media/isv-portal-homepage-graph2.png)

## <a name="additional-insights"></a>追加の洞察情報

概要セクションの下では、さらなる洞察情報にアクセスし、認証されたアプリケーションまたはテナントの視点を通してインストールの履歴を深く掘り下げることができます。

**上位の認証アプリ** と  **上位のテナント** は既定でページに表示されます。 **すべてを表示** を選択してすべてのアプリを表示することもできます。

アプリ名称とアイコンは AppSourceに由来します。

![すべてのアプリ](media/isv-portal-homepage-seeall.png)

### <a name="see-also"></a>関連項目

[Power Platform ISV Studioの概要](isv-app-management.md)  
[アプリ ページ](isv-app-management-apppage.md)  
[テナント ページ](isv-app-management-tenantpage.md)
