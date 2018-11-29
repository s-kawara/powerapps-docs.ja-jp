---
title: モデル駆動型アプリの formContext.ui.FormSelector (クライアント API 参照) | Microsoft Docs
description: クライアント API を使用したモデル駆動型アプリのプロセスの作業の詳細
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 32e8d1d0-4093-4588-a517-2930eec34dce
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="formcontextuiformselector-client-api-reference"></a>formContext.ui.formSelector (クライアント API 参照)



**formContext.ui.formSelector** プロパティにより、フォーム アイテムを操作できます。フォーム アイテムは、ユーザーに関連付けられているセキュリティ ロールにも関連付けられているので、ユーザーに利用できるフォームを表します。 通常、フォームは 1 つしかありません。 複数のフォームが利用可能な場合、フォーム アイテムのためのメソッドを使用して、ユーザーに表示されるフォームを変更できます。

フォーム アイテムは、次のいずれかから利用できます。

- **formselector.items** コレクション: 現在のユーザーがアクセスできるすべてのフォーム アイテムのコレクション。 ユーザーのセキュリティ ロールの 1 つとの関連付けを共有するフォームだけが、このコレクションで使用できます。 例: 
 
    `formItem = formContext.ui.formSelector.items.get(arg);`

    コレクション メソッドについては、「[コレクション](collections.md)」を参照してください。
 
    >[!NOTE]
    >このコレクションは、Dynamics 365 モバイル クライアント (電話とタブレット) では使用できません。

- **formselector.getCurrentItem** メソッド: 現在表示されているフォームへの参照を返します。 フォームが一つしか存在しない場合、このメソッドは **null** を返します。 例: 
 
    `formItem = formContext.ui.formSelector.getCurrentItem();`       

## <a name="form-item-methods"></a>フォーム アイテム メソッド

上記の方法のいずれかを使用してフォーム アイテムを取得した後、次のメソッドを使用してフォーム アイテムを操作します。 

|Name|内容|
|--|--|
|[getId](formcontext-ui-formselector/getId.md)|[!INCLUDE[formcontext-ui-formselector/includes/getId-description.md](formcontext-ui-formselector/includes/getId-description.md)]|
|[getLabel](formcontext-ui-formselector/getLabel.md)|[!INCLUDE[formcontext-ui-formselector/includes/getLabel-description.md](formcontext-ui-formselector/includes/getLabel-description.md)]|
|[navigate](formcontext-ui-formselector/navigate.md)|[!INCLUDE[formcontext-ui-formselector/includes/navigate-description.md](formcontext-ui-formselector/includes/navigate-description.md)]|


