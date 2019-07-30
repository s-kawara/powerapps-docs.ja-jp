---
title: モデル駆動型アプリでレコードを検索する |MicrosoftDocs
ms.custom: ''
author: mduelae
manager: kvivek
ms.service: powerapps
ms.component: pa-user
ms.topic: conceptual
ms.date: 11/16/2018
ms.author: mduelae
ms.reviewer: ''
ms.assetid: ''
search.audienceType:
- enduser
search.app:
- PowerApps
- D365CE
ms.openlocfilehash: 35cd4e4f0393f28d6cca5a2bd67497018a12ae26
ms.sourcegitcommit: 483c777a1537ccab6a2a2da6a5d1fe4470dd0e7e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2019
ms.locfileid: "61559359"
---
# <a name="search-for-records-in-an-app"></a>アプリでレコードを検索する

複数のエンティティでレコードを検索するには、関連検索またはモデル駆動型アプリでのカテゴリ別検索を使用します。 関連性検索では、複数のエンティティにわたる高速で包括的な結果を1つのリストにして、関連性によって並べ替えます。 分類された検索は、アカウント、連絡先、潜在顧客などのエンティティの種類別にグループ化された検索結果を返します。

通常、分類された検索は、既定の検索オプションです。 ただし、関連性検索が組織によって有効になっている場合は、既定の検索エクスペリエンスになります。   
  
### <a name="normal-quick-find-categorized-search"></a>通常のクイック検索 (分類された検索) 
  
- 次**のもので始まる**:結果には、特定の単語で始まるレコードが含まれます。 たとえば、"Alpine Ski House" を検索する場合は、検索ボックスに「 **alp** 」と入力します。「 **ski**」と入力した場合、レコードは表示されません。  
  
- **ワイルドカード**:たとえば、* ski または * ski のようになります。\*  
  
### <a name="relevance-search"></a>関連性の検索
  
- **検索範囲**:結果には、検索語句内のすべての単語を含むフィールドを含むレコードが含まれます。  個々の単語は、文字列内の任意の順序で任意の場所に記述できます。  たとえば、"Alpine Ski House" を検索すると、すべての検索語が文字列のどこかに出現するので、「今日の家を Meadows に移動します」という結果を見つけることができます。  

## <a name="switch-between-relevance-and-categorized-search"></a>関連性と分類された検索の切り替え

組織で両方の検索オプション (関連性と分類された検索) をオンにしている場合は、2つを切り替えることができます。

1. 検索の種類を切り替えるには、ナビゲーションバーで **[検索]** ボタンを選択します。

2. 左側のドロップダウンメニューを選択して、関連性のある**検索**または**分類**された検索を切り替えます。

## <a name="start-a-search"></a>検索を開始する  
  
1.  上部のナビゲーションバーで、 **[検索]** を選択します。  
  
2.  検索ボックスに検索語句を入力し、 **[検索]** を選択します。  
  
## <a name="filter-search-results"></a>検索結果のフィルター処理  
  
-   1つのレコードの種類で結果をフィルター処理するには、[検索] 画面で、[**フィルター**条件] ボックスの一覧からレコードの種類を選択します。  
  
-   すべてのレコードの種類を検索するには、 **[フィルター条件]** ドロップダウンボックスで **[なし]** を選択します。  
  
 
