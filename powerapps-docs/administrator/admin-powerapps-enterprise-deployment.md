---
title: PowerApps のエンタープライズ展開の管理 | MicrosoftDocs
description: PowerApps のエンタープライズ展開の管理に関するホワイト ペーパーをご覧ください。
ms.custom: ''
ms.date: 08/09/2018
ms.reviewer: ''
ms.service: crm-online
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: get-started-article
applies_to:
- Dynamics 365 (online)
- Dynamics 365 Version 9.x
ms.assetid: 83200632-a36b-4401-ba41-952e5b43f939
caps.latest.revision: 31
author: jimholtz
ms.author: jimholtz
manager: kvivek
search.audienceType:
- admin
search.app:
- D365CE
- PowerApps
- Powerplatform
ms.openlocfilehash: ce8daad960834c2965e2a5432ccaf2a3f515e503
ms.sourcegitcommit: 429b83aaa5a91d5868e1fbc169bed1bac0c709ea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/24/2018
ms.locfileid: "42857496"
---
# <a name="administering-a-powerapps-enterprise-deployment"></a>PowerApps のエンタープライズ展開を管理する

PowerApps は、Microsoft が提供する生産性の高いアプリケーション開発プラットフォームです。  このプラットフォームは、Microsoft が独自のファースト パーティ アプリケーションである Dynamics 365 for Sales、Service、Field Service、Marketing、および Talent を構築するために使用しています。  つまり、これらのアプリケーションは、そのプラットフォーム上でネイティブに構築されます。   企業のお客様も、同じテクノロジを使用して独自の基幹業務アプリケーションを構築することができます。  さらに、組織内の個々のユーザーおよびチームもノーコードまたはローコードで生産性向上アプリケーションを作成することができます。 

[PowerApps のエンタープライズ展開の管理](https://aka.ms/powerappsadminwhitepaper)に関するダウンロード可能なホワイト ペーパーをご覧ください

このホワイト ペーパーは、PowerApps プラットフォーム上で構築されるアプリケーションの計画、セキュリティ保護、配置、サポートを担当するエンタープライズ アプリケーションの管理者を対象としています。  このホワイト ペーパーの目的は、ご利用の環境内に現在あるもの、アプリケーションの開発および展開を事前に計画する方法、最後に展開を管理するための日常的な管理タスクを処理する方法を理解する助けとなることです。
このホワイト ペーパーでは、主要な概念、プラットフォーム アーキテクチャ、および必要となる意思決定を取り上げています。  展開の成功とプラットフォームを使用するユーザーの高い生産性を保証する、組織にとってのベスト プラクティスを開発できるように、可能な限り協力させていただきます。

PowerApps プラットフォームは、より大きな Microsoft Power プラットフォームの一部です。Microsoft Power プラットフォームには、PowerBI と Microsoft Flow も含まれ、Common Data Service for Apps と Data Connectors の共通のインフラストラクチャが利用されています。 これらの機能は Microsoft Azure クラウド サービス、上で構築され、それらのサービスが活用されます。  PowerApps プラットフォームで構築されるアプリケーションについては、Azure クラウド サービスを含めることで、個人的な生産性アプリケーションから企業のミッション クリティカルな基幹業務アプリケーションにスケーリングすることができます。

![Microsoft Power プラットフォーム](media/ms-power-platform.png "Microsoft Power プラットフォーム")
