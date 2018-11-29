---
title: モデル駆動型アプリにおける GridCell (Client API リファレンス) | Microsoft Docs
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
# <a name="gridcell-client-api-reference"></a>GridCell (クライアント API 参照)



GridCell は編集可能なグリッドに対してのみサポートされます。

選択したグリッドの行の GridCell は、編集可能なグリッドの属性に関連付けられたフォームにあるコントロールに似ています。 コレクション内のデータにアクセスするために使用できるメソッドの詳細については、「[コレクション (クライアント API 参照)](../collections.md)」を参照してください。

## <a name="methods"></a>メソッド

GridCell では、次のメソッドがサポートされます。

|Name |内容 |
|--|--|
|[clearNotification](../controls/clearNotification.md)| セルに対する通知をクリアします。|
|[getDisabled](../controls/getDisabled.md)| セルが無効かどうかを返します (読み取り専用)。|
|[setDisabled](../controls/setDisabled.md)| セルが無効かどうかを設定します。<br/><br/>**注意**: 読み取り専用セルの編集を有効にすると、レコードが保存されるときにエラーが発生する場合があります。 サーバーによってフィールドが読み取り専用と見なされると、値が変更された場合にエラーが発生する可能性があります。 このことは、ユーザーにレコードへの書き込み特権がない、レコードが無効である、または必要なフィールド レベルのセキュリティ特権をユーザーが持っていない、といった場合に生じる可能性があります。| 
|[setNotification](../controls/setNotification.md)|データが無効であることを示すために、セルに対してエラー メッセージを表示します。|
|[getLabel](../controls/getLabel.md)|セルを含む列のラベルを返します。|


### <a name="related-topics"></a>関連トピック

[モデル駆動型アプリにおけるグリッドおよびサブグリッド](../grids.md)

[コントロール](../controls.md)


