---
title: モデル駆動型アプリの getVisible (クライアント API 参照)| MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 72c7ec48-1d27-499c-b56c-b7a449a347b8
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getvisible-client-api-reference"></a>getVisible (クライアント API 参照)



[!INCLUDE[./includes/getVisible-description.md](./includes/getVisible-description.md)]

>[!NOTE]
>このコントロールに含まれる**セクション**または**タブ**が表示されない場合も、このメソッドは **true** を返します。 コントロールが実際に表示可能ですることを確かめるには、含まれる要素の可視性も確認する必要があります。

## <a name="syntax"></a>構文

`quickViewControl.getVisible();`

## <a name="return-value"></a>戻り値

**種類**: ブール値。

**説明**: コントロールが可視である場合は true、それ以外の場合は false です。

### <a name="related-topics"></a>関連トピック

[setVisible](setVisible.md)

[formContext.ui.quickForms](../formContext-ui-quickForms.md)



