---
title: モデル駆動型アプリにおける refreshParentGrid (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 89123cde-7c66-4c7d-94e4-e287285019f8
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="refreshparentgrid-client-api-reference"></a>refreshParentGrid (クライアント API 参照)



[!INCLUDE[./includes/refreshParentGrid-description.md](./includes/refreshParentGrid-description.md)] 

## <a name="syntax"></a>構文

`Xrm.Utility.refreshParentGrid(lookupOptions)`

## <a name="parameters"></a>パラメーター

**lookupOptions**: レコードを指定する次のプロパティを持つオブジェクト:

|プロパティ名 |種類​​ |必須出席者  |内容 |
|---|---|---|---|
|entityType|String|あり |レコードのエンティティの種類。|
|ID|String|あり |レコードの ID。|
|名前|String|No |レコードの名前。|

### <a name="related-topics"></a>関連トピック

[Xrm.Utility](../xrm-utility.md)



