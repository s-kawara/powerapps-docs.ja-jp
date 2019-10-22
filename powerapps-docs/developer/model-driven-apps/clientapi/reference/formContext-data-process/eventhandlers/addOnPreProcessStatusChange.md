---
title: Dynamics 365 for Customer Engagement の addOnPreProcessStatusChange (クライアント API 参照) | MicrosoftDocs
ms.date: 08/05/2017
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 for Customer Engagement (online)
ms.assetid: null
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - D365CE
---
# <a name="addonpreprocessstatuschange-client-api-reference"></a>addOnPreProcessStatusChange (クライアント API 参照)

[!INCLUDE[](../../../../../../includes/cc_applies_to_update_9_0_0.md)]

[!INCLUDE[./includes/addOnPreProcessStatusChange-description.md](./includes/addOnPreProcessStatusChange-description.md)]

## <a name="syntax"></a>構文

`formContext.data.process.addOnPreProcessStatusChange(myFunction);`

## <a name="parameter"></a>パラメーター

|Name|種類​​|必須出席者|内容|
|--|--|--|--|
|myFunction|関数リファレンス|あり|業務プロセス フローの状態を変更するときに実行する関数です。 その関数は、イベント ハンドラー パイプラインのスタートに追加されます。 実行コンテキストは、この関数に最初のパラメーターとして自動的に渡されます。 詳細については、「[実行コンテキスト](../../../clientapi-execution-context.md)」を参照してください。<br/><br/>後でイベント ハンドラーを削除する場合は、匿名関数ではなく、名前付き関数への参照を使用する必要があります。|

このクライアントAPIは統一クライアントでのみサポートされます。 従来WebクライアントではこのクライアントAPIはサポートされていません。

### <a name="related-topics"></a>関連トピック

[removeOnPreProcessStatusChange](removeOnPreProcessStatusChange.md)

[formContext.data.process](../../formContext-data-process.md)
