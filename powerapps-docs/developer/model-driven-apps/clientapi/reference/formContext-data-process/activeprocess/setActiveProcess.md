---
title: モデル駆動型アプリにおける setActiveProcess (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 0d4c2d8a-a2fb-4cdd-9153-041646068992
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="setactiveprocess-client-api-reference"></a>setActiveProcess (クライアント API 参照)



[!INCLUDE[./includes/setActiveProcess-description.md](./includes/setActiveProcess-description.md)]

プロセスのアクティブなインスタンスがある場合、エンティティ レコードはプロセス インスタンス ID とともに読み込まれます。 プロセスのアクティブなインスタンスがない場合、新しいプロセス インスタンスが作成され、エンティティ レコードがプロセス インスタンス ID とともに読み込まれます。 現在のプロセスの複数のインスタンスがある場合、レコードは既定値設定ロジックごとのアクティブなプロセスの最初のインスタンスとともに読み込まれ、これはユーザーごとの最近使用したプロセス インスタンスになります。

## <a name="syntax"></a>構文

`formContext.data.process.setActiveProcess(processId, callbackFunction);`

## <a name="parameter"></a>パラメーター

|Name|種類​​|必須出席者|内容|
|--|--|--|--|
|processInstanceId|String|あり|アクティブなプロセスとして設定するプロセスの ID。|
|callbackFunction|関数|No|操作が完了したときに呼び出す関数。 このコールバック関数に、操作が成功したかどうかを示すために次のいずれかの文字列値が渡されます。<br/>- **success**: 操作が成功しました。<br/>- **invalid**: processId が有効でないか、またはプロセスが有効な状態になっていません。|

### <a name="related-topics"></a>関連トピック

[getActiveProcess](getActiveProcess.md)

[setActiveProcessInstance](../setActiveProcessInstance.md)

[formContext.data.process](../../formContext-data-process.md)
 


