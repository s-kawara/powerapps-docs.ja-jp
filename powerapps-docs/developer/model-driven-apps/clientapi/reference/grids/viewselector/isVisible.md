---
title: モデル駆動型アプリにおける isVisible (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: d22cd046-064c-47ef-9e46-5cc4c8b6e280
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="isvisible-client-api-reference"></a>isVisible (クライアント API 参照)



[!INCLUDE[./includes/isVisible-description.md](./includes/isVisible-description.md)]

## <a name="grid-types-supported"></a>サポートされるグリッドの種類

読み取り専用グリッド

## <a name="syntax"></a>構文

`viewSelector.isVisible();`

## <a name="return-value"></a>戻り値

**種類**: ブール値

**説明**: 有効な場合は true、そうでない場合は false です。

## <a name="remarks"></a>備考

ビュー セレクターが表示されるようにサブグリッド コントロールが構成されていない場合、GridControl.getViewSelector メソッドによって返される **ViewSelector** でこのメソッドを呼び出すと、エラーがスローされます。

`viewSelector` オブジェクトを取得するには、「[ViewSelector](../viewselector.md)」を参照してください。



