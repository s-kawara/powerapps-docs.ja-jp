---
title: Dynamics 365 for Customer Engagement の addOnPreStageChange (クライアント API 参照) | MicrosoftDocs
ms.date: 07/19/2019
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 for Customer Engagement (online)
ms.assetid: null
author: msftman
ms.author: deonhe
manager: KVivek
search.audienceType:
  - developer
search.app:
  - D365CE
---
# <a name="addonprestagechange-client-api-reference"></a>addOnPreStageChange (クライアント API 参照)

[!INCLUDE[./includes/addOnStageChange-description.md](./includes/AddOnPreStageChange-description.md)]

## <a name="syntax"></a>構文

`formContext.data.process.addOnPreStageChange(myFunction);`

## <a name="parameter"></a>パラメーター

Name|種類​​|必須出席者|説明|
|--|--|--|--|
|myFunction|関数リファレンス|あり|業務プロセス フローのステージを変更する **前** に実行する関数です。 その関数は、イベント ハンドラー パイプラインのスタートに追加されます。 実行コンテキストは、この関数に最初のパラメーターとして自動的に渡されます。 詳細については、「[実行コンテキスト](../../../clientapi-execution-context.md)」を参照してください。<br/><br/>後でイベント ハンドラーを削除する場合は、匿名関数ではなく、名前付き関数への参照を使用する必要があります。|

このクライアントAPIは統一クライアントでのみサポートされます。 従来WebクライアントではこのクライアントAPIはサポートされていません。

### <a name="related-topics"></a>関連トピック

- [addOnStageChange](addOnStageChange.md)
 
- [removeOnStageChange](removeOnStageChange.md)

- [formContext.data.process](../../formContext-data-process.md)
 


