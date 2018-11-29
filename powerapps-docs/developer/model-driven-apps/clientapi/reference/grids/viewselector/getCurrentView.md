---
title: モデル駆動型アプリの getCurrentView (クライアント API 参照) | Microsoft Docs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 4d025f92-db16-440c-9f82-e40d71e09862
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getcurrentview-client-api-reference"></a>getCurrentView (クライアント API 参照)



[!INCLUDE[./includes/getCurrentView-description.md](./includes/getCurrentView-description.md)]

## <a name="grid-types-supported"></a>サポートされるグリッドの種類

読み取り専用グリッド

## <a name="syntax"></a>構文

`viewSelector.getCurrentView();`

## <a name="return-value"></a>戻り値

**種類**: 検索オブジェクト

**説明**: 検索オブジェクトには、次の 3 つの属性があります。

- **entityType**: 番号。 ユーザーが選択可能なビューを表す、SavedQuery (1039) または UserQuery (4230) のオブジェクトの種類コード。
- **id**: 文字列。 ユーザーが選択できるビューの ID。
- **name**: 文字列。 ユーザーが選択できるビューの名前。

## <a name="remarks"></a>備考

ビュー セレクターが表示されるようにサブグリッド コントロールが構成されていない場合、`viewSelector` オブジェクトでこのメソッドを呼び出すと、エラーがスローされます。

`viewSelector` オブジェクトを取得するには、「[ViewSelector](../viewselector.md)」を参照してください。



