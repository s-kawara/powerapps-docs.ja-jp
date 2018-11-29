---
title: モデル駆動型アプリの openUrl (Client API reference)| MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 29cb3685-21aa-42fc-8e84-0074dcc69197
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="openurl-client-api-reference"></a>openUrl (クライアント API 参照)



[!INCLUDE[./includes/openUrl-description.md](./includes/openUrl-description.md)]

## <a name="syntax"></a>構文

`Xrm.Navigation.openUrl(url,openUrlOptions)`

## <a name="parameters"></a>パラメーター

|Name |種類​​ |必須出席者 |内容 |
|---|---|---|---|
|url|String|あり|開く URL。|
|openUrlOptions|オブジェクト|No|URL を開くためのオプション。オブジェクトには次の属性が含まれます。<br/>- **height**: (任意) 数値。 結果ページに表示されるウィンドウの高さです (単位はピクセル)。<br/>- **width**: (任意) 数値。 結果ページに表示されるウィンドウの幅です (単位はピクセル)。|

## <a name="remarks"></a>備考

このメソッドは、モバイル クライアントがシム以外のブラウザーで URL を開く場合に特に役立ちます。

 ### <a name="related-topics"></a>関連トピック

[Xrm.Navigation](../xrm-navigation.md)

