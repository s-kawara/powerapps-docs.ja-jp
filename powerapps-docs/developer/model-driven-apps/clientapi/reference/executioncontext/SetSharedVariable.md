---
title: モデル駆動型アプリにおける setSharedVariable (クライアント API 参照) | MicrosoftDocs
description: 呼び出された場所によってフォーム上のフォームまたはアイテムへの参照を返す getEventSource メソッドについて説明します。
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 702a13c1-f4ae-4de2-9e8b-95360ad9240c
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="setsharedvariable-client-api-reference"></a>setSharedVariable (クライアント API 参照)



現在のハンドラーの終了後に別のハンドラーから使用できる変数の値を設定します。

## <a name="syntax"></a>構文

`ExecutionContextObj.setSharedVariable(key, value)`

## <a name="parameters"></a>パラメーター

- **キー**: 文字列: 変数の名前
- **値**: オブジェクト。 設定する値



## <a name="return-value"></a>戻り値

**種類**: オブジェクト

**説明**: 特定の種類はオブジェクトの値によって異なります。

### <a name="related-topics"></a>関連トピック
[getSharedVariable](getSharedVariable.md)

[実行コンテキスト](../execution-context.md)





