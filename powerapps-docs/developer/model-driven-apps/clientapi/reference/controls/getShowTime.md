---
title: モデル駆動型アプリの getShowTime (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 43341b96-ca2c-4c7e-b6d5-fe7a5fd3c8b2
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getshowtime-client-api-reference"></a>getShowTime (クライアント API 参照)



日付コントロールに日付の時刻の部分が表示されているかどうかを取得します。 

## <a name="control-types-supported"></a>サポートされているコントロールの種類

**datetime** 属性の標準コントロール。

## <a name="syntax"></a>構文

`formContext.getControl(arg).getShowTime();`

## <a name="return-value"></a>戻り値

**種類:** ブール値

**説明**: 日付の時刻の部分を表示する場合は true、それ以外の場合は false。

### <a name="related-topics"></a>関連トピック

[setShowTime](setShowTime.md)

