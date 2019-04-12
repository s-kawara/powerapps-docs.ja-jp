---
title: カテゴリ エンティティの使用 (Common Data Service) | Microsoft Docs
description: カテゴリ エンティティを使用したエンティティ レコードの分類について説明します。
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
# <a name="use-the-category-entity"></a>カテゴリ エンティティを使用してください。

Common Data Service でエンティティ レコードを分類すると、レコードにタグをつけるのに便利で簡単に検索できます。 Common Data Service で新しい `Category` エンティティを使用して、カテゴリの階層構造を作成して管理し、次に 1 つまたは複数のカテゴリにエンティティ レコードを関連付けます。  
  
 カテゴリは複数の子カテゴリを持つ場合がありますが、子カテゴリは親カテゴリを 1 つのみ持つことができます。 親 `Category` レコードを削除すると、そのすべての子レコードおよびエンティティ関係が自動的に削除されます。 あるカテゴリの親カテゴリは、`Category.ParentCategoryId` 属性を使用して定義します。  
  
 `Category.SequenceNumber` 属性を使用して、階層内のカテゴリ表示順序をプログラムで定義します。  Web クライアントを使用して新しいカテゴリを追加するとき、それは階層の最後のカテゴリの後ろに自動的に追加されます。 また、`Category.CategoryNumber` 属性を使用して、カテゴリの番号をプログラムでセットまたは更新し、容易にカテゴリのグループを識別することができます。 カテゴリ番号には任意の値をプログラムでセットすることができますが、Web クライアント内のカテゴリのために管理者が指定した自動番号付けの接頭辞に基づき、Web クライアントを使用してカテゴリを作成するときに自動的にセットすることができます (**設定** > **管理** > **自動付番** > **カテゴリ**タブ)。  
  
 リレーションシップおよび接続を使用して、`Category` レコードをシステムおよびユーザ定義エンティティ レコードを関連付けることができます。 カテゴリ レコードは異なるエンティティ レコードに関連付けることができます。 たとえば、プログラムで `Category` レコードを `Account`、`Contact` および `Incident` レコードと関連付けることができます。   

