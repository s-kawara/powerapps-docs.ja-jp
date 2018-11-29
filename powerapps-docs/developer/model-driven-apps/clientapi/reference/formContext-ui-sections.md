---
title: モデル駆動型アプリの formContext.ui.sections (クライアント API 参照) | Microsoft Docs
description: クライアント API を使用したモデル駆動型アプリのプロセスの作業の詳細
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: e362dfb2-cb64-49f5-b3d4-d77e813325ca
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="formcontextuisections-client-api-reference"></a>formContext.ui.sections (クライアント API 参照)



セクションには、表示方法、およびセクションを含むタブへのアクセスを管理するメソッドが含まれます。

次のコード例を使用して、セクション オブジェクト (たとえば、**sectionObj**) を取得できます。

```JavaScript
var tabObj = formContext.ui.tabs.get(arg);
var sectionObj = tabObj.sections.get(arg);
```

## <a name="properties"></a>プロパティ​​

- **コントロール**: セクション コントロールのコレクションは、セクション内のコントロールへのアクセスを提供します。 コレクションによって公開されるメソッドについては、「[コレクション (クライアント API 参照)](collections.md)」を参照してください。 このコレクションのオブジェクトによって公開されるプロパティとメソッドについては、「[コントロール (クライアント API 参照)](controls.md)」を参照してください。


## <a name="methods"></a>メソッド

|Name | 内容 |
|--|--|
|[getLabel](formcontext-ui-sections/getLabel.md)|[!INCLUDE[formcontext-ui-sections/includes/getLabel-description.md](formcontext-ui-sections/includes/getLabel-description.md)]|
|[getName](formcontext-ui-sections/getName.md)|[!INCLUDE[formcontext-ui-sections/includes/getName-description.md](formcontext-ui-sections/includes/getName-description.md)]|
|[getParent](formcontext-ui-sections/getParent.md)|[!INCLUDE[formcontext-ui-sections/includes/getParent-description.md](formcontext-ui-sections/includes/getParent-description.md)]|
|[getVisible](formcontext-ui-sections/getVisible.md)|[!INCLUDE[formcontext-ui-sections/includes/getVisible-description.md](formcontext-ui-sections/includes/getVisible-description.md)]|
|[setLabel](formcontext-ui-sections/setLabel.md)|[!INCLUDE[formcontext-ui-sections/includes/setLabel-description.md](formcontext-ui-sections/includes/setLabel-description.md)]|
|[setVisible](formcontext-ui-sections/setVisible.md)|[!INCLUDE[formcontext-ui-sections/includes/setVisible-description.md](formcontext-ui-sections/includes/setVisible-description.md)]|

### <a name="related-topics"></a>関連トピック

[formcontext.ui.tabs](formcontext-ui-tabs.md)

[formContext](../clientapi-form-context.md)