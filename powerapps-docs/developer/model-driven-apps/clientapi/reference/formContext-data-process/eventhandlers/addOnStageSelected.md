---
title: モデル駆動型アプリにおける addOnStageSelected (クライアント API 参照) | Microsoft Docs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 5982770c-d5a4-415a-a32d-3734b6210bb9
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="addonstageselected-client-api-reference"></a>addOnStageSelected (クライアント API 参照)



[!INCLUDE[./includes/addOnStageSelected-description.md](./includes/addOnStageSelected-description.md)]

## <a name="syntax"></a>構文

`formContext.data.process.addOnStageSelected(myFunction);`

## <a name="parameter"></a>パラメーター

|Name|種類​​|必須出席者|内容|
|--|--|--|--|
|myFunction|関数リファレンス|あり|業務プロセス フローのステージを選択するときに実行する関数です。  その関数は、イベント ハンドラー パイプラインの一番下に追加されます。 実行コンテキストは、この関数に最初のパラメーターとして自動的に渡されます。 詳細については、「[実行コンテキスト](../../../clientapi-execution-context.md)」を参照してください。<br/><br/>後でイベント ハンドラーを削除する場合は、匿名関数ではなく、名前付き関数への参照を使用する必要があります。|

### <a name="related-topics"></a>関連トピック

[removeOnStageSelected](removeOnStageSelected.md)
 
[formContext.data.process](../../formContext-data-process.md)
 


