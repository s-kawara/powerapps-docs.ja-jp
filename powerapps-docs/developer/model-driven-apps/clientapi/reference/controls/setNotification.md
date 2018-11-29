---
title: モデル駆動型アプリの setNotification (クライアント API 参照) | Microsoft Docs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 4d025f92-db16-440c-9f82-e40d71e09862
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="setnotification-client-api-reference"></a>setNotification (クライアント API 参照)



データが無効であることを示すコントロールのエラー メッセージを表示します。 このメソッドを使用するとき、赤い "X" アイコンがコントロールの隣に表示されます。 Dynamics 365 モバイル クライアント上でアイコンをタップするとメッセージが表示されます。 

## <a name="control-types-supported"></a>サポートされているコントロールの種類

すべて

## <a name="syntax"></a>構文

`formContext.getControl(arg).setNotification(message,uniqueId);`

## <a name="parameters"></a>パラメーター

|Name | 種類​​ | 必須出席者 | 内容|
|--|--|--|--|
|メッセージ |String |あり|表示するメッセージ。| 
|uniqueId |String |No|**clearNotification** メソッドを使用する場合にこのメッセージをクリアする ID。
| | |

## <a name="return-value"></a>戻り値
**種類**: ブール値 

**説明**: メソッドが成功したかどうかを示します。

## <a name="remarks"></a>備考

コントロールにエラー通知を設定すると、フォームの保存がブロックされます。

### <a name="related-topics"></a>関連トピック

[addNotification](addNotification.md)

[clearNotification](clearNotification.md)