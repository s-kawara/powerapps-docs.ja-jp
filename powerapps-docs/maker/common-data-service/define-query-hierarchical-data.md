---
title: Common Data Service for Apps で階層データの定義とクエリを行う |MicrosoftDocs
description: 階層的な関連データを定義とクエリを行う方法について説明します
ms.custom: ''
ms.date: 06/02/2018
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
ms.assetid: 0cf62817-5ff5-40bb-ad17-e1f6b0921720
caps.latest.revision: 42
ms.author: matp
manager: kvivek
ms.openlocfilehash: 4dad7da635156350d104d68108ac4acfbb991862
ms.sourcegitcommit: aba996b1773ecdf62758e06b34eaf57bede29e08
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/08/2018
ms.locfileid: "39690725"
---
# <a name="define-and-query-hierarchically-related-data"></a>階層的な関連データの定義とクエリを行う

階層的な関連データを定義とクエリを実行すると、貴重なビジネスの分析情報を得ることができます。 階層モデリングおよび視覚化機能にはさまざまな利点があります。  
  
- 複雑な階層情報を表示および探索します。  
- 階層のコンテキスト ビューで、主要業績評価指標 (KPI) を表示します。  
- Web およびタブレットにわたって重要な情報を視覚的に分析します。  
  
一部の標準エンティティでは、階層が既に定義されています。 カスタム エンティティを含むその他のエンティティは、階層に対して有効化でき、それらの視覚エフェクトを作成できます。 

## <a name="define-hierarchical-data"></a>階層データを定義する

Common Data Service for Apps では、関連レコードの*自己参照型*一対多 (1:N) リレーションシップによって階層データ構造がサポートされています。 

> [!NOTE]
> *自己参照型*とは、エンティティがそれ自体に関連することを意味します。 たとえば、アカウント エンティティには、別のアカウント エンティティ レコードに関連付ける参照フィールドがあります。

自己参照型一対多 (1:N) リレーションシップが存在する場合は、[Relationship definition]/(リレーションシップの定義/) で、**[Hierarchical]/(階層/)** オプションを **[はい]** に設定できます。

![リレーションシップの定義での階層設定](media/self-referential-relationship-car-solution-explorer.png)

データを階層としてクエリを実行するには、エンティティの自己参照型一対多 (1:N) リレーションシップのいずれかを階層として設定する必要があります。 この処理には必ずソリューション エクスプ ローラーを使用します。

[!INCLUDE [cc_navigate-solution-from-powerapps-portal](../../includes/cc_navigate-solution-from-powerapps-portal.md)]

階層を有効にするには、次の手順に従います。  
  
1. [1:N リレーションシップの表示](create-edit-1n-relationships-solution-explorer.md#view-entity-relationships)中に、編集する自己参照型リレーションシップを選択します。
2. **[Relationship definition]/(リレーションシップの定義/)** で、**[Hierarchical]/(階層/)** を **[はい]** に設定します。  
  
> [!NOTE]
> - 一部の標準の (1: N) リレーションシップはカスタマイズできません。 これらのリレーションシップを階層として設定できなくなります。  
> - システムの自己参照型リレーションシップに対して、階層リレーションシップを指定できます。 これには、"contact_master_contact" リレーションシップなど、システムの種類の 1:N 自己参照型リレーションシップが含まれます。  

> [!IMPORTANT]
> 複数の自己参照型リレーションシップを含めることができますが、階層リレーションシップとして定義できるのは、エンティティごとに 1 つのリレーションシップだけです。 適用後の設定を変更しようとすると、次の警告が表示されます。
>
> - **無効にする場合:** If you turn off the hierarchy setting for this relationship, all rollup definitions, processes, and views that use this hierarchy won't work. Do you want to continue? (このリレーションシップの階層設定をオフにすると、この階層を使用するすべてのロールアップ定義、プロセス、およびビューが機能しなくなります。 続行しますか。) 
> - **有効にする場合:** If you enable the hierarchy setting for this relationship, all rollup definitions that use the existing hierarchy will become invalid. Do you want to continue? (このリレーションシップの階層設定を有効にすると、既存の階層を使用するすべてのロールアップ定義が無効になります。 続行しますか。)
>
> 既存の階層上に明らかに他の依存関係がない場合を除き、続行する前に、デプロイに関するドキュメントを確認するか、または他のカスタマイザーに相談して、既存の階層リレーションシップを使用する方法を理解する必要があります。

<a name="BKMK_Querydata"></a> 
  
## <a name="query-hierarchical-data"></a>階層データのクエリを実行する  

定義済みの階層がない場合に階層データを取得するには、繰り返し関連レコードにクエリを実行する必要があります。 定義済みの階層がある場合は、1 つの手順で階層として関連データのクエリを実行できます。 **Under** および **Not Under** ロジックを使用して、レコードをクエリできます。 **Under** および **Not Under** 階層演算子は、高度な検索とワークフロー エディターで公開されています。 これらの演算子の使用方法の詳細については、[ワークフロー ステップの構成](/flow/configure-workflow-steps#setting-conditions-for-workflow-actions)に関するページを参照してください。 高度な検索の詳細については、「[高度な検索の作成、編集または保存](https://docs.microsoft.com/dynamics365/customer-engagement/basics/save-advanced-find-search)」を参照してください。  

> [!NOTE]
> 開発者はこれらの演算子をコードで使用することもできます。 詳細については、[開発者向けドキュメントの階層データのクエリの実行](/dynamics365/customer-engagement/developer/org-service/query-hierarchical-data)に関するページを参照してください。
  
次の例では、階層に対しクエリを実行するためのシナリオを示します。  
  
### <a name="query-account-hierarchy"></a>アカウント階層のクエリ  
  
![アカウント階層でのアカウントのクエリ](media/query-accounts.png)  
  
### <a name="query-account-hierarchy-including-related-activities"></a>関連アクティビティを含むアカウント階層のクエリ  
  
![アカウントの関連アクティビティのクエリ](media/query-account-related-activities.png)  
  
###  <a name="query-account-hierarchy-including-related-opportunities"></a>関連する営業案件を含むアカウント階層のクエリ  
  
![アカウントの関連する営業案件のクエリ](media/query-account-related-opportunities.png)  
  
## <a name="see-also"></a>関連項目 
[1:N (一対多) または N:1 (多対一) のエンティティ リレーションシップを作成および編集する](create-edit-1n-relationships.md)<br />
[ソリューション エクスプローラーを使用して 1:N (一対多) または N:1 (多対一) のエンティティ リレーションシップを作成および編集する](create-edit-1n-relationships-solution-explorer.md)<br />
[モデル駆動型アプリで階層データを視覚化する](visualize-hierarchical-data.md)<br />
[ビデオ: 階層セキュリティ モデリング](http://www.youtube.com/watch?v=kx5So32DrCo&index=10&list=PLC3591A8FE4ADBE07)<br />
[ビデオ: 階層の視覚化](http://www.youtube.com/watch?v=_dGBE6icLNw&index=9&list=PLC3591A8FE4ADBE07)
