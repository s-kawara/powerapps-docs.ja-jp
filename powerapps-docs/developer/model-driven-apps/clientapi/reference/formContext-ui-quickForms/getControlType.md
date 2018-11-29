---
title: モデル駆動型アプリの getControlType (クライアント API 参照) | Microsoft Docs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 72d6c761-bcc7-4de6-b73f-5f2833297825
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getcontroltype-client-api-reference"></a>getControlType (クライアント API 参照)



[!INCLUDE[./includes/getControlType-description.md](./includes/getControlType-description.md)]

## <a name="syntax"></a>構文

`quickViewControl.getControlType();`

## <a name="return-value"></a>戻り値

**種類**: 文字列。

**説明**: 簡易表示コントロールの場合、メソッドは "quickform" を返します。 

簡易表示コントロールの構成コントロールでは、メソッドはコントロールの実際の分類を返します。 その他の可能な戻り値については、「[getControlType](../controls/getControlType.md)」を参照してください。

### <a name="related-topics"></a>関連トピック

[formContext.ui.quickForms](../formContext-ui-quickForms.md)