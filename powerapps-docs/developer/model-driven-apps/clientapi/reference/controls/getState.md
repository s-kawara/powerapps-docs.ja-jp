---
title: モデル駆動型アプリの getState (クライアント API 参照)| MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 199d1344-351a-44ee-8c43-f6b00b85a793
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getstate-client-api-reference"></a>getState (クライアント API 参照)



タイマー コントロールの状態を返します。

このメソッドは、 [統一インターフェイス](/dynamics365/get-started/whats-new/customer-engagement/new-in-july-2017-update#unified-interface-framework-for-new-apps) でのみサポートされます。 

## <a name="control-types-supported"></a>サポートされているコントロールの種類

タイマー

## <a name="syntax"></a>構文

`formContext.getControl(arg).getState();`

## <a name="return-value"></a>戻り値

**種類**: 数値

**説明**: 次のいずれかの値を返します。

|Value | 完了状態 |
|--|--|
|1 | 設定しない|
|2 | 処理中|
|3 | 警告|
|4 | 違反しました|
|5 | 成功|
|6 | 期限切れ|
|7 | 取り消されました|
|8 | 一時停止|

### <a name="related-topics"></a>関連トピック

[コントロール](../controls.md)
