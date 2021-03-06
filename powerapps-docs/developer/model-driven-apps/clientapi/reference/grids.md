---
title: Dynamics 365 用モデル駆動型アプリにおけるグリッドとサブグリッド | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 9d35c036-637f-4580-8ba0-027a44c0fdee
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="grids-and-subgrids-in-model-driven-apps-client-api-reference"></a>モデル駆動型アプリにおけるグリッドおよびサブグリッド (クライアント API リファレンス)



モデル駆動型アプリでは、グリッドは表形式のデータを表します。 グリッドは、フォーム全体にまたがることも、フォーム上のアイテムの 1 つになることもできます。後者は *サブグリッド* と呼ばれます。

## <a name="types-of-grids"></a>グリッドの種類

モデル駆動型アプリのグリッドには 2 種類あります。
- **読み取り専用グリッド**: 表形式でデータを表示します。 読み取り専用グリッドに表示されているデータを編集するには、グリッド内のレコードをクリックして、フォームを開き、データを編集し、保存します。
-  **編集可能グリッド**: 表形式でデータを表示するだけでなく、同じグリッド内でのデータのグループ化、並び替え、およびフィルタ処理の機能を含めた Web およびモバイル クライアントでの豊富なインライン編集機能を提供するので、レコードまたはビューを切り替える必要はありません。 編集可能グリッドは、カスタム コントロールであり、Web クライアントおよびダッシュボードのフォームでのメイン グリッドやサブグリッド、およびモバイル クライアントでのフォーム グリッドでサポートされます。 編集可能グリッド コントロールでは編集機能を提供しますが、読み取り専用グリッド メターデータおよびフィールドレベルのセキュリティ設定に従います。

<a name="bkmk_gridcontext"></a>
## <a name="getting-the-grid-context"></a>グリッド コンテキストの取得

グリッド コンテキストは、コードを実行する対象であるフォーム上のグリッドまたはサブグリッドのインスタンスです。 JavaScript コードを実行するグリッド コンテキストの取得の詳細については、[クライアント API グリッド コンテキスト](../clientapi-grid-context.md)を参照してください

## <a name="events"></a>イベント

|Name|内容|次に適用可能|
|--|--|--|
|[Subgrid OnLoad イベント](events/subgrid-onload.md)|サブグリッドが更新されるたびに発生します。 これは、ユーザーが列見出しをクリックしてサブグリッド内の値を並べ替えるときに取り込まれます。|読み取り専用グリッド|
|[グリッド OnChange](events/grid-onchange.md)|編集可能なグリッドのセルで値が変更されているとき、またはセルがフォーカスを失ったときに発生します|編集可能なグリッド|
|[グリッド OnRecordSelect](events/grid-onrecordselect.md)|単一の行 (レコード) が編集可能なグリッドで選択されている場合に発生します|編集可能なグリッド|
|[グリッド OnSave](events/grid-onsave.md)|更新された情報がサーバーに送信される前、および次のいずれかが起こると発生します。レコードの選択で変更がある、ユーザーが編集可能なグリッドの保存ボタンを使用して、保存操作を明示的にトリガーする、または、保留中の変更がある間に編集可能なグリッドから、ユーザーが並べ替え、フィルター、グループ化、改ページ、ナビゲーション操作を適用する。|編集可能なグリッド|

>[!NOTE]
>エンティティまたは読み取り専用グリッドに対して編集可能なグリッドを有効にするために使用されるモデル駆動型アプリのページの**イベント** タブを使用して、**OnChange**、**OnRecordSelect**、および **OnSave** イベントに登録できます。

## <a name="methods"></a>メソッド

|Name|内容|以下に使用できます|
|--|--|--|
|[GridControl](grids/gridcontrol.md)|グリッドまたはサブグリッド コントロールを操作するためのメソッドを提供します。|読み取り専用および編集可能なグリッド|
|[グリッド](grids/grid.md)|グリッドのデータに関する情報にアクセスするためのメソッドを提供します。|読み取り専用および編集可能なグリッド|
|[GridRow](grids/gridrow.md)|グリッドの行または選択した行を操作するためのメソッドを提供します。|読み取り専用および編集可能なグリッド|
|[GridRowData](grids/gridrowdata.md)|グリッドの行または選択した行を操作するためのメソッドを提供します。|読み取り専用および編集可能なグリッド|
|[GridEntity](grids/gridentity.md)|行内の特定のレコードに関するデータにアクセスするためのメソッドを提供します。|読み取り専用および編集可能なグリッド|
|[GridAttribute](grids/gridattribute.md)|編集可能なグリッドのセルのデータにアクセスするためのメソッドを提供します。|編集可能なグリッド|
|[GridCell](grids/gridcell.md)|編集可能なグリッドの属性に関連付けられたフォーム上のコントロールに関連するデータにアクセスするメソッドを提供します。|編集可能なグリッド|
|[ViewSelector](grids/viewselector.md)|サブグリッド コントロールのビュー セレクターに関する情報を取得または設定するメソッドを提供します。|読み取り専用グリッド|


### <a name="related-topics"></a>関連トピック

[クライアントAPIグリッドコンテキスト](../clientapi-grid-context.md)

[編集可能グリッドの使用](../../use-editable-grids.md)

[モデル駆動型アプリのクライアント API リファレンス](../reference.md)

[モデル駆動型アプリの開発者向けの概要](../../overview.md)

