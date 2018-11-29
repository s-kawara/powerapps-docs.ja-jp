---
title: モデル駆動型アプリの getName (クライアント API 参照) | MicrosoftDocs
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
# <a name="getname-client-api-reference"></a>getName (クライアント API 参照)



コントロールに割り当てられた名前を返します。

>[!NOTE]
>コントロールに割り当てられた名前は、フォームが読み込まれるまで決定されません。 フォームに変更を加えると、特定のコントロールに割当てわれた名前が変更される場合があります。 

## <a name="control-types-supported"></a>サポートされているコントロールの種類

すべて

## <a name="syntax"></a>構文

`formContext.getControl(arg).getName();`

## <a name="return-value"></a>戻り値

**種類**: 文字列

**説明**: コントロールの名前。

### <a name="related-topics"></a>関連トピック

[コントロール](../controls.md)

