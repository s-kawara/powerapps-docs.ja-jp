---
title: モデル駆動型アプリでクライアント スクリプトを使用する | Microsoft Docs
description: 開発者がクライアント側スクリプトとモデル駆動型アプリで JavaScript を利用する方法について説明します。
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
ms.date: 03/13/2018
ms.author: jdaly
search.audienceType:
- developer
search.app:
- PowerApps
- D365CE
ms.openlocfilehash: 38a1a5371cbaf5d10c59a291127c13a1d00a3056
ms.sourcegitcommit: 429b83aaa5a91d5868e1fbc169bed1bac0c709ea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/24/2018
ms.locfileid: "42829401"
---
# <a name="client-scripting-with-model-driven-apps"></a>モデル駆動型アプリでのクライアント スクリプト

JavaScript を使用したクライアント側スクリプトは、モデル駆動型アプリのフォームにデータを表示するためにカスタムの業務プロセス ロジックを適用する方法の 1 つですが、最優先する方法ではありません。 *業務ルール*を利用すると、JavaScript の知識がなく、開発者でない人でも、業務プロセス ロジックをフォームに適用することができます。 詳細情報: [Dynamics 365 Customer Engagement カスタマイズ ガイド: フォームにロジックを適用するために業務ルールおよびビジネス レコメンデーションを作成する](/dynamics365/customer-engagement/customize/create-business-rules-recommendations-apply-logic-form)

> [!TIP]
> [powerapps.com](http://web.powerapps.com?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc) の **Common Data Service** 領域内に業務ルール デザイナーがあります。 エンティティを確認するには、**[業務ルール]** タブを探します。

業務ルールを使用して業務の要件を達成できない場合は、クライアント API オブジェクト モデルを使用したクライアント スクリプトをお勧めします。この方法でアプリケーションの動作を拡張し、クライアントの自動化を実現できます。

## <a name="resources"></a>リソース

クライアント スクリプトに関する以下のリソースは、Dynamics 365 Customer Engagement の開発者ドキュメントで参照できます。

- [JavaScript を使用したクライアント スクリプト](/dynamics365/customer-engagement/developer/clientapi/client-scripting)
- [フォームおよびグリッドのイベント](/dynamics365/customer-engagement/developer/clientapi/events-forms-grids)
- [クライアント API オブジェクト モデルについて](/dynamics365/customer-engagement/developer/clientapi/understand-clientapi-object-model)
- [チュートリアル: 最初のクライアント スクリプトを記述する](/dynamics365/customer-engagement/developer/clientapi/walkthrough-write-your-first-client-script)
- [JavaScript コードのデバッグ](/dynamics365/customer-engagement/developer/clientapi/debug-javascript-code)
- [ベストプラクティス: クライアント スクリプト](/dynamics365/customer-engagement/developer/clientapi/client-scripting-best-practices)
- [クライアント API 参照](/dynamics365/customer-engagement/developer/clientapi/reference)

