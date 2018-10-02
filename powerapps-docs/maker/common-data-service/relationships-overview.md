---
title: PowerApps のエンティティの概要 | MicrosoftDocs
description: PowerApps ポータルを使用してエンティティを作成および編集する方法について説明します。
ms.custom: ''
ms.date: 07/25/2018
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
ms.assetid: null
caps.latest.revision: 0
ms.author: matp
manager: kvivek
search.audienceType:
  - maker
search.app:
  - PowerApps
  - D365CE
---

# <a name="entity-relationships-overview"></a>エンティティの関連付けの概要

エンティティ関係によって、エンティティ レコードを他のエンティティや同じエンティティからのレコードと関連付けることのできる方法が定義されます。 2 種類のエンティティ関係が用意されています。
- **一対多関連付け**。 一対多エンティティ関係では、多くの参照元 (関連) エンティティ レコードを単一の参照先 (主) エンティティ レコードと関連付けることができます。 参照先エンティティ レコードは "親" と呼ばれ、参照元エンティティのレコードは "子" と呼ばれることがあります。  多対 1 の関連付けは、1 対多の関連付けの下位観点です。
- **多対多関連付け**。 多対多エンティティ関係では、多数のエンティティ レコードを他の多数のエンティティ レコードと関連付けることができます。 多対多の関連付けを使用して関連付けられたレコードは同等であると考えられ、この関係は相互的なものです。 

## <a name="see-also"></a>関連項目
[エンティティ間の関連付けを作成](data-platform-entity-lookup.md) <br/>
[PowerApps ポータルを使用してアプリ用 Common Data Service で多対多のエンティティの関連付けを作成する](create-edit-nn-relationships-portal.md)
