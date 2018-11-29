---
title: モデル駆動型アプリにおける addOnLoad (クライアント API 参照) | Microsoft Docs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 31a146de-9e25-43be-ae3e-83a2a5c86543
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="addonload-client-api-reference"></a>addOnLoad (クライアント API 参照)



[!INCLUDE[./includes/addOnLoad-description.md](./includes/addOnLoad-description.md)]

## <a name="syntax"></a>構文

`formContext.ui.addOnLoad(myFunction)`

## <a name="parameter"></a>パラメーター

|Name|種類​​|必須出席者|内容|
|--|--|--|--|
|myFunction|関数リファレンス|あり|フォーム [OnLoad](../events/form-onload.md) イベントで実行する関数。  その関数は、イベント ハンドラー パイプラインの一番下に追加されます。 実行コンテキストは、この関数に最初のパラメーターとして自動的に渡されます。 詳細については、「[実行コンテキスト](../../clientapi-execution-context.md)」を参照してください。|

### <a name="related-topics"></a>関連トピック

[removeOnLoad](removeOnLoad.md)

[フォーム OnLoad イベント](../events/form-onload.md)

[formContext.ui](../formContext-ui.md)

[formContext](../../clientapi-form-context.md)

