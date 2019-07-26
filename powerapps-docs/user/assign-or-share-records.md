---
title: レコードの割り当てまたは共有 |MicrosoftDocs
ms.custom: ''
author: mduelae
manager: kvivek
ms.service: powerapps
ms.component: pa-user
ms.topic: conceptual
ms.date: 7/22/2019
ms.author: mduelae
ms.reviewer: ''
ms.assetid: ''
search.audienceType:
- enduser
search.app:
- PowerApps
- D365CE
ms.openlocfilehash: 9091121e874726681e062ef3bb09fc4f561a8a18
ms.sourcegitcommit: 8f27a61ce2ec32b8d911845dd00708e3c87b86bb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/24/2019
ms.locfileid: "68428893"
---
# <a name="assign-or-share-records"></a>レコードの割り当てまたは共有

組織内の別のユーザーが顧客レコードを処理できるようにする場合は、その人物にレコードを割り当てることができます。 また、チームや自分自身にレコードを割り当てることもできます。  

レコードの所有権を保持し、他のユーザーが自分で作業できるようにする場合は、 **[共有]** オプションを使用します。 

1. 左側のナビゲーションウィンドウで、レコードの種類を選択します。 たとえば、 **Contacts**です。

2. レコードの一覧から、再割り当てするレコードを選択します。  
  
3. コマンドバーで **[割り当て]** を選択します。

   > [!div class="mx-imgBorder"]
   > ![レコードの再割り当て](media/assign1.png "レコードの再割り当て")

   > [!NOTE]
   > レコードの所有権を保持し、他のユーザーがそのレコードを操作できるようにするには、 **[共有]** を選択します。 次に、ツールヒントを使用して、 **[共有]** オプションを表示します。 
   
4. 割り当て] ダイアログボックスの **[割り当て先]** 領域で、[ユーザー また**は [ユーザー] または [チーム**] を選択します。

   > [!div class="mx-imgBorder"]
   > ![自分またはチームへのレコードの再割り当て](media/assign2.png "レコードを再割り当てするチーム")
  
   [ユーザー]**または [チーム**] を選択した場合は、 **[検索するレコード]** ボックスにユーザーまたはチームの名前を入力します。 新しいレコードを作成する必要がある場合は、 **[+ 新規]** を選択します。
  
5. 完了したら、 **[割り当て]** を選択します。

## <a name="use-advanced-find-to-reassign-records"></a>高度な検索を使用してレコードを再割り当てする

高度な検索を使用してレコードを検索し、他のユーザーに再割り当てします。 高度な検索の詳細については、「高度な検索[検索の作成、編集、または保存](create-edit-or-save-advanced-find-search.md)」を参照してください。


1. コマンドバーで **[高度な検索]** を選択します。

   > [!div class="mx-imgBorder"]
   > ![高度な検索](media/assign3.png "advacned 検索")
   
2. レコードの一覧から、再割り当てするレコードを選択し、[割り当て] オプションを選択します。

   > [!div class="mx-imgBorder"]
   > ![高度な検索を使用してレコードを再割り当てする](media/assign4.png "Advacned find を使用してレコードを再割り当て")する
   
 
 ## <a name="reassign-all-records-for-admins"></a>すべてのレコードを再割り当てする (管理者用)
 
 管理者は、[管理者の設定] 領域からユーザーのすべてのレコードを再割り当てできます。
 
 1. **[設定]**  >  **[セキュリティ]** の順に移動します。
 2. [**ユーザー] を**選択し、ユーザー名を選択して、ユーザーのプロファイルを開きます。
 3. コマンドバーで、 **[レコードの再割り当て]** を選択します。
 
   > [!div class="mx-imgBorder"]
   > ![すべてのレコードを再割り当て]する(media/assign5.png "すべてのレコードを再割り当て")する
   
 4. **[レコードの再割り当て]** ダイアログボックスで、すべてのレコードを再割り当てする方法を選択し、[ **OK]** を選択します。
 
  > [!NOTE]
   > **[レコードの再割り当て]** オプションを選択すると、その状態に関係なくすべてのレコードが再割り当てされます。 アクティブでないレコードとアクティブなレコードは、他のユーザーまたはチームに再割り当てされます。
 
   > [!div class="mx-imgBorder"]
   > ![ユーザーまたはチームにすべてのレコードを再割り当てする](media/assign6.png "ユーザーまたはチームにすべてのレコードを再割り当てする")
 

