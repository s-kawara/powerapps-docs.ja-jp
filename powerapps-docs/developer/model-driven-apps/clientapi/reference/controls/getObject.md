---
title: モデル駆動型アプリの getObject (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: ad68d177-3715-468e-b4af-8cf9b3c77799
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getobject-client-api-reference"></a>getObject (クライアント API 参照)



IFRAME または Web リソースを示す、フォームのオブジェクトを戻します。 

## <a name="control-types-supported"></a>サポートされているコントロールの種類

iframe、Web リソース

## <a name="syntax"></a>構文

`formContext.getControl(arg).getObject();`

## <a name="return-value"></a>戻り値

**種類**: オブジェクト

**説明**: オブジェクトはコントロールの種類によって異なります。
- IFRAME は、ドキュメント オブジェクト モデル (DOM) から [IFrame](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe) 要素を返します。
- Silverlight Web リソースは DOM から [オブジェクト](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/object) 要素を戻し、これは埋め込み Silverlight プラグインを表します。



