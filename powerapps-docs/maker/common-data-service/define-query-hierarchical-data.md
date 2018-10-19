---
title: アプリ用 Common Data Service で階層データの定義とクエリ | MicrosoftDocs
description: 階層的に関連するデータを定義およびクエリする方法を説明する
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
search.audienceType:
  - maker
search.app:
  - PowerApps
  - D365CE
---
# <a name="define-and-query-hierarchically-related-data"></a>階層的に関連するデータの定義とクエリ

階層的に関連するデータを定義およびクエリすることにより、役に立つ業務把握が可能です。 階層モデル化およびビジュアル化の機能には、以下に示すさまざまな利点があります。  
  
- 複雑な階層情報を表示および検証します。  
- 主要業績評価指標 (KPI) を階層のコンテキスト ビューに表示します。  
- Web およびタブレット PC 全体の主要な情報を視覚的に分析します。  
  
一部の標準エンティティには、すでに階層が定義されています。 任意の階層にのユーザー定義エンティティを含むそのほかのエンティティを有効にし、それらのビジュアル化を作成することができます。 

## <a name="define-hierarchical-data"></a>階層データの定義

アプリ用 Common Data Service では、階層データ構造が、関連レコードの*自己参照*一対多 (1:N) の関連付けでサポートされます。 

> [!NOTE]
> *自己参照*では、エンティティがそれ自体に関連していることを意味します。 たとえば、取引先企業エンティティには別の取引先企業エンティティと関連付ける検索フィールドがあります。

自己参照の 1 対多 (1:N) の関連付けが存在する場合、関連付けの定義で **Hierarchcial** オプションを**はい**に設定できます。

![関係定義における階層設定](media/self-referential-relationship-car-solution-explorer.png)

データを階層としてクエリするには、エンティティの一対多 (1:N) の自己参照の関連付けの 1 つを階層として設定する必要があります。 これはソリューション エクスプローラーを使用してのみ行うことができます。

[!INCLUDE [cc_navigate-solution-from-powerapps-portal](../../includes/cc_navigate-solution-from-powerapps-portal.md)]

階層の有効化:  
  
1. [1:N 関連付けを表示](create-edit-1n-relationships-solution-explorer.md#view-entity-relationships)しているときに、編集したい自己参照の関連付けを選択します。
2. **関連付けの定義**で、**階層**に**はい**をセットします。  
  
> [!NOTE]
> - 一部の既定の (1:N) の関連付けはカスタマイズできません。 これにより、これらの関連付けを階層として設定することはできません。  
> - 自己参照の関連付けシステムには、階層型の関連付けを指定できます。 これには、"contact_master_contact" 関連付けなどの、システムタイプの 1:N の自己参照の関連付けが含まれます。  

> [!IMPORTANT]
> 複数の自己参照の関連付けを持つことができますが、エンティティごとに 1 つの関連付けのみを階層型の関連付けとして定義できます。 いったん適用した設定を変更しようとすると、警告が表示されます。
>
> - **無効にする場合:** この関連付けの階層設定をオフにすると、この階層を使用するすべてのロールアップ定義、プロセス、およびビューは動作しません。 続行しますか? 
> - **有効にする場合:** この関連付けの階層設定を有効にすると、既存の階層を使用するすべてのロールアップ定義が無効になります。 続行しますか?
>
> 既存の階層にその他の依存関係がないことを特定している場合を除き、展開に関するドキュメントを確認するか、他のカスタマイザーと相談して、既存の階層型の関連付けがどのように使用されているかを理解してください。

<a name="BKMK_Querydata"></a> 
  
## <a name="query-hierarchical-data"></a>クエリ階層型データ  

定義された階層がない場合、階層データを取得するには、関連レコードのクエリを繰り返す必要があります。 定義された階層では、関連データを階層として 1 回の手順でクエリすることができます。 レコードを**属する**と**属さない**のロジックを使用してクエリできます。 **に属する**と**に属さない**の階層演算子は、高度な検索やワークフロー エディタで公開されます。 これらの演算子の使用方法の詳細については、[ワークフロー ステップの構成](/flow/configure-workflow-steps#setting-conditions-for-workflow-actions) を参照してください。 高度な検索の詳細については、「[高度な検索の作成、編集または保存](https://docs.microsoft.com/dynamics365/customer-engagement/basics/save-advanced-find-search)」を参照してください。  

> [!NOTE]
> 開発者は、コード内でこれらの演算子を使用できます。 詳細 [開発者ドキュメント: クエリ階層型データ](/dynamics365/customer-engagement/developer/org-service/query-hierarchical-data)
  
階層クエリのさまざまなシナリオを示した例を以下に紹介します。  
  
### <a name="query-account-hierarchy"></a>取引先企業階層のクエリ  
  
![取引先企業階層クエリの取引先企業](media/query-accounts.png)  
  
### <a name="query-account-hierarchy-including-related-activities"></a>関連する活動を含む取引先企業のクエリ  
  
![クエリの取引先企業に関する活動](media/query-account-related-activities.png)  
  
###  <a name="query-account-hierarchy-including-related-opportunities"></a>関連する営業案件を含む取引先企業のクエリ  
  
![クエリの取引先企業に関する営業案件](media/query-account-related-opportunities.png)  
  
## <a name="see-also"></a>関連項目 
[1:N (一対多) または N:1 (多対一) のエンティティの作成および編集](create-edit-1n-relationships.md)<br />
[ソリューション エクスプローラーを使用して 1:N (1 対多) または N:1 (多対 1) のエンティティ関連付けを作成および編集する](create-edit-1n-relationships-solution-explorer.md)<br />
[モデル駆動型アプリによる階層型データのビジュアル化](visualize-hierarchical-data.md)<br />
[ビデオ: 階層セキュリティ モデル](http://www.youtube.com/watch?v=kx5So32DrCo&index=10&list=PLC3591A8FE4ADBE07)<br />
[ビデオ: 階層ビジュアル化](http://www.youtube.com/watch?v=_dGBE6icLNw&index=9&list=PLC3591A8FE4ADBE07)
