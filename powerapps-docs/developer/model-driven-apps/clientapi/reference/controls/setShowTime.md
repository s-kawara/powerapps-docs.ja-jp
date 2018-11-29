---
title: モデル駆動型アプリにおける setShowTime (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 77999c82-3d6a-4db9-af9c-7322491768d9
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="setshowtime-client-api-reference"></a>setShowTime (クライアント API 参照)



日付コントロールで日付の時間の部分を表示するかどうかを指定します。 

## <a name="control-types-supported"></a>サポートされているコントロールの種類

**datetime** 属性の標準コントロール。

## <a name="syntax"></a>構文

`formContext.getControl(arg).setShowTime(bool);`

## <a name="parameter"></a>パラメーター

|Name|種類​​|必須出席者|内容|
|--|--|--|--|
|bool|Boolean|あり|日付の時刻の部分を表示する場合は true、それ以外の場合は false を指定します。|

## <a name="remarks"></a>備考

このメソッドは、属性で **DateAndTime** 形式が使用されている日付コントロールの時刻コンポーネントを表示または非表示にします。 このメソッドは、**DateOnly** 形式が使用されている場合は無効です。

### <a name="related-topics"></a>関連トピック

[getShowTime](getShowTime.md)

