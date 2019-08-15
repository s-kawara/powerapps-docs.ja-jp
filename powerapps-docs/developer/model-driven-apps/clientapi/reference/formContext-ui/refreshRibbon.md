---
title: モデル駆動型アプリにおける refreshRibbon (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: powerapps
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: dbd43d7b-c9b0-4ca5-943d-dd813d3bb049
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="refreshribbon-client-api-reference"></a>refreshRibbon (クライアント API 参照)



[!INCLUDE[./includes/refreshRibbon-description.md](./includes/refreshRibbon-description.md)]

## <a name="syntax"></a>構文

`formContext.ui.refreshRibbon(refreshAll);`

## <a name="parameter"></a>パラメーター

|Name|種類​​|必須出席者|内容|
|--|--|--|--|
|refreshAll|Boolean|No|現在のページのすべてのリボンのコマンド バーを更新するかどうかを示します。 **false** を指定する場合、ページ レベルのリボン コマンド バーのみが更新されます。 このパラメーターを指定しない場合、既定で **false** が渡されます。|

## <a name="remarks"></a>備考

 この機能は一般に、リボン `<EnableRule>` (RibbonDiffXml) がフォーム内の値に依存しているときに使用されます。 コードがルールによって使用される値を変更した後は、このメソッドを使用して、このルールが適用されるようにリボンがフォームのデータを再評価するようにします。

### <a name="related-topics"></a>関連トピック

[formContext.ui](../formContext-ui.md)

[formContext](../../clientapi-form-context.md)

