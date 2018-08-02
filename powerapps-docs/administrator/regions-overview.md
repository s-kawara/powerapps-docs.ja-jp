---
title: リージョンの概要 | Microsoft Docs
description: PowerApps のリージョンについて説明します
author: manasmams
manager: kvivek
ms.service: powerapps
ms.component: pa-admin
ms.topic: conceptual
ms.date: 03/21/2018
ms.author: manasma
ms.openlocfilehash: 7cf52b8f21c5188b799904175f473210fa1b45b4
ms.sourcegitcommit: 2e7b621066cdc3e7be329d5213ecfee0b4223641
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/30/2018
ms.locfileid: "39348882"
---
# <a name="regions-overview-in-powerapps"></a>PowerApps のリージョン概要
## <a name="how-do-i-find-out-where-my-app-is-deployed"></a>アプリがデプロイされる場所
アプリは、環境をホストするリージョンにデプロイされます。 たとえば、環境がヨーロッパ リージョンで作成された場合、アプリはヨーロッパ データ センターにデプロイされます。

管理者は、PowerApps 管理センターで各環境のリージョンを特定できます。

* [管理センター](https://admin.powerapps.com)にアクセスし、職場アカウントでサインインします。
  
    管理センターでは、**[環境]** タブに既存のすべての環境が一覧表示されます。この一覧には、アプリがデプロイされている**リージョン**が表示されます。
  
   ![[環境] タブ](./media/regions-overview/environment-list.png)

## <a name="what-regions-are-available"></a>利用可能なリージョン
* 米国
* カナダ
* ヨーロッパ
* アジア
* オーストラリア
* インド
* 日本
* イギリス

## <a name="what-features-are-specific-to-a-given-region"></a>リージョン固有の機能
環境は、場合によってそれぞれ異なるリージョンで作成され、その地域にバインドされます。 環境内でアプリを作成すると、アプリはその地域内のデータセンターにのみデプロイされます。 このことは、その環境で作成するすべての項目に当てはまります (Common Data Service 内のデータベース、アプリ、接続、ゲートウェイ、およびカスタム コネクタを含む)。

最適なパフォーマンスを維持するため、ユーザーがヨーロッパにいる場合は、ヨーロッパ リージョン内の環境を使用してください。 ユーザーが米国にいる場合は、米国内の環境を使用してください。

> [!NOTE]
> 現時点では、(Azure AD または Office 365 テナントのホーム リージョンと同じリージョン内にある) 運用環境または試用環境にのみデータベースを作成できます。 Microsoft では、テナントのホームとは異なるリージョンで作成された環境にもデータベースを作成できるように取り組んでいます。 また、現在のところ、既定の環境と (PowerApp Community プランで作成した) 個別環境にデータベースを作成することはできません。

> [!NOTE]
> オンプレミスのデータ ゲートウェイは、インドのリージョンまたはカスタム環境では利用できません。 既定の環境でゲートウェイを作成する必要があります。

