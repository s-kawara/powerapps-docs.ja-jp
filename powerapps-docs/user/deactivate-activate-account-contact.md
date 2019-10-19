---
title: モデル駆動型アプリでアカウントまたは連絡先を非アクティブ化またはアクティブ化する |MicrosoftDocs
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
ms.openlocfilehash: a0b4e125749d5b0179489677e9a1103cb14a0697
ms.sourcegitcommit: 481a89e50c282f1e533a8526035dd3c38e3818a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/08/2019
ms.locfileid: "72023297"
---
# <a name="deactivate-or-activate-an-account-or-contact"></a>アカウントまたは連絡先を非アクティブ化またはアクティブ化する

モデル駆動型アプリでは、アカウントを削除するのではなく、アカウントを非アクティブ化することができます。 これにより、そのレコードに関連付けられている監査証跡の整合性が確保されます。  
  
非アクティブ化されたアカウントまたは連絡先は非アクティブになります。つまり、他のレコードとの新しい関係を確立するときに、そのアカウントまたは連絡先を編集したり使用したりする ただし、非アクティブ化された項目で作成されたすべてのリレーションシップは引き続き使用できます。  
  
後で非アクティブ化されたアカウントを再び有効にする必要がある場合は、簡単に再アクティブ化することができます。   
  
## <a name="deactivate-an-account-or-contact"></a>アカウントまたは連絡先を非アクティブ化する 
  
1.  左側のメニューで、 **[アカウント]** または **[連絡先]** に移動します。  
  
2.  非アクティブ化するアクティブなアカウントまたは連絡先を選択し、コマンドバーの **[非アクティブ化]** を選択して、非アクティブ化を確定します。

    > [!div class="mx-imgBorder"]
    > Powerapps で![アカウントを非アクティブ化](media/DeactiveAccounts.png "する powerapps でアカウントを非アクティブ化する")


## <a name="activate-an-account-or-contact"></a>アカウントまたは連絡先のアクティブ化  
  
1.  左側のメニューで、 **[アカウント]** または **[連絡先]** に移動します。 
  
2.  **システムビュー**の一覧にアクセスします。

3.  **非アクティブなアカウント**または**非アクティブな連絡先**を選択します。  
  
4.  アクティブ化する非アクティブなアカウントまたは連絡先を選択します。

5.  **[アクティブ化]** を選択し、アクティブ化を確定します。  

    > [!div class="mx-imgBorder"]
    > Powerapps で![アカウントをアクティブ化]する(media/ActiveAccounts.png "powerapps でアカウントをアクティブ化する")  



