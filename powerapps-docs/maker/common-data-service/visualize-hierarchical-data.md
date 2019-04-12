---
title: モデル駆動型アプリによる階層型データのビジュアル化 | MicrosoftDocs
description: 関連する階層データをクエリおよびビジュアル化する方法を学習します
ms.custom: ''
ms.date: 09/19/2018
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
ms.author: matp
manager: kvivek
search.audienceType:
  - maker
search.app:
  - PowerApps
  - D365CE
---
# <a name="visualize-hierarchical-data-with-model-driven-apps"></a>モデル駆動型アプリによる階層型データのビジュアル化

階層型自己参照の関連付けを持つようにエンティティが構成されている場合は、その階層を使用してビジュアル化を設定できます。 詳細情報: [階層的に関連するデータを定義およびクエリする](../common-data-service/define-query-hierarchical-data.md)

既定でビジュアル化を使用可能なエンティティには、[取引先企業](/powerapps/developer/common-data-service/reference/entities/account)、[ポジション](/powerapps/developer/common-data-service/reference/entities/position)、[ユーザー](/powerapps/developer/common-data-service/reference/entities/systemuser) が含まれます。 これらのエンティティ グリッド ビューには、レコード名の左側に階層グラフを表示するアイコンが表示されます。 階層アイコンは既定ではすべてレコードに存在するわけではありません。 アイコンは、階層の関連付けを使用して関連するレコードに表示されます。  
> [!div class="mx-imgBorder"] 
> ![[階層] ボタンの表示](media/view-hierarchy-button.png)  
  
 階層アイコンを選択すると、次に示すように、左側にツリー ビュー、右側にタイルビューの形で階層を表示できます。  
  
> [!div class="mx-imgBorder"] 
> ![階層のツリーとタイル ビュー](media/tree-view-and-tile-view-in-hierarchy.png)  
  
 階層のすべての他のいくつかのエンティティは有効にすることができます。 これらのエンティティには、[取引先担当者](/powerapps/developer/common-data-service/reference/entities/contact)と[チーム](/powerapps/developer/common-data-service/reference/entities/team)が含まれます。 階層のすべてのユーザー定義エンティティは有効にすることができます。  
  
ビジュアル化の作成で重要な留意点は次のとおりです。  
  
- 各エンティティについて (1:N) の自己参照の関連付けを 1 つだけ階層として設定できます。 自己参照の関連付けで、主エンティティおよび関連エンティティが同じ種類である必要があります。  
- 階層またはビジュアル化は 1 つのエンティティのみに基づいています。 取引先企業を複数レベルで示す取引先企業階層を表現することはできますが、取引先企業と取引先担当者を同じ階層型ビジュアル化に表示することはできません。 
- タイルに表示できる最大のレコード数は 4 です。 タイル ビューに使用される簡易入力フォームに複数のフィールドを追加すると、最初の 4 つのフィールドだけが表示されます。 

## <a name="hierarchy-settings"></a>階層設定

階層のビジュアル化を有効にするには、階層を簡易表示フォームに接続する必要があります。 これは、ソリューション エクスプローラーを使用してのみ行うことができます。

[!INCLUDE [cc_navigate-solution-from-powerapps-portal](../../includes/cc_navigate-solution-from-powerapps-portal.md)]

階層設定は、ソリューション エクスプローラーでエンティティに関連付けられます。 

1. [エンティティを表示](../common-data-service/create-edit-entities-solution-explorer.md#view-entities)しながら、**階層構成**を選択することもできます。
2. 既存の階層設定がある場合は、それを編集できます。 それ以外の場合は、**新規**をクリックして新規作成します。
    
    > [!NOTE]
    > 階層設定が存在しない場合、エンティティで階層を構成することはできません。
    >階層設定は 1 つのみ存在できます。 

1. 以下のフィールドでデータを設定します。

|フィールド|説明|
|--|--|
|**名前**|*必須。* 階層設定の一意の名前を追加します。 これは、通常エンティティの名前にすぎません。 この値には、ソリューション発行者のカスタマイズ接頭辞が含まれます。|
|**既定の簡易表示フォーム**|*必須。* 既存の簡易ビュー フォームから選択することや、**新規作成** を選択して簡易ビュー フォーム エディターを開き、新規作成します。|
|**階層的な関連付け**|*必須。* 階層型の関連付けが既にエンティティに定義されている場合、値はここで設定されます。 値がない場合、**関係を階層に対して有効としてマークします** を選択してダイアログを開き、使用可能な自己参照の関連付けのいずれかを選択します。|
|**説明**|今後システムをカスタマイズするユーザーが、これが行われた理由を理解できるように、この階層の目的の説明を含めます。|
    

ビジュアル化のための同じ階層設定は一度に設定されますが、Web とモバイル クライアントの両方に適用されます。 タブレット PC では、ビジュアルは小さいフォーム ファクターに最適な修正した形式で作成されます。 階層のビジュアル化に必要なカスタマイズ可能なコンポーネントはソリューションに対応しているため、そのほかのカスタマイズのように、組織間で移動できます。 簡易入力フォームをフォーム エディターでカスタマイズして、ビジュアル化に表示される属性を構成できます。
  
## <a name="visualization-walk-through"></a>ビジュアル化のチュートリアル

ユーザー定義エンティティのビジュアル化の作成の例を見てみましょう。 以下に示すように、`new_Widget` という名前のユーザー定義エンティティを作成し、(1:N) の自己参照関連付け `new_new_widget_new_widget` を作成し、それを階層として登録しました。  
  
![ウィジェット関連付けの定義](media/widget-relationship-definition.png)  
  
次に、**階層設定**グリッド ビューで、`new_new_widget_new_widget` という階層の関連付けを選択しました。 フォームの必須フィールドに入力しました。 (1:N) の関連付けを階層としてまだ登録していなかった場合は、フォーム上のリンクから関連付けの定義フォームに戻って、関連付けを階層として登録することができます。  

> [!IMPORTANT]
> エンティティごとに、階層関係は一度に 1 つのみです。 これを別の自己参照関連付けに変更すると、問題が発生することがあります。 詳細情報: [階層データの定義](../common-data-service/define-query-hierarchical-data.md#define-hierarchical-data)

> [!div class="mx-imgBorder"] 
> ![階層設定](media/hierarchy-settings.png)  
  
**簡易表示フォーム**について、**ウィジェットの階層タイル フォーム**という名前の簡易入力フォームを作成しました。 このフォームで、各タイルに表示する 4 つのフィールドを追加しました。  

> [!div class="mx-imgBorder"] 
> ![ウィジェットの簡易入力フォームを作成する](media/create-quickform.png)  
  
このセットアップが完了した後、*Standard Widget* と *Premium Widget* という 2 つのレコードを作成しました。 Premium Widget を検索フィールドを使用して Standard Widget の親にした後、以下に示すように、`new_Widget` グリッド ビューに階層アイコンが表示されました。  

> [!div class="mx-imgBorder"] 
> ![ウィジェットの階層グリッド](media/widget-hierarchy-grid.png)  
  
> [!NOTE]
>  階層アイコンは、レコードが階層関係を使用して関連付けられるまで、レコード グリッド ビューに表示されません。  
  
階層アイコンを選択すると、左側にツリー ビュー、右側にタイルビューの形で、2 つのレコードを示す `new_Widget` 階層が表示されます。 各タイルには、**ウィジェットの階層タイル フォーム**で指定した 4 つのフィールドが含まれています。  

> [!div class="mx-imgBorder"] 
> ![ウィジェットのツリーとタイルの表示](media/widget-tree-tiles.png)  

ユーザーは、必要に応じて、階層全体を表示するツリー ビューか、または階層のより小さい部分を表示するタイル表示を選択できます。 両方のビューは並んで表示されます。 階層ツリーを展開および折りたたむことで、階層を調べることができます。 

### <a name="see-also"></a>関連項目 

[階層的に関連するデータの定義とクエリ](../common-data-service/define-query-hierarchical-data.md)<br />
[ビデオ: 階層ビジュアル化](http://www.youtube.com/watch?v=_dGBE6icLNw&index=9&list=PLC3591A8FE4ADBE07)
