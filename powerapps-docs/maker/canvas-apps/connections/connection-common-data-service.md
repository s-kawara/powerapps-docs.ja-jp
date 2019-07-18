---
title: Common Data Service に接続 |Microsoft Docs
description: Common Data Service に接続し、PowerApps でアプリを構築するために使用する方法について説明します。
author: aftowen
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: ''
ms.date: 04/22/2019
ms.author: anneta
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: da68abeec51df102647ea32a17b3d76451f2f1aa
ms.sourcegitcommit: 982cab99d84663656a8f73d48c6fae03e7517321
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/28/2019
ms.locfileid: "67456728"
---
# <a name="connect-to-common-data-service"></a>Common Data Service に接続

ビジネスデータを Common Data Service に安全に格納し、PowerApps で豊富なアプリケーションを構築し、ユーザーがそのデータを管理することができます。そのデータを、Microsoft Flow、Power BI、および Dynamics 365 を含むソリューションに統合することができます。

既定では、Common Data Service のコネクタは、アプリの現在の環境のデータに接続します。 アプリが、別の環境に移動した場合、コネクタは、新しい環境のデータに接続します。 この動作は、1 つの環境を利用するアプリケーション、開発からテスト、そして本番へ移行するための ALM プロセスに従うアプリケーションに適しています。

Common Data Service コネクタを使用してデータ ソースを追加すると、環境を変更後、1 つまたは複数のエンティティを選択できます。 既定では、アプリは現在の環境のデータに接続し、UI は エンティティリストの上に **(Current)** と表示します。

> [!div class="mx-imgBorder"]
> ![既定の環境](media/connection-common-data-service/common-data-service-connection-change-environment.png)

**変更** を選択した場合、現在の環境に加えて、他の環境からデータを取得するために別の環境を指定できます。

> [!div class="mx-imgBorder"]
> ![その他の環境](media/connection-common-data-service/common-data-service-connection-select-environment.png)

選択した環境の名前が検索ボックスの下に表示されます。

> [!div class="mx-imgBorder"]
> ![新しい環境](media/connection-common-data-service/common-data-service-connection-after-change-environment.png)

Common Data Service コネクタは、Dynamics 365 コネクタよりも堅牢で、機能も同等です。

詳細情報:[Common Data Service とは](../../common-data-service/data-platform-intro.md)
