---
title: モデル駆動型アプリの formContext.ui.tabs (クライアント API 参照) | Microsoft Docs
description: クライアント API を使用したモデル駆動型アプリのプロセスの作業の詳細
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 1888a882-7dfc-41a8-9bb4-d693d6046666
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="formcontextuitabs-client-api-reference"></a>formContext.ui.tabs (クライアント API 参照)



タブは、ページ上のセクションのグループです。 タブを操作するためのメソッド、およびセクションのコレクションを使用してタブ内のセクションにアクセスするためのプロパティおよびメソッドが含まれています。

次のコード例を使用して、タブ オブジェクト (たとえば、**tabObj**) を取得できます。

```JavaScript
var tabObj = formContext.ui.tabs.get(arg);
```

## <a name="properties"></a>プロパティ​​

- **セクション**: セクションのコレクションは、タブ内のセクションへのアクセスを提供します。コレクション内のセクションにアクセスするメソッドの詳細については、「[コレクション (クライアント API 参照)](collections.md)」を参照してください。 コレクションのセクション オブジェクトのプロパティとメソッドについては、「[formContext.ui section](formContext-ui-sections.md)」を参照してください。

## <a name="methods"></a>メソッド

|Name | 内容 |
|--|--|
|[addTabStateChange](formcontext-ui-tabs/addTabStateChange.md)|[!INCLUDE[formcontext-ui-tabs/includes/addTabStateChange-description.md](formcontext-ui-tabs/includes/addTabStateChange-description.md)]|
|[getDisplayState](formcontext-ui-tabs/getDisplayState.md)|[!INCLUDE[formcontext-ui-tabs/includes/getDisplayState-description.md](formcontext-ui-tabs/includes/getDisplayState-description.md)]|
|[getLabel](formcontext-ui-tabs/getLabel.md)|[!INCLUDE[formcontext-ui-tabs/includes/getLabel-description.md](formcontext-ui-tabs/includes/getLabel-description.md)]|
|[getName](formcontext-ui-tabs/getName.md)|[!INCLUDE[formcontext-ui-tabs/includes/getName-description.md](formcontext-ui-tabs/includes/getName-description.md)]|
|[getParent](formcontext-ui-tabs/getParent.md)|[!INCLUDE[formcontext-ui-tabs/includes/getParent-description.md](formcontext-ui-tabs/includes/getParent-description.md)]|
|[getVisible](formcontext-ui-tabs/getVisible.md)|[!INCLUDE[formcontext-ui-tabs/includes/getVisible-description.md](formcontext-ui-tabs/includes/getVisible-description.md)]|
|[removeTabStateChange](formcontext-ui-tabs/removeTabStateChange.md)|[!INCLUDE[formcontext-ui-tabs/includes/removeTabStateChange-description.md](formcontext-ui-tabs/includes/removeTabStateChange-description.md)]|
|[setDisplayState](formcontext-ui-tabs/setDisplayState.md)|[!INCLUDE[formcontext-ui-tabs/includes/setDisplayState-description.md](formcontext-ui-tabs/includes/setDisplayState-description.md)]|
|[setFocus](formcontext-ui-tabs/setFocus.md)|[!INCLUDE[formcontext-ui-tabs/includes/setFocus-description.md](formcontext-ui-tabs/includes/setFocus-description.md)]|
|[setLabel](formcontext-ui-tabs/setLabel.md)|[!INCLUDE[formcontext-ui-tabs/includes/setLabel-description.md](formcontext-ui-tabs/includes/setLabel-description.md)]|
|[setVisible](formcontext-ui-tabs/setVisible.md)|[!INCLUDE[formcontext-ui-tabs/includes/setVisible-description.md](formcontext-ui-tabs/includes/setVisible-description.md)]|

### <a name="related-topics"></a>関連トピック

[formcontext.ui.tabs](formcontext-ui-tabs.md)

[formContext](../clientapi-form-context.md)

