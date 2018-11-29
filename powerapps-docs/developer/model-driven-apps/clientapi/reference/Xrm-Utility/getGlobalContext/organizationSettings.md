---
title: モデル駆動型アプリにおける getGlobalContext.organizationSettings (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: badf4f82-cb47-4864-aa43-bb777d04de4d
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getglobalcontextorganizationsettings-client-api-reference"></a>getGlobalContext.organizationSettings (クライアント API 参照)



現在の組織の設定に関する情報を返します。 

`var organizationSettings = Xrm.Utility.getGlobalContext().organizationSettings`

**organizationSettings** オブジェクトには以下のプロパティがあります。

## <a name="attributes"></a>属性

組織エンティティに使用可能な `key:value` のペアとして属性およびその値を返します。 追加の値は、Web リソースの依存関係リストで属性の依存関係として指定されている場合には、属性として使用できます。 `key` は属性の論理名になります。

### <a name="syntax"></a>構文

`organizationSettings.attributes`

### <a name="return-value"></a>戻り値

**種類**: オブジェクト

**説明**: 属性とその値があるオブジェクト。

## <a name="basecurrencyid"></a>baseCurrencyId 

現在の組織の基本通貨の ID を返します。

### <a name="syntax"></a>構文

`organizationSettings.baseCurrencyId`

### <a name="return-value"></a>戻り値

**種類**: 文字列

**説明**: 基本通貨の ID。

## <a name="defaultcountrycode"></a>defaultCountryCode 

現在の組織の電話番号の、既定の国/地域コードを返します。

### <a name="syntax"></a>構文

`organizationSettings.defaultCountryCode`

### <a name="return-value"></a>戻り値

**種類**: 文字列

**説明**: 電話番号の既定の国/地域コード。

## <a name="isautosaveenabled"></a>isAutoSaveEnabled 

現在の組織に対して自動保存オプションを有効にするかどうかを示します。

### <a name="syntax"></a>構文

`organizationSettings.isAutoSaveEnabled`

### <a name="return-value"></a>戻り値

**種類:** ブール値

**説明**: 有効な場合は **true**、そうでない場合は **false** です。

## <a name="languageid"></a>languageId 

現在の組織の優先する言語 ID を返します。

### <a name="syntax"></a>構文

`organizationSettings.languageId`

### <a name="return-value"></a>戻り値

**種類**: 数値

**説明**: 優先する言語 ID。 たとえば、次のようになります。

`1033`

## <a name="organizationid"></a>organizationId 

現在の組織の ID を返します。

### <a name="syntax"></a>構文

`organizationSettings.organizationId`

### <a name="return-value"></a>戻り値

**種類**: 文字列

**説明**: 現在の組織の ID。

## <a name="uniquename"></a>uniqueName 

現在の組織の固有名を返します。

### <a name="syntax"></a>構文

`organizationSettings.uniqueName`

### <a name="return-value"></a>戻り値

**種類**: 文字列

**説明**: 現在の組織の固有名。

## <a name="useskypeprotocol"></a>useSkypeProtocol 

Skype プロトコルが現在の組織に対して使用されているかどうかを示します。

### <a name="syntax"></a>構文

`organizationSettings.useSkypeProtocol`

### <a name="return-value"></a>戻り値

**種類:** ブール値

**説明**: Skype プロトコルが使用されている場合は **true**、そうでない場合は **false** です。


## <a name="related-topics"></a>関連トピック

[クライアント コンテキスト](client.md)

[ユーザー設定](userSettings.md)

[Xrm.Utility.getGlobalContext](../getGlobalContext.md)