---
title: Web リソースの使用 | Microsoft Docs
description: 開発者がモデル駆動型アプリ内で Web リソースを使用する方法について説明します。
services: ''
suite: powerapps
documentationcenter: na
author: JimDaly
manager: kvivek
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/31/2018
ms.author: jdaly
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---

# <a name="use-web-resources"></a>Web リソースの使用

各アプリ用 Common Data Service インスタンス内には `webresources` と呼ばれる仮想フォルダーがあり、ここでは、名前で HTML、JS、CSS、イメージ、および他ファイルを要求し、ブラウザーでアクセスできます。 これらのファイルは、アプリケーションを使用してをアップロードしたり、または [WebResource エンティティ](../common-data-service/reference/entities/webresource.md) レコードとしてプログラムによって追加できます。 [XrmToolBox WebResources マネージャ](https://www.xrmtoolbox.com/plugins/MsCrmTools.WebResourcesManager/) は、これらのレコードの使用を容易にできるコミュニティ ツールです。

これらのレコードは、コンテンツの相対パス名を使用して相互に表示できます。 ファイルをアップロードして名前で要求するこの機能は、ブラウザーの認証セッション内で処理されているファイルを使用して Web アプリケーションを作成するのに必要なすべての構成要素を提供します。 AJAX テクノロジによるクライアント側のコードを使用して、ブラウザー ウィンドウまたはフォームまたはダッシュボードの IFrame 内で実行できる豊富なアプリケーションを作成できます。 

最も一般的には、フォームとコマンドにイベント ハンドラー関数を追加する JavaScript Webリソースを使用します。

詳細:
- [モデル駆動型アプリによるクライアント スクリプト](client-scripting.md)
- [Web リソース](/dynamics365/customer-engagement/developer/web-resources)
