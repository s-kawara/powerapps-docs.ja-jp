---
title: モデル駆動型アプリの formContext.ui.quickForms (クライアント API 参照) | Microsoft Docs
description: クライアント API を使用したモデル駆動型アプリのプロセスの作業の詳細
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: a04043de-3497-433a-ae73-4101806dd931
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="formcontextuiquickforms-client-api-reference"></a>formContext.ui.quickForms (クライアント API 参照)



新しいフォーム レンダリング エンジン (「ターボフォーム」とも呼ばれます) を使用するときに、モデル駆動型アプリ上のすべての簡易表示コントロールおよびスタッフ コントロールにアクセスするためのメソッドを提供します。 簡易表示コントロールは、モデル駆動型アプリのメイン フォームに追加される簡易表示フォームで、メイン フォーム内の関連エンティティ レコードに関する情報を表示することができます。 簡易表示コントロールの構成コントロールでは編集できません。

**quickForms** コレクションは、フォーム上のすべての簡易表示コントロールへのアクセスを提供し、コレクションのすべての標準メソッドをサポートします。 コレクション メソッドについては、「[コレクション](collections.md)」を参照してください。 

簡易表示コントロール インスタンスのインデックス値 (整数) または名前 (文字列) を引数として指定して、[get](collections/get.md) メソッドを使用することで、**quickForms** コレクションの簡易表示コントロールを取得できます。

`quickViewControl = formContext.ui.quickForms.get(arg)`


## <a name="quick-form-control-methods"></a>簡易入力フォーム コントロールのメソッド

|Name|内容|
|--|--|
|[getControl](formcontext-ui-quickForms/getControlType.md)|[!INCLUDE[formcontext-ui-quickForms/includes/getControl-description.md](formcontext-ui-quickForms/includes/getControl-description.md)]|
|[getControlType](formcontext-ui-quickForms/getControlType.md)|[!INCLUDE[formcontext-ui-quickForms/includes/getControlType-description.md](formcontext-ui-quickForms/includes/getControlType-description.md)]|
|[getDisabled](formcontext-ui-quickForms/getDisabled.md)|[!INCLUDE[formcontext-ui-quickForms/includes/getDisabled-description.md](formcontext-ui-quickForms/includes/getDisabled-description.md)]|
|[getLabel](formcontext-ui-quickForms/getLabel.md)|[!INCLUDE[formcontext-ui-quickForms/includes/getLabel-description.md](formcontext-ui-quickForms/includes/getLabel-description.md)]|
|[getName](formcontext-ui-quickForms/getName.md)|[!INCLUDE[formcontext-ui-quickForms/includes/getName-description.md](formcontext-ui-quickForms/includes/getName-description.md)]|
|[getParent](formcontext-ui-quickForms/getParent.md)|[!INCLUDE[formcontext-ui-quickForms/includes/getParent-description.md](formcontext-ui-quickForms/includes/getParent-description.md)]|
|[getVisible](formcontext-ui-quickForms/getVisible.md)|[!INCLUDE[formcontext-ui-quickForms/includes/getVisible-description.md](formcontext-ui-quickForms/includes/getVisible-description.md)]|
|[isLoaded](formcontext-ui-quickForms/isLoaded.md)|[!INCLUDE[formcontext-ui-quickForms/includes/isLoaded-description.md](formcontext-ui-quickForms/includes/isLoaded-description.md)]|
|[最新の情報に更新](formcontext-ui-quickForms/refresh.md)|[!INCLUDE[formcontext-ui-quickForms/includes/refresh-description.md](formcontext-ui-quickForms/includes/refresh-description.md)]|
|[setDisabled](formcontext-ui-quickForms/setDisabled.md)|[!INCLUDE[formcontext-ui-quickForms/includes/setDisabled-description.md](formcontext-ui-quickForms/includes/setDisabled-description.md)]|
|[setFocus](formcontext-ui-quickForms/setFocus.md)|[!INCLUDE[formcontext-ui-quickForms/includes/setFocus-description.md](formcontext-ui-quickForms/includes/setFocus-description.md)]|
|[setLabel](formcontext-ui-quickForms/setLabel.md)|[!INCLUDE[formcontext-ui-quickForms/includes/setLabel-description.md](formcontext-ui-quickForms/includes/setLabel-description.md)]|
|[setVisible](formcontext-ui-quickForms/setVisible.md)|[!INCLUDE[formcontext-ui-quickForms/includes/setVisible-description.md](formcontext-ui-quickForms/includes/setVisible-description.md)]|


### <a name="related-topics"></a>関連トピック

[formContext.ui](formContext-ui.md)