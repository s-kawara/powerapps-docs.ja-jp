---
title: PowerApps でフィールドを削除する | Microsoft Docs
description: フィールドの削除方法について説明します
ms.custom: ''
ms.date: 06/20/2018
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
ms.assetid: 578ac950-da16-4ec6-a0a4-25f3aaa3b96e
caps.latest.revision: 33
ms.author: matp
manager: kvivek
tags: ''
ms.openlocfilehash: 82e560f063f2e46190420b6be5cef4cc55d9ab4f
ms.sourcegitcommit: aba996b1773ecdf62758e06b34eaf57bede29e08
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/08/2018
ms.locfileid: "39692669"
---
# <a name="delete-fields"></a>フィールドを削除する

<a name="BKMK_DeletingFields"></a>   
 
 システム管理者ロールが与えられているユーザーは、マネージド ソリューションに含まれないカスタム フィールドすべてを削除できます。 フィールドを削除すると、フィールドに格納されているすべてのデータは失われます。 削除されたフィールドからデータを復元する唯一の方法は、フィールドが削除される前のポイントからデータベースを復元することです。  
  
 カスタム エンティティを削除するには、他のソリューション コンポーネントに存在する可能性のあるすべての依存関係を事前に削除する必要があります。 フィールドを開き、メニューバーの **[依存関係を表示]** ボタンを使用して、すべての **[依存コンポーネント]** を表示します。 たとえば、フィールドがフォームまたはビューで使用されている場合は、まずそのソリューション コンポーネントのフィールドへの参照を削除する必要があります。  
  
 ルックアップ フィールドを削除すると、その 1:N のエンティティ関係は自動的に削除されます。  

 ## <a name="next-steps"></a>次の手順

 [カスタム エンティティの削除](data-platform-delete-entity.md)
