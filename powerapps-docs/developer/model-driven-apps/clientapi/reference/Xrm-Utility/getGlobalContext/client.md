---
title: モデル駆動型アプリにおける getGlobalContext.client (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 89123cde-7c66-4c7d-94e4-e287285019f8
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getglobalcontextclient-client-api-reference"></a>getGlobalContext.client (クライアント API 参照)



メソッドへのアクセスを提供して、使用されているクライアント、クライアントがサーバーに接続されているかどうか、使用されているデバイスの種類を決定します。

`var clientContext = Xrm.Utility.getGlobalContext().client`

クライアントコンテキストでは、次のメソッドを使用できます。

## <a name="getclient"></a>getClient

どのクライアントでスクリプトを実行するかを示す値を返します。 

### <a name="syntax"></a>構文

`clientContext.getClient()`

### <a name="return-value"></a>戻り値

**種類**: 文字列

**説明**: 返される可能性のある値は次のとおりです:

Value |クライアント | 
|---|---|
|Web |Web アプリケーション|
|Web |統一インターフェイス|
|Outlook |Outlook |
|携帯電話 |モバイル アプリ |

## <a name="getclientstate"></a>getClientState

クライアントの状態を示す値を返します。

### <a name="syntax"></a>構文

`clientContext.getClientState()`

### <a name="return-value"></a>戻り値

**種類**: 文字列

**説明**: 返される可能性のある値は次のとおりです:

Value |クライアント | 
|---|---|
|Online |Webアプリケーション、Outlook、モバイルアプリ、統一インターフェイス|
|オフライン |Outlook、モバイル アプリ|

## <a name="getformfactor"></a>getFormFactor

このメソッドを使用して、ユーザーが使用しているデバイスの種類に関する情報を返します。

### <a name="syntax"></a>構文

`clientContext.getFormFactor()`

### <a name="return-value"></a>戻り値

**種類**: 数値

**説明**:返される可能性のある値は次のとおりです:

Value |フォーム ファクター | 
|---|---|
|0 |不明|
|1 |デスクトップ|
|2 |タブレット |
|3 |Phone |

## <a name="isoffline"></a>isOffline

サーバーがオンラインまたはオフラインかどうかを示す情報を返します。

### <a name="syntax"></a>構文

`clientContext.isOffline()`

### <a name="return-value"></a>戻り値

**種類** :ブール値

**説明**: サーバーがオフラインの場合 **true** ; それ以外の場合 **false**。

## <a name="related-topics"></a>関連トピック

[組織の設定](organizationSettings.md)

[ユーザー設定 ](userSettings.md)

[Xrm.Utility.getGlobalContext](../getGlobalContext.md)

