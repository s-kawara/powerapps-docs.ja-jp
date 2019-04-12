---
title: PowerApps でエンティティ フィールドをマップする | MicrosoftDocs
description: エンティティ フィールドのマップ方法を解説します
ms.custom: ''
ms.date: 05/29/2018
ms.reviewer: ''
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
  - Dynamics 365 Version 9.x
  - powerapps
author: Mattp123
ms.assetid: 7c5aa1c3-bde9-43f1-a369-fdcdbf14dec0
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
# <a name="map-entity-fields"></a>エンティティ フィールドのマップ
 
エンティティの関連付けを持つエンティティ間で属性をマップできます。 これにより、他のレコードのコンテキストで作成したレコードの既定値を設定できます。 

## <a name="easier-way-to-create-new-records-in-model-driven-apps"></a>モデル駆動型アプリで新しいレコードを作成する簡単な方法

特定の取引先企業の従業員に新しい取引先担当者レコードを追加すると仮定します。 2 つの方法でできます。  
  
### <a name="the-hard-way"></a>難しい方法

アプリに移動して、新しい取引先担当者レコードを初めから作成できます。 しかし、取引先企業の親会社を設定し、取引先企業の親会社と同じ情報の項目 (住所、電話番号など) を入力する必要があります。 これには時間がかかり、営業案件に間違いが生じる場合があります。  
  
### <a name="the-easier-way"></a>簡単な方法

最も簡単な方法は、取引先企業エンティティから開始し、フォームの**取引先担当者**サブグリッドを使って、**+** を選択して取引先担当者を追加することです。 最初に、関連する既存の取引先担当者を見つけるように促されるため、重複レコードを誤って作成することはありません。 既存のレコードが見つからなければ、**新規**を選択して、新しい取引先担当者レコードを作成することができます。 

新しい取引先担当者レコード フォームには、既定値として取引先企業からマップした属性値 (住所や電話番号など) が含まれています。 ユーザーはレコードを保存する前に、これらの値を編集できます。

## <a name="how-this-works"></a>しくみ

1:N エンティティ関連付けのエンティティ フィールドをマッピングすると、主エンティティ レコードから取られたデータの特定のアイテムが、新しい関連エンティティ フォームにコピーされ、保存する前に編集できる既定値が設定されます。
 
  
> [!NOTE]
> これらのマッピングは、保存する前に、レコードに既定値を設定するだけです。 保存する前に値を編集できます。 転送されるデータは、その時点のデータです。 ソース データが後で変更された場合は同期されません。
>   
> これらのマッピングは、ワークフローとダイアログ プロセスを使用して作成された関連レコードに適用されません。 開発者が使用可能なマッピングを使用して新しいレコードを作成するのに `InitializeFrom` ([InitializeFrom 関数](/dynamics365/customer-engagement/web-api/initializefrom?view=dynamics-ce-odata-9) または [InitializeFromRequest クラス](/dotnet/api/microsoft.crm.sdk.messages.initializefromrequest?view=dynamics-general-ce-9)) と呼ばれる特別なマッピングを使用しても、これらのマッピングはコードを使用して作成された新しいレコードに自動的には適用されません。  

## <a name="open-solution-explorer"></a>ソリューション エクスプローラーを開きます

エンティティ フィールドをマップする唯一の方法は、ソリューション エクスプローラーを使用することです。

[!INCLUDE [cc_navigate-solution-from-powerapps-portal](../../includes/cc_navigate-solution-from-powerapps-portal.md)]
  
フィールドのマッピングは、1:N または N:1 のエンティティの関連付けのコンテキストで行われるため、最初に [1:N または N:1 エンティティ関係を表示](create-edit-1n-relationships-solution-explorer.md#view-entity-relationships)する必要があります。

## <a name="view-mappable-fields"></a>マッピング可能なフィールドの表示

フィールド マッピングは、エンティティ関係内で実際に定義されていませんが、関連付けユーザー インターフェイスで公開されます。 すべての 1:N のエンティティ関係にあるわけではありません。 エンティティの 1:N (または N:1) エンティティ関係のリストを表示して、表示される関係を種類別にフィルター処理できます。 **すべて**、**カスタム**、**カスタマイズ可能**、または**マッピング可能**のいずれかを選択できます。 マッピング可能のエンティティ関係は、エンティティ フィールドのマッピング可能にするアクセスを提供します。 

![マッピング可能なエンティティの関連付けの表示](media/mappable-entity-relationships.png) 

マッピング可能な関連付けを開くとき、左側のナビゲーションの **マッピング** を選択します。

![エンティティの関連付けのマッピングを選択する](media/map-entity-fields-ui-solution-explorer.png)

## <a name="delete-mappings"></a>マッピングを削除する

適用しないマッピングがある場合は、それらを選択して ![[削除] アイコン](media/delete.gif) アイコンをクリックできます。

## <a name="add-new-mappings"></a>新しいマッピングを追加する

新しいマッピングを作成するには、ツール バーで、**新規** をクリックします。 これにより、**フィールド マッピングの作成** ダイアログが開きます。

![フィールド マッピング ダイアログを作成する](media/create-field-mapping-dialog.png)

マップする値を持つ 1 つのソース エンティティ フィールドと 1 つのターゲット エンティティ フィールドを選択します。 

![フィールド マッピングを構成する](media/configure-field-mapping.png)

次に、**OK** を選択してダイアログを閉じます。

次の規則は、マップできるデータの種類を示します。  
  
- 両方のフィールドが同じ種類で、同じ形式である必要があります。  
- ターゲット フィールドの長さが、ソース フィールドの長さと同じかそれ以上である必要があります。  
- ターゲット フィールドが、別のフィールドにまだマップされていない必要があります。  
- ソース フィールドがフォーム上で表示可能である必要があります。  
- ターゲット フィールドが、ユーザーがデータを入力可能なフィールドである必要があります。  
- アドレス ID の値はマップできません。
- フォームに表示されていないフィールドとの間でマップを行った場合、フィールドがフォームに追加されるまで、マッピングは行われません。
- フィールドがオプション セットの場合、各オプションの整数値が同一である必要があります。  
  
> [!NOTE]
>  オプション セット フィールドをマップする必要がある場合、同じグローバル オプション セットを使用するように両方のフィールドを構成するようお勧めします。 そうしないと、別々の 2 種類のオプションのセットの同期を手動で保つことが難しくなります。 各オプションの整数値が正しくマップされていない場合、データに問題が発生することがあります。 詳細: [Common Data Service のグローバル オプション設定の作成および編集 (候補リスト)](create-edit-global-option-sets.md)  
  
## <a name="automatically-generate-field-mappings"></a>フィールド マッピングを自動的に生成する  

**その他の操作** メニューから **マッピングの生成** を選択しても、マッピングを自動的に生成できます。

システム エンティティでこれを行うときは注意する必要があります。 ユーザー定義エンティティを作成し、マッピングを活用する場合に使用します。 

> [!WARNING]
> これにより、既存のマッピングがすべて削除され、類似の名前とデータの種類を持つフィールドのみに基づく推奨のマッピングで置き換えます。 システム エンティティで使用している場合は、必要なマッピングを失う場合があります。 ユーザー定義エンティティの場合、不要なマッピングを容易に削除し、マッピングの生成操作で作成されなかったそのほかのものを追加できるので時間を節約できます。  


## <a name="publish-customizations"></a>カスタマイズの公開 

フィールド マッピングがメタデータではないため、変更を有効にするには公開する必要があります。 
<!-- TODO Need a general topic about publishing to link to in situations like this -->

### <a name="see-also"></a>関連項目
[ソリューション エクスプローラーを使用して 1:N (1 対多) または N:1 (多対 1) のエンティティ関連付けを作成および編集する](create-edit-1n-relationships-solution-explorer.md)<br />
[開発者ドキュメント: エンティティ マッピングおよび属性マッピングのカスタマイズ](/dynamics365/customer-engagement/developer/customize-entity-attribute-mappings)<br />
[開発者ドキュメント: Web API 別のエンティティから新しいエンティティを作成する](/dynamics365/customer-engagement/developer/webapi/create-entity-web-api#create-a-new-entity-from-another-entity)
