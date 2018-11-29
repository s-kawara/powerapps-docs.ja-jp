---
title: モデル駆動型アプリの getFormType (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 6c57db71-a76d-404c-852e-9c36a1c549ee
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getformtype-client-api-reference"></a>getFormType (クライアント API 参照)



[!INCLUDE[./includes/getFormType-description.md](./includes/getFormType-description.md)]

## <a name="syntax"></a>構文

`formContext.ui.getFormType();`

## <a name="return-value"></a>戻り値

**種類**: 数値

**説明**: フォームの種類。 次のいずれかの値を返します。 

|Value |フォームの種類 |
|---|---|
|0|未定義|
|1|作成​​|
|2|更新プログラム|
|3|読み取り専用|
|4|無効化|
|6|一括編集|

>[!NOTE]
>簡易作成フォームは 1 を返します。


### <a name="related-topics"></a>関連トピック

[formContext.ui](../formContext-ui.md)

[formContext](../../clientapi-form-context.md)

