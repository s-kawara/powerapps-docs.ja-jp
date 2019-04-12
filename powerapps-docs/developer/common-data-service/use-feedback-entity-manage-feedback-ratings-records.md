---
title: フィードバック エンティティを使用してレコードのフィードバックと評価を管理する (Common Data Service) | Microsoft Docs
description: レコードのフィードバックと評価を取得するためのフィードバック エンティティについて説明します。
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: JimDaly
ms.author: jdaly
manager: ryjones
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="use-the-feedback-entity-to-manage-feedback-and-ratings-for-records"></a>フィードバック エンティティを使用してレコードのフィードバックと評価を管理する

Common Data Serviceでユーザーがエンティティ レコードのフィードバックと評価を提供できるようにすることで製品やサービスを向上します。 例えば、`Product` エンティティのフィードバックと評価を有効にして、販売する製品に関するユーザーのフィードバックがわかるようにしたり、または顧客サポート チームの質を理解して向上させるために、`Incident`(サポート案件 )エンティティに関するユーザーのフィードバックがわかるようにします。  
  
 Common Data Service のシステム エンティティとユーザー定義エンティティの両方について、フィードバックと評価を有効にできます。 既定では、`KnowledgeArticle` エンティティがフィードバックと評価に対して有効になります。 新しい `Feedback` エンティティを使用して、エンティティ レコードのフィードバックをプログラムにより作成して管理します。  
  
 プログラムにより次のフィードバックを有効にするには:  
  
- システム エンティティ、<xref:Microsoft.Xrm.Sdk.Messages.UpdateEntityRequest> メッセージを使用してエンティティ更新し、<xref:Microsoft.Xrm.Sdk.Messages.UpdateEntityRequest.HasFeedback> プロパティを true に設定します。  
  
- ユーザー定義エンティティ、エンティティの作成中に <xref:Microsoft.Xrm.Sdk.Messages.CreateEntityRequest>.<xref:Microsoft.Xrm.Sdk.Messages.CreateEntityRequest.HasFeedback>  プロパティを true に設定、または既存のユーザー定義エンティティを更新するために<xref:Microsoft.Xrm.Sdk.Messages.UpdateEntityRequest>.<xref:Microsoft.Xrm.Sdk.Messages.UpdateEntityRequest.HasFeedback> プロパティを true に設定します。  
  
  フィードバックと評価のエンティティを有効にする場合、それを無効にすることはできません。 エンティティをフィードバックに対して有効にすると、そのエンティティと `Feedback` エンティティの間に関連の関係性が作成されます。  
  
> [!NOTE]
>  また、システム エンティティやユーザー定義エンティティのフィードバックと評価を有効にするために Common Data Service のカスタマイズ ツールも使用できます。 詳細: [エンティティをフィードバックに対して有効化](http://go.microsoft.com/fwlink/p/?LinkId=785436)  
  
 `Feedback` エンティティは、以下の情報を格納します:  
  
- フィードバックのタイトル  
  
- フィードバックのコメント  
  
- フィードバックの評価。 また、評価の最小および最大(数)値を指定することによって評価の範囲も定義できます。 たとえば、1-5 のスケールで 4 の評価。  
  
- 最小および最大の評価値に基づいて 0 ~ 1 の値のサイズになっている指定されたユーザーの評価を示すために自動的に計算されたフィードバックの正規化された評価。  
  
  > [!NOTE]
  >  正規化された評価が、正規化、または異なる期間の評価 (評価の最小値および最大値) に対して指定された評価値の一定化を助けます。 正規化された評価は次のようにして計算されます: (評価 - 最小評価) / (最大評価  - 最小評価)。  
  >   
  >  また、レコードに対する評価は、レコードに対する正規化された評価すべての平均として計算されます。  
  
- オープンまたはクローズなどフィードバックの状態  
  
- フィードバックが送信された場所からソースを表示するためのフィードバック ソース。 フィードバックが Common Data Service 内で作成された場合、その値は **Internal** に設定されます。 開発者は、フィードバックを提供するために使用されるアプリケーションに応じて選択の値を追加できます。  
  
- フィードバック レコードを作成または最後に修正したユーザー  
  
- フィードバックが関連付けられているエンティティレコード  
  