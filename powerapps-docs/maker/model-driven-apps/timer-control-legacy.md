---
title: PowerApps におけるモデル駆動型アプリのタイマー コントロール | MicrosoftDocs
description: タイマー コントロールの使用方法について
ms.custom: ''
ms.date: 06/06/2018
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
ms.assetid: b2b64771-083b-42f9-a3d5-2218f9d8a713
caps.latest.revision: 63
ms.author: matp
manager: kvivek
search.audienceType:
  - maker
search.app:
  - PowerApps
  - D365CE
---
# <a name="model-driven-app-timer-control-overview"></a>モデル駆動型アプリのタイマー コントロールの概要

 レコードが特定の時間ベースのマイルス トーンを満たすために必要があるフォームでタイマー コントロールを使用します。 タイマー コントロールは、アクティブなレコードを解決するアクションにどのくらいの時間が利用可能か、アクションを完了するのにどのくらいの時間が経過したかを示します。 最低限、アクションの完了が成功または失敗したかを表示するようにタイマー コントロールを構成しなければなりません。 さらに、条件が失敗に近づいているときに警告を表示するように構成できます。  
  
 タイマー コントロールは、任意のエンティティのフォームに追加できますが、サービス レベル アグリーメントを追跡するフィールドにリンクされている場合は特に、サポート案件エンティティに使用されます。 フォームの本文に複数のタイマー コントロールを追加できます。 ヘッダーまたはフッターに追加することはできません。  
  
 タイマー コントロールの**データ ソース**プロパティは、エンティティのフィールドを使用します。  
  
-   **失敗時間フィールド**は、日付と時刻のフィールドを使用して時間を設定します。  
  
-   3 つの条件フィールドは、エンティティの**オプション セット**、  **2 つのオプション**、**状態**、または**ステータス**フィールドのいずれかを使用します。  

タイマー コントロールを作成するには、フォーム デザイナーで **挿入** タブを選択し、ツール バーで **タイマー** を選択します。 

  > [!div class="mx-imgBorder"] 
  > ![タイマー コントロールを挿入する](media/insert-timer-control.png)

タイマー コントロールのプロパティ ページで、目的のプロパティを入力するか選択し、**OK** を選択します。 

  
<a name="BKMK_TimerControlProperties"></a>   

## <a name="timer-control-properties"></a>タイマー コントロールのプロパティ  
 次の表に、タイマー コントロールのプロパティを説明します。  
  
|グループ|名前|内容|  
|-----------|----------|-----------------|  
|名前|名前|**必須**。 コントロールの一意の名前。|  
||ラベル|**必須**。 タイマー コントロールに対して表示するラベル。|  
|データ ソース|失敗時間フィールド|**必須**。 エンティティの日付と時刻のフィールドのいずれかを選択して、マイルス トーンを正常に完了する時を表します。|  
||成功条件|**必須**。 エンティティのフィールドを選択して、マイルス トーンの成果を評価し、成功を示すオプションを選択します。|  
||警告条件|エンティティのフィールドを選択して、マイルス トーンの成功が危険な状態にあるかを評価して、警告を表示し、警告を表示することを示すオプションを選択します。|  
||取り消し条件|エンティティのフィールドを選択して、マイルス トーンの達成をキャンセルする必要があるかどうかを評価し、マイルス トーンがキャンセルされたことを示すオプションを選択します。|  

## <a name="next-steps"></a>次のステップ

[フォーム エディターのユーザー インターフェイスの概要](form-editor-user-interface-legacy.md)