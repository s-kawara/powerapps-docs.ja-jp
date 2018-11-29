---
title: モデル駆動型アプリにおける addOnSave (クライアント API 参照) | Microsoft Docs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 1a66f93d-a47c-4316-91f1-dcf5d09f9d19
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="addonsave-client-api-reference"></a>addOnSave (クライアント API 参照)



[!INCLUDE[./includes/addOnSave-description.md](./includes/addOnSave-description.md)]

## <a name="syntax"></a>構文

`formContext.data.entity.addOnSave(myFunction)`

## <a name="parameter"></a>パラメーター

|Name|種類​​|必須出席者|内容|
|--|--|--|--|
|myFunction|関数リファレンス|あり|レコードが保存されるときに実行される関数。  その関数は、イベント ハンドラー パイプラインの一番下に追加されます。 実行コンテキストは、この関数に最初のパラメーターとして自動的に渡されます。 詳細については、「[実行コンテキスト](../../clientapi-execution-context.md)」を参照してください。

### <a name="related-topics"></a>関連トピック

[removeOnSave](removeOnSave.md)

[フォーム OnSave イベント](../events/form-onsave.md)

