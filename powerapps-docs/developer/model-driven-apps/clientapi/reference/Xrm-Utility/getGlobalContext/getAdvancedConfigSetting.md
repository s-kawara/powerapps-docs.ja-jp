---
title: モデル駆動型アプリの getAdvancedConfigSetting (クライアント API 参照) | MicrosoftDocs
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
# <a name="getadvancedconfigsetting-client-api-reference"></a>getAdvancedConfigSetting (クライアント API 参照)



組織の高度な構成設定に関する情報を返します。 

## <a name="syntax"></a>構文

```JavaScript
var globalContext = Xrm.Utility.getGlobalContext();
globalContext.getAdvancedConfigSetting(setting);
```

## <a name="parameters"></a>パラメーター

|Name |種類​​ |必須出席者 |内容 |
|---|---|---|---|
|設定 |String |あり |構成設定の名前。 <br/>次の 2 つの構成設定のみがサポートされます。**"MaxChildIncidentNumber"** および **"MaxIncidentMergeNumber"** |

## <a name="return-value"></a>戻り値

高度な構成設定の値を返します。

### <a name="related-topics"></a>関連トピック

[Xrm.Utility.getGlobalContext](../getGlobalContext.md)



