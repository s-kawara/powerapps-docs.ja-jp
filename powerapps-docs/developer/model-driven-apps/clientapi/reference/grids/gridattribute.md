---
title: モデル駆動型アプリにおける GridAttribute (Client API リファレンス) | Microsoft Docs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 8139c622-e4d9-478f-9510-414d140e5556
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="gridattribute-client-api-reference"></a>GridAttribute (クライアント API 参照)



GridAttribute は編集可能なグリッドに対してのみサポートされます。

GridAttribute は編集可能なグリッドのセルのデータを表し、その属性に関連付けられているすべてのセルへの参照を含んでいます。 コレクション内のデータにアクセスするために使用できるメソッドの詳細については、「[コレクション (クライアント API 参照)](../collections.md)」を参照してください。

また、GridAttribute は、選択したグリッドの行の属性の**コントロール**コレクションをサポートしています。このコレクションは、属性に関連付けられているセルのコレクションを操作するメソッドを提供します。 選択したグリッドの行の各セル ([GridCell](gridcell.md)) は、編集可能なグリッドの属性に関連付けられたフォームにあるコントロールに似ています。 コレクション内のデータにアクセスするために使用できるメソッドの詳細については、「[コレクション (クライアント API 参照)](../collections.md)」を参照してください。

>[!TIP]
>パフォーマンス上の理由のため、編集可能なグリッドの行 (レコード) はレコードが選択されるまで編集できません。 ユーザーはグリッド内で単一レコードを選択して編集する必要があります。 編集可能なグリッドでレコードが選択されると、Dynamics 365 は、レコードへのユーザーアクセス、レコードがアクティブかどうか、フィールドの検証を含む一連の事柄を内部で評価して、データのセキュリティと有効性がデータの編集時に保証されていることを確認します。 編集可能な状態にあるグリッド内のレコードにアクセスするために、[getFormContext](../executioncontext/getFormContext.md) メソッドで [OnRecordSelect](../events/grid-onrecordselect.md) イベントを使用することを検討してください。

## <a name="methods"></a>メソッド

GridAttribute は、選択したグリッドの行の属性に対して次のメソッドをサポートしています。

|Name|内容|
|--|--|
|[getName](../attributes/getName.md)|選択したグリッドの行の属性の論理名を返します。|
|[getRequiredLevel](../attributes/getRequiredLevel.md)| 属性の値が必要または推奨かどうかを示す値を文字列を返します。|
|[setRequiredLevel](../attributes/setRequiredLevel.md)| レコードを保存できるようにするには、その前に、選択したグリッドの行の属性に対してデータが必須であるかまたは推奨であるか設定します。|
|[getValue](../attributes/getValue.md)| 属性のデータ値を取得します。|
|[setValue](../attributes/setValue.md)| 属性のデータ値を設定します。|

>[!NOTE]
>編集可能グリッドの行を選択するには、[Grid](grid.md).[getSelectedRows](grid/getSelectedRows.md) を使用します。

### <a name="related-topics"></a>関連トピック

[GridCell](gridcell.md)

[モデル駆動型アプリにおけるグリッドおよびサブグリッド](../grids.md)

[コントロール コレクション](../attributes/controls-collection.md)


