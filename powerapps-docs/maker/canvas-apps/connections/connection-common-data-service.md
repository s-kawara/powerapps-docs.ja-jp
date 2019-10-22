---
title: Common Data Service | に接続します。Microsoft Docs
description: Common Data Service に接続して、PowerApps でアプリを構築するために使用する方法について説明します。
author: tapanm-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: ''
ms.date: 04/22/2019
ms.author: tapanm
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: fcadc4d214494380f50f712e453554d41d08eabe
ms.sourcegitcommit: 7dae19a44247ef6aad4c718fdc7c68d298b0a1f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2019
ms.locfileid: "71994002"
---
# <a name="connect-to-common-data-service"></a>Common Data Service への接続

ユーザーがデータを管理できるように、Common Data Service にビジネスデータを安全に格納したり、PowerApps でリッチなアプリを構築したりすることができます。 また、Dynamics 365 の Microsoft Flow、Power BI、データを含むソリューションにそのデータを統合することもできます。

既定では、Common Data Service コネクタは、アプリの現在の環境のデータに接続します。 アプリが別の環境に移動した場合、コネクタは新しい環境のデータに接続します。 この動作は、1つの環境を使用するアプリ、または開発からテスト環境への移行のために ALM プロセスに従うアプリに適しています。

Common Data Service コネクタを使用してデータソースを追加する場合は、環境を変更してから1つまたは複数のエンティティを選択することができます。 既定では、アプリは現在の環境のデータに接続し、UI はエンティティの一覧に対して **(現在)** を表示します。

> [!div class="mx-imgBorder"]
> ![Default 環境 @ no__t-1

**[変更]** を選択した場合は、現在の環境に加えて、または現在の環境の代わりに、別の環境を使用してデータをプルするように指定できます。

> [!div class="mx-imgBorder"]
> ![Other environment @ no__t-1

検索ボックスの下に、選択した環境の名前が表示されます。

> [!div class="mx-imgBorder"]
> ![New environment @ no__t-1

Common Data Service コネクタは、Dynamics 365 コネクタより堅牢で、機能のパリティに近づいています。

詳細情報:[Common Data Service とは](../../common-data-service/data-platform-intro.md)
