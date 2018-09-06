---
title: Web リソースの使用 | Microsoft Docs
description: 開発者がモデル駆動型アプリ内の Web リソースをどのように使用するかについて説明します。
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
search.audienceType:
- developer
search.app:
- PowerApps
- D365CE
ms.openlocfilehash: 88e51e4547732bed2d3e7ef3290bc8d933afded3
ms.sourcegitcommit: 429b83aaa5a91d5868e1fbc169bed1bac0c709ea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/24/2018
ms.locfileid: "42849913"
---
# <a name="use-web-resources"></a>Web リソースの使用

各 Common Data Service for Apps インスタンスには、`webresources` と呼ばれる仮想フォルダーがあります。ここに名前で、HTML、JS、CSS、画像、およびその他のファイルを要求して、ブラウザーでアクセスできます。 これらのファイルはアプリケーションを使用してアップロードしたり、プログラムから [WebResource エンティティ](../common-data-service/reference/entities/webresource.md) レコードとして追加することができます。 [XrmToolBox WebResources Manager](https://www.xrmtoolbox.com/plugins/MsCrmTools.WebResourcesManager/) は、これらのレコードの操作を容易にするコミュニティ ツールです。

これらのレコードでは、そのコンテンツの相対パス名を使用して、相互参照できます。 ファイルをアップロードし、名前で要求できるこの機能は、ブラウザーの認証されたセッション内で処理されるファイルを使用した Web アプリケーションを作成するために必要なビルディング ブロックをすべて提供します。 AJAX の手法でクライアント側コードのみを使用して、ブラウザー ウィンドウ内またはフォームまたはダッシュボードの IFrame 内で実行できる豊かなアプリケーションを作成できます。 

一般に、フォームやコマンドには、JavaScript Web リソースを使用して、イベント ハンドラー機能を追加します。

詳細情報:
- [モデル駆動型アプリでのクライアント スクリプト](client-scripting.md)
- [Dynamics 365 Customer Engagement の開発者ガイド: Web リソース](/dynamics365/customer-engagement/developer/web-resources)
