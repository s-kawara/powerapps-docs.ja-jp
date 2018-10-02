---
title: PowerApps でフィールドを削除する | MicrosoftDocs
description: フィールドを削除する方法を説明します
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
tags: null
search.audienceType:
  - maker
search.app:
  - PowerApps
  - D365CE
---
# <a name="delete-fields"></a>フィールドの削除

<a name="BKMK_DeletingFields"></a>   
 
 システム管理者のセキュリティ ロールを持つユーザーとして、管理ソリューションの一部でないユーザー定義フィールドを削除できます。 フィールドを削除するときに、フィールドに格納したデータはすべて失われます。 削除されたフィールドからデータを回復する唯一の方法は、フィールドが削除される前の時点からデータベースを復元することです。  
  
 ユーザー定義エンティティを削除する前に、他のソリューション コンポーネントに存在する依存関係を削除する必要があります。 フィールドを開き、メニュー バーの**依存関係の表示**ボタンを使用し、**依存コンポーネント**を表示します。 たとえば、フィールドがフォームまたはビューで使用される場合は、最初に、ソリューション コンポーネントでフィールドへの参照を削除する必要があります。  
  
 検索フィールドを削除すると、そのフィールドの 1:N エンティティ関係が自動的に削除されます。  

 ## <a name="next-steps"></a>次のステップ

 [ユーザー定義エンティティの削除](data-platform-delete-entity.md)
