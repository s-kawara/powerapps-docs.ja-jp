---
title: モデル駆動型アプリを使用してコマンドをカスタマイズする |Microsoft Docs
description: モデル駆動型アプリを使用してコマンドをカスタマイズする方法を説明します。
services: ''
suite: powerapps
documentationcenter: na
author: JimDaly
manager: faisalmo
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/17/2018
ms.author: jdaly
ms.openlocfilehash: 7ad955ed5858cab69aaf8b2993ae3f98a04147fb
ms.sourcegitcommit: 59785e9e82da8f5bd459dcb5da3d5c18064b0899
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/22/2018
ms.locfileid: "30024553"
---
# <a name="customize-commands-with-model-driven-apps"></a>モデル駆動型アプリを使用してコマンドをカスタマイズする 

フォームまたはリスト コマンド バー内に表示されるコマンドは、カスタマイズできます。 コマンドは Office リボンで使用されている XML スキーマに基づいているため、*リボン*という用語は引き続き使用します。 コマンドを作成するときには、次の 3 つの要素を定義します。

- *[Display rules]\(ルールを表示する\)* は、フォームまたは一覧が読み込まれ、コマンドまたはグループのコマンドを表示するかどうかを決定するときに評価されます。
- *[ルールを有効にする]* は、現在 UI で選択されている項目など、さまざまな条件に基づいて、コマンドが有効になっているかどうかを制御します。
- 各コマンドの *[アクション]* は、それが選択されたときの動作を指示します。 コマンドでは、URL を開いたり、JavaScript Web リソース内に定義された関数を実行できます。

カスタム コマンドは、任意の既存のコマンドに基づいて配置されます。 *カスタム アクション*は、既存のコマンドのセットに適用する変更を定義して、作成する必要があります。 

コマンド用にはデザイナーは用意されていません。 さいわいにも、ツールはコミュニティで用意しています。 コマンドをカスタマイズするときによく使用するグラフィカル インターフェイスのツールは、[リボン ワークベンチ](http://www.develop1.net/public/rwb/ribbonworkbench.aspx)にあります。

詳細情報: [Dynamics 365 Customer Engagement の開発者ガイド: コマンドおよびリボンをカスタマイズする](/dynamics365/customer-engagement/developer/customize-dev/customize-commands-ribbon)


