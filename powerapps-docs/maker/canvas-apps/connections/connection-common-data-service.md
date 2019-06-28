---
title: Common Data Service への接続 |Microsoft Docs
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
# <a name="connect-to-common-data-service"></a>Common Data Service への接続します。

安全に Common Data Service にビジネス データを格納し、ユーザーがそのデータを管理できるように、PowerApps の機能豊富なアプリをビルドできます。 Microsoft Flow、Power BI、および Dynamics 365 からデータを含むソリューションに、そのデータを統合することもできます。

既定では、Common Data Service のコネクタは、アプリの現在の環境でのデータに接続します。 アプリは、別の環境に移動した場合、コネクタは、新しい環境でのデータに接続します。 この動作では、1 つの環境または開発から運用環境にテストする移動の ALM プロセスに従ってアプリを使用してアプリに適しています。

Common Data Service コネクタの使用のデータ ソースを追加すると、環境を変更し、し、1 つまたは複数のエンティティを選択できます。 既定では、アプリは現在の環境でのデータに接続し、UI は **(現在)** エンティティの一覧を列挙します。

> [!div class="mx-imgBorder"]
> ![既定の環境](media/connection-common-data-service/common-data-service-connection-change-environment.png)

選択した場合**変更**、または指定できます、別の環境データをプルからの代わりに、現在の環境だけでなく。

> [!div class="mx-imgBorder"]
> ![その他の環境](media/connection-common-data-service/common-data-service-connection-select-environment.png)

検索ボックスの下に、選択した環境の名前が表示されます。

> [!div class="mx-imgBorder"]
> ![新しい環境](media/connection-common-data-service/common-data-service-connection-after-change-environment.png)

Common Data Service コネクタは、Dynamics 365 コネクタと同等の機能が近づいているよりも堅牢です。

詳細情報:[Common Data Service とは](../../common-data-service/data-platform-intro.md)
