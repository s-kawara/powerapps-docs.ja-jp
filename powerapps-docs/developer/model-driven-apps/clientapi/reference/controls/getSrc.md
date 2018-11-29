---
title: モデル駆動型アプリの getSrc (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: e003d21f-393a-4681-a6fc-256949167fcc
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getsrc-client-api-reference"></a>getSrc (クライアント API 参照)



IFRAME または Web リソースに表示されている、現在の URL が返されます。 

## <a name="control-types-supported"></a>サポートされているコントロールの種類

iframe、Web リソース

## <a name="syntax"></a>構文

`formContext.getControl(arg).getSrc();`

## <a name="return-value"></a>戻り値

**種類**: 文字列

**説明**: IFRAME または Web リソースの **src** プロパティを表す URL。

### <a name="related-topics"></a>関連トピック

[setSrc](setSrc.md)

