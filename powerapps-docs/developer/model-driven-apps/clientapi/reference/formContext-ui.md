---
title: モデル駆動型アプリの formContext.ui (クライアント API 参照) | Microsoft Docs
description: クライアント API を使用したモデル駆動型アプリのプロセスの作業の詳細
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: f93e0e21-f911-4681-81b0-82ccf98ee28b
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="formcontextui-client-api-reference"></a>formContext.ui (クライアント API 参照)



ユーザー インターフェイス (UI) に関する情報を取得するプロパティおよびメソッド、およびフォームのいくつかのサブコンポーネントのコレクションを提供します。

![formContext UI オブジェクト モデル](../../media/ClientAPI-formContext-ui-Model.png)

## <a name="properties"></a>プロパティ​​

|Name|内容|
|--|--|
|コントロール|ページのすべてのコントロールのコレクション。 コレクションに関する詳細については、「[コレクション](collections.md)」、コレクションのコントロール オブジェクトに関する情報については、「[コレクション](controls.md)」を参照してください。|
|formSelector|formSelector.getCurrentItem メソッドを使用して、現在使用中のフォームに関する情報を取得します。 formSelector.items コレクションを使用して、ユーザーに対して使用できるすべてのフォームに関する情報を返します。 **formSelector** はタブレット PC 用 Microsoft Dynamics 365 では使用できません。|
|ナビゲーション|ページのすべてのナビゲーション アイテムのコレクション。 コレクション メソッドに関する詳細については、「[コレクション](collections.md)」、コレクションのアイテムに関する情報については、「[formContext.ui.navigation アイテム](formContext-ui-navigation.md)」を参照してください。 **ナビゲーション**はタブレット PC 用 Microsoft Dynamics 365 では使用できません。|
|プロセス|フォームの業務プロセス フローのコントロールを操作するためのオブジェクトおよびメソッドを提供します。<br/>詳細: [formContext.ui.process](formContext-ui-process.md)|
|quickForms|新しいフォームのレンダリング エンジンを使用するフォームのすべての簡易表示コントロールのコレクション(「ターボ フォーム」とも呼ばれる)。<br/>詳細: [formContext.ui quickForms](formContext-ui-quickforms.md)|
|タブ|ページのすべてのタブのコレクション。<br/>コレクション メソッドに関する詳細については、「[コレクション](collections.md)」、コレクションのアイテムに関する情報については、「[formContex.ui タブ](formContext-ui-tabs.md)」を参照してください。|


## <a name="methods"></a>メソッド 

|Name|内容|
|--|--|
|[addOnLoad](formContext-ui/addOnload.md)|[!INCLUDE[formContext-ui/includes/addOnLoad-description.md](formContext-ui/includes/addOnLoad-description.md)]|
|[clearFormNotification](formContext-ui/clearFormNotification.md)|[!INCLUDE[formContext-ui/includes/clearFormNotification-description.md](formContext-ui/includes/clearFormNotification-description.md)]|
|[close](formContext-ui/close.md)|[!INCLUDE[formContext-ui/includes/close-description.md](formContext-ui/includes/close-description.md)]|
|[getFormType](formContext-ui/getFormType.md)|[!INCLUDE[formContext-ui/includes/getFormType-description.md](formContext-ui/includes/getFormType-description.md)]|
|[getViewPortHeight](formContext-ui/getViewPortHeight.md)|[!INCLUDE[formContext-ui/includes/getViewPortHeight-description.md](formContext-ui/includes/getViewPortHeight-description.md)]|
|[getViewPortWidth](formContext-ui/getViewPortWidth.md)|[!INCLUDE[formContext-ui/includes/getViewPortWidth-description.md](formContext-ui/includes/getViewPortWidth-description.md)]|
|[refreshRibbon](formContext-ui/refreshRibbon.md)|[!INCLUDE[formContext-ui/includes/refreshRibbon-description.md](formContext-ui/includes/refreshRibbon-description.md)]|
|[removeOnLoad](formContext-ui/removeOnLoad.md)|[!INCLUDE[formContext-ui/includes/removeOnLoad-description.md](formContext-ui/includes/removeOnLoad-description.md)]|
|[setFormEntityName](formContext-ui/setFormEntityName.md)|[!INCLUDE[formContext-ui/includes/setFormEntityName-description.md](formContext-ui/includes/setFormEntityName-description.md)]|
|[setFormNotification](formContext-ui/setFormNotification.md)|[!INCLUDE[formContext-ui/includes/setFormNotification-description.md](formContext-ui/includes/setFormNotification-description.md)]|



### <a name="related-topics"></a>関連トピック

[formContext](../clientapi-form-context.md)




