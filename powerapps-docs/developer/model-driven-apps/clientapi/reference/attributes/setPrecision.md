---
title: モデル駆動型アプリにおける setPrecision (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 580aebec-c1d1-4e4a-8c20-ced859569fb2
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="setprecision-client-api-reference"></a>setPrecision (クライアント API 参照)



小数点以下の桁数を設定します。 

## <a name="attribute-types-supported"></a>サポートされる属性の種類

通貨、少数、倍精度浮動小数点、および整数

## <a name="syntax"></a>構文

`formContext.getAttribute(arg).setPrecision(value);`

## <a name="parameter"></a>パラメーター

 パラメーター名| 種類​​| 内容  |
| --------|-----------| -----|
|値| 数値| 小数点以下の桁数。|

### <a name="related-topics"></a>関連トピック

[getPrecision](getPrecision.md)

