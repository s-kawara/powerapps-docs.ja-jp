---
title: PowerAppsを使用したフィードバックのエンティティの構成 | MicrosoftDocs
description: エンティティのフィードバックを有効にする方法を説明する
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
search.audienceType:
  - maker
search.app:
  - PowerApps
  - D365CE
---
# <a name="configure-an-entity-for-feedbackratings"></a>フィードバック/評価のためにエンティティを構成する

エンティティをフィードバックに対して有効化することによって、顧客や従業員が、エンティティ レコードに関するフィードバックを記述したり、定義された評価の範囲内でエンティティ レコードを評価できるようにします。  

この機能は一般的に、ポータルや調査を通じて顧客からデータを取得するシステムで使用されます。 サービスまたは製品の満足度に対するデータを、そのような種類のデータを表すエンティティに適用できます。

フィードバックは、従業員が共同作業のフィードバックを提供するために使用することもできます。

> [!NOTE]
> 次の手順を実行するために、システム管理者またはシステム カスタマイザーのセキュリティ ロール、または同等のアクセス許可が必要になります。
  
## <a name="enable-feedback"></a>フィードバックの有効化  
  
エンティティを編集して**フィードバック**を有効にします。 詳細: [エンティティの編集](edit-entities.md)
  
## <a name="add-a-subgrid-for-feedback-on-the-entity-form"></a>フィードバック用のサブグリッドをエンティティ フォームに追加  

既定では、ユーザーは、フィードバックを追加するレコードの関連レコードの一覧に移動する必要があります。 ユーザーが簡単にフィードバックを追加できるようにするために、フィードバックを有効にする対象のエンティティのフォームにフィードバックのサブグリッドを追加することができます。  

<!-- This is the closest I could find to a topic about adding an subgrid to a form. --> 詳細:  [サブグリッド プロパティの概要](../model-driven-apps/sub-grid-properties-legacy.md)

## <a name="add-a-rollup-field--to-the-entity-form-to-show-the-ratings"></a>評価を表示するためにエンティティ フォームにロールアップ フィールドを追加  

エンティティの評価の計算方法に基づいて、評価を計算するロールアップ フィールドを作成し、フィードバックに対して有効にするエンティティのフォームに追加します。 詳細: [値を集約するロールアップ フィールドを定義](define-rollup-fields.md)
  
### <a name="see-also"></a>関連項目  
 [Dynamics 365 のレコードに対してフィードバックまたは評価を送信する](/dynamics365/customer-engagement/basics/submit-feedback-ratings)
