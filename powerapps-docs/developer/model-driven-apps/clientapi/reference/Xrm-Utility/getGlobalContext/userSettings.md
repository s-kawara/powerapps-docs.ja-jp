---
title: モデル駆動型アプリにおける getGlobalContext.userSettings (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 44296667-f1cd-49be-a300-7259bc3b41e0
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getglobalcontextusersettings-client-api-reference"></a>getGlobalContext.userSettings (クライアント API 参照)



現在のユーザー設定に関する情報を返します。

`var userSettings = Xrm.Utility.getGlobalContext().userSettings`

**userSettings** オブジェクトには以下のプロパティとメソッドがあります。

## <a name="dateformattinginfo"></a>dateFormattingInfo 

現在のユーザーの日付の書式設定情報を返します。

### <a name="syntax"></a>構文

`userSettings.dateFormattingInfo`

### <a name="return-value"></a>戻り値

**種類**: オブジェクト

**説明**: **FirstDayOfWeek**、**LongDatePattern**、**MonthDayPattern**、**TimeSeparator** などの日付の書式設定情報を持つオブジェクト。

## <a name="defaultdashboardid"></a>defaultDashboardId 

現在のユーザーの既定のダッシュボードの ID を返します。

### <a name="syntax"></a>構文

`userSettings.defaultDashboardId`

### <a name="return-value"></a>戻り値

**種類**: 文字列

**説明**: 既定のダッシュボードの ID。 

## <a name="isguidedhelpenabled"></a>isGuidedHelpEnabled 

ガイド付きヘルプが現在のユーザーに対して有効になっているかどうかを示します。

### <a name="syntax"></a>構文

`userSettings.isGuidedHelpEnabled`

### <a name="return-value"></a>戻り値

**種類**: ブール値

**説明**: 有効な場合は true、そうでない場合は false です。 

## <a name="ishighcontrastenabled"></a>isHighContrastEnabled 

ハイ コントラストが現在のユーザーに対して有効になっているかどうかを示します。

### <a name="syntax"></a>構文

`userSettings.isHighContrastEnabled`

### <a name="return-value"></a>戻り値

**種類**: ブール値

**説明**: 有効な場合は true、そうでない場合は false です。

## <a name="isrtl"></a>isRTL 

現在のユーザーの言語が右から左 (RTL) の言語かどうかを示します。

### <a name="syntax"></a>構文

`userSettings.isRTL`

### <a name="return-value"></a>戻り値

**種類**: ブール値

**説明**: RTL の場合は true、それ以外の場合は false です。

## <a name="languageid"></a>languageId 

現在のユーザーの言語 ID を返します。

### <a name="syntax"></a>構文

`userSettings.languageId`

### <a name="return-value"></a>戻り値

**種類**: 数値

**説明**: 言語 ID。

## <a name="securityroleprivileges"></a>securityRolePrivileges 

ユーザーが関連付けられているセキュリティ ロールの特権、またはユーザーが割り当てられているチームのそれぞれの GUID 値を表す文字列の配列を返します。

### <a name="syntax"></a>構文

`userSettings.securityRolePrivileges`

### <a name="return-value"></a>戻り値

**種類**: 配列

**説明**: それぞれのセキュリティ ロールの特権の GUID 値。

## <a name="securityroles"></a>securityRoles 

ユーザーが関連付けられているセキュリティ ロール、またはユーザーが割り当てられているチームのそれぞれの GUID 値を表す文字列の配列を返します。

### <a name="syntax"></a>構文

`userSettings.securityRoles`

### <a name="return-value"></a>戻り値

**種類**: 配列

**説明**: それぞれのセキュリティ ロールの GUID 値。 たとえば、次のようになります。

`["0d3dd20a-17a6-e711-a94e-000d3a1a7a9b", "ff42d20a-17a6-e711-a94e-000d3a1a7a9b"]`

## <a name="transactioncurrencyid"></a>transactionCurrencyId 

現在のユーザーの取引通貨 ID を返します。

### <a name="syntax"></a>構文

`userSettings.transactionCurrencyId`

### <a name="return-value"></a>戻り値

**種類**: 文字列

**説明**: 取引通貨の ID。

## <a name="userid"></a>userId 

現在のユーザーの **SystemUser.Id** 値の GUID を返します。

### <a name="syntax"></a>構文

`userSettings.userId`

### <a name="return-value"></a>戻り値

**種類**: 文字列

**説明**: ユーザーの ID。 たとえば、次のようになります。

`"{75B5BA27-FD41-4D45-8E3A-C8446C95F0CC}"`

## <a name="username"></a>userName 

現在のユーザー名を返します。

### <a name="syntax"></a>構文

`userSettings.userName`

### <a name="return-value"></a>戻り値

**種類**: 文字列

**説明**: 現在のユーザーの名前。

## <a name="gettimezoneoffsetminutes-method"></a>getTimeZoneOffsetMinutes メソッド

ローカル時間と標準の協定世界時 (UTC) との時差 (分単位) を返します。

### <a name="syntax"></a>構文

`userSettings.getTimeZoneOffsetMinutes()`

### <a name="return-value"></a>戻り値

**種類**: 数値

**説明**: タイム ゾーンのオフセット (分単位)。

## <a name="related-topics"></a>関連トピック

[クライアント コンテキスト](client.md)

[組織の設定](organizationSettings.md)

[Xrm.Utility.getGlobalContext](../getGlobalContext.md)

