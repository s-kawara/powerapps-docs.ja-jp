---
title: PowerApps のエンティティ概要 | Microsoft Docs
description: PowerApps ポータルを利用してエンティティを作成し、編集する方法について説明します
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
ms.assetid: ''
caps.latest.revision: 0
ms.author: matp
manager: kvivek
ms.openlocfilehash: 1c45941a7b00e9393aab429d2573b2e48964a4de
ms.sourcegitcommit: aba996b1773ecdf62758e06b34eaf57bede29e08
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/08/2018
ms.locfileid: "39695997"
---
# <a name="entity-relationships-overview"></a>エンティティ リレーションシップの概要

エンティティ リレーションシップによって、エンティティ レコードを他のエンティティまたは同じエンティティのレコードに関連付ける方法が定義されます。 エンティティ リレーションシップには 2 つの種類があります。
- **一対多のリレーションシップ**。 一対多のエンティティ リレーションシップでは、複数の参照元 (関連) エンティティ レコードを、1 つの参照先 (プライマリ) エンティティ レコードに関連付けることができます。 参照先エンティティ レコードは「親」と呼ばれ、参照元エンティティのレコードは「子」と呼ばれる場合があります。  多対一のリレーションシップは、一対多のリレーションシップを子の側から見た場合にすぎません。
- **多対多のリレーションシップ**。 多対多のエンティティ リレーションシップでは、複数のエンティティ レコードを他の複数のエンティティ レコードに関連付けることができます。 多対多のリレーションシップを使用して関連付けられるレコードはピアと見なすことができ、リレーションシップは相互関係となります。 

## <a name="see-also"></a>関連項目
[エンティティ間のリレーションシップを作成する](data-platform-entity-lookup.md) <br/>
[PowerApps ポータルを使用してアプリ用 Common Data Service に多対多のエンティティ リレーションシップを作成する](create-edit-nn-relationships-portal.md)