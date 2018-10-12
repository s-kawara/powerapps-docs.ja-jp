---
title: PowerApps でモデル駆動型アプリのフォーム エディターを開く |MicrosoftDocs
ms.custom: ''
ms.date: 06/27/2018
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
ms.assetid: 8478a07a-c697-4784-874b-36958eb4f95d
caps.latest.revision: 63
ms.author: matp
manager: kvivek
ms.openlocfilehash: e0fe15df88fccbaee3c13a344416a434e1f92923
ms.sourcegitcommit: aba996b1773ecdf62758e06b34eaf57bede29e08
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/08/2018
ms.locfileid: "39691142"
---
# <a name="open-the-model-driven-app-form-editor"></a>モデル駆動型アプリのフォーム エディターを開く 
フォーム エディターは、セクション、タブ、フィールド、およびコントロールなどのコンポーネントをフォーム エディター キャンバス上にドロップして、フォームを設計する場所です。 このトピックでは、フォーム エディターにアクセスするいくつかの異なる方法について説明します。
 
たとえば、Web リソースについて、フォームの編集時に新しいソリューション コンポーネントを作成する場合、コンポーネントの名前では既定のソリューションのソリューション発行者のカスタマイズ接頭辞が使用され、既定のソリューションにはこれらのコンポーネントのみが含まれます。 特定のアンマネージド ソリューションに新しいソリューション コンポーネントを含める場合は、そのアンマネージド ソリューションを介してフォーム エディターを開く必要があります。  

## <a name="access-the-form-editor-from-the-powerapps-site"></a>PowerApps サイトからフォーム エディターにアクセスする

1. [PowerApps](https://web.powerapps.com/) にサインインします。 

2. **[モデル駆動型]** > **[データ]** > **[エンティティ]** の順に選択します。次に、アカウント エンティティなど、目的のエンティティを選びます。 

3. **[フォーム]** タブを選択し、**[アカウント]** メイン フォームなど、目的のフォームを開きます。

## <a name="access-the-form-editor-from-solution-explorer"></a>ソリューション エクスプローラーからフォーム エディターにアクセスする
  
1.  [ソリューション エクスプローラー](advanced-navigation.md#solution-explorer)を開きます。
  
2.  **[コンポーネント]** の下にある **[エンティティ]** を展開します。次に、目的のエンティティを展開して、**[フォーム]** をクリックします。  
  
3.  フォームのリストで、編集するフォームをクリックします。  
  

## <a name="access-the-form-editor-through-the-command-bar-within-a-model-driven-app"></a>モデル駆動型アプリ内のコマンド バーからフォーム エディターにアクセスする 
  
1.  レコードを開きます。  
  
2.  エンティティに対して複数のメイン フォームがある場合は、フォームが編集対象であることを確認します。 対象でない場合は、フォーム セレクターを使用して編集対象のフォームを選択します。  
  
3.  **[その他のコマンド]** ボタン ![予定アクティビティの [その他のコマンド] ボタン](media/more-commands.gif "予定アクティビティの [その他のコマンド] ボタン") を選択します。  
  
4.  **[フォーム エディター]** を選択します。  

## <a name="access-the-form-editor-from-within-dynamics-365-customer-engagement"></a>Dynamics 365 Customer Engagement 内からフォーム エディターにアクセスする
  
 Dynamics 365 Customer Engagement で、エンティティに応じて、コマンド バーまたはリボンを使用してフォーム エディターにアクセスすることができます。 これらの両方の方法では、既定のソリューションのコンテキストでフォームが開かれます。 

## <a name="access-the-form-editor-for-an-unmanaged-solution"></a>アンマネージド ソリューションのフォーム エディターにアクセスする  
  
1.  [ソリューション](advanced-navigation.md#solutions)を開きます。  
  
2.  使用するアンマネージ ソリューションをダブルクリックします。  
  
3.  フォームを編集するエンティティを検索します。 そこにエンティティがない場合は、追加する必要があります。 詳細情報: [エンティティをアンマネージド ソリューションに追加する](#add-an-entity-to-an-unmanaged-solution) 
  
### <a name="add-an-entity-to-an-unmanaged-solution"></a>エンティティをアンマネージド ソリューションに追加する  
  
1.  **[エンティティ]** ノードを選択し、リストの上にあるツールバーで、**[既存を追加]** をクリックします。  
  
2.  **[ソリューション コンポーネントの選択]** ダイアログ ボックスで、**[コンポーネントの種類]** セレクターを **[エンティティ]** に設定し、追加するエンティティを選択して **[OK]** をクリックします。  
  
3.  **[不足している必須コンポーネント]** ダイアログ ボックスが表示されたときに、このアンマネージド ソリューションを別の環境にエクスポートする予定がない場合は、**[いいえ、必須コンポーネントを含めません]** をクリックすることができます。 この時点で不足している必須コンポーネントを含めないことにした場合は、後で追加できます。 このソリューションを後でエクスポートすると、再び通知が表示されます。  
  
5.  ソリューション エクスプローラーで、編集するフォームを含むエンティティを展開して、**[フォーム]** を選択します。  
  
6.  フォームのリストで、編集するフォームをダブルクリックします。  

## <a name="next-steps"></a>次の手順

[フォームの作成および設計](create-design-forms.md)
