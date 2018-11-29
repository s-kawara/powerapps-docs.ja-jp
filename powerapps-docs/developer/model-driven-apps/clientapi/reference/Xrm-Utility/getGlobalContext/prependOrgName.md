---
title: モデル駆動型アプリにおける prependOrgName (Client API リファレンス) | Microsoft Docs
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
# <a name="prependorgname-client-api-reference"></a>prependOrgName (クライアント API 参照)



現在の組織の一意の名前を文字列、通常、URL パスの前につけます。

## <a name="syntax"></a>構文

 ```JavaScript
var globalContext = Xrm.Utility.getGlobalContext();
globalContext.prependOrgName(sPath);
```

## <a name="parameters"></a>パラメーター

|Name |種類​​ |必須出席者 |内容 |
|---|---|---|---|
|sPath |String |あり |リソースへのローカル パス。 |

## <a name="return-value"></a>戻り値

**種類**: 文字列

**説明**: 次の形式で前に付けられる組織名があるパス文字列:

`"/"+ orgName + sPath`

### <a name="related-topics"></a>関連トピック

[Xrm.Utility.getGlobalContext](../getGlobalContext.md)


