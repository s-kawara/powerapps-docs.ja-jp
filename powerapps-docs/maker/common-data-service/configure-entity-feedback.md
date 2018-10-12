---
title: PowerApps でフィードバックするためのエンティティの構成 | MicrosoftDocs
description: エンティティでフィードバックを有効にする方法を学習します。
ms.custom: ''
ms.date: 05/18/2018
ms.reviewer: ''
ms.service: crm-online
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Dynamics 365 (online)
- Dynamics 365 Version 9.x
- powerapps
author: Mattp123
ms.assetid: 5b25cf09-d43b-4165-9eaa-7549f4855e7c
caps.latest.revision: 13
ms.author: matp
manager: kvivek
ms.openlocfilehash: efb1cf167353d5928564b42aeb7a49f43cf272d6
ms.sourcegitcommit: aba996b1773ecdf62758e06b34eaf57bede29e08
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/08/2018
ms.locfileid: "39692885"
---
# <a name="configure-an-entity-for-feedbackratings"></a>エンティティをフィードバックおよび評価用に構成する

エンティティでフィードバックを有効にすると、お客様や従業員が任意のエンティティ レコードのフィードバックを記述したり、定義された評価範囲内でエンティティ レコードを評価できるようになります。  

この機能は、ポータルまたは調査でお客様からデータを取得するシステムで通常使用されます。 サービスや製品の満足度の種類のデータに、それらのデータを表すエンティティを適用できます。

フィードバックは、従業員の共同作業のフィードバックに使用することも可能です。

> [!NOTE]
> これらの手順を実行するには、システム管理者またはシステム カスタマイザーのセキュリティ ロールまたはそれと同等のアクセス許可が必要です。
  
## <a name="enable-feedback"></a>フィードバックを有効にする  
  
エンティティを編集して**フィードバック**を有効にします。 詳細情報: [Edit an entity](edit-entities.md) (エンティティを編集する)
  
## <a name="add-a-subgrid-for-feedback-on-the-entity-form"></a>エンティティ フォームにフィードバック用のサブグリッドを追加する  

ユーザーは既定で、フィードバックを追加するレコードの関連レコード一覧に移動する必要があります。 ユーザーが簡単にフィードバックを追加できるようにするには、フィードバックを有効にするエンティティのフォームにフィードバック サブグリッドを追加します。  

<!-- This is the closest I could find to a topic about adding an subgrid to a form. --> 詳細情報: [Sub-Grid properties overview](../model-driven-apps/sub-grid-properties-legacy.md) (サブグリッド プロパティの概要)

## <a name="add-a-rollup-field--to-the-entity-form-to-show-the-ratings"></a>エンティティ フォームに評価を表示するロールアップ フィールドを追加する  

エンティティの評価の計算をどのように行うかにより、評価を計算するロールアップ フィールドを作成し、フィードバックを有効にするエンティティのフォームに追加することができます。 詳細情報: [Define rollup fields that aggregate values](define-rollup-fields.md) (値を集計するロールアップ フィールドを定義する)
  
### <a name="see-also"></a>関連項目  
 [Dynamics 365 レコードのフィードバックまたは評価を送信する](/dynamics365/customer-engagement/basics/submit-feedback-ratings)
