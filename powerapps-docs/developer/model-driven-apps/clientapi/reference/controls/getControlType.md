---
title: Dynamics 365 用モデル駆動型アプリの getControlType (クライアント API 参照) | MicrosoftDocs
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
# <a name="getcontroltype-client-api-reference"></a>getControlType (クライアント API 参照)



コントロールを分類する値を戻します。

## <a name="control-types-supported"></a>サポートされているコントロールの種類

すべて

## <a name="syntax"></a>構文

`getControl(arg).getControlType();`

**戻り値**:

**種類**: 文字列

|戻り値 |内容|
|--|--|
|標準|標準のコントロール|
|iframe|IFRAME コントロール|
|kbsearch|サポート情報検索コントロール|
|lookup|検索コントロール|
|multiselectoptionset|複数選択オプション セット コントロール|
|注意|メモ コントロール|
|optionset|オプション セット コントロール|
|quickform | [簡易表示](../formContext-ui-quickForms.md) コントロール|
|サブグリッド | [サブグリッド](../grids.md) コントロール|
|timercontrol | タイマー コントロール|
|timelinewall | タイムライン コントロール (統一インターフェイス用)|
|webresource | Web リソース コントロール|
|customcontrol: \<*namespace*>.\<*name*> | Dynamics 365 モバイル クライアント (電話やタブレット PC) のカスタム コントロール|
|customsubgrid:\<*namespace*>.\<*name*> | Dynamics 365 モバイル クライアント (電話やタブレット PC) のカスタム データセット コントロール|

### <a name="related-topics"></a>関連トピック

[コントロール](../controls.md)

[getControl](getcontrol.md)


