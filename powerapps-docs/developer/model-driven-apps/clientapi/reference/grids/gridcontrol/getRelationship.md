---
title: モデル駆動型アプリの getRelationship (クライアント API 参照) | Microsoft Docs
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
# <a name="getrelationship-client-api-reference"></a>getRelationship (クライアント API 参照)



[!INCLUDE[./includes/getRelationship-description.md](./includes/getRelationship-description.md)]

## <a name="grid-types-supported"></a>サポートされるグリッドの種類

読み取り専用および編集可能なグリッド

## <a name="syntax"></a>構文

`gridContext.getRelationship();`

## <a name="return-value"></a>戻り値

**種類**: オブジェクト。

**説明**: 次の属性を持つ関連付けブジェクトです。
- **attributeName**: 文字列。 属性の名前です。
- **name**: 文字列。 関係の名前。 
- **navigationPropertyName**: 文字列。 この関係のナビゲーション プロパティの名前。
- **relationshipType**: 番号。 関連付けの種類を示す次のいずれかの値を返します。
    - 0: OneToMany
    - 1: ManyToMany
- **roleType**: 番号。 関連付けのロールの種類を示す次のいずれかの値を返します。
    - 1: Referencing
    - 2: AssociationEntity

## <a name="remarks"></a>備考

`gridContext` を取得するには、「[グリッド コンテキストの取得](../../grids.md#bkmk_gridcontext)」を参照してください。

### <a name="related-topics"></a>関連トピック

[openRelatedGrid](openRelatedGrid.md)

<!-- TODO:
[Customize entity relationship metadata](../../../../customize-entity-relationship-metadata.md) -->


