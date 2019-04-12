---
title: モデル駆動型アプリの close (クライアント API 参照) | Microsoft Docs
ms.date: 10/31/2018
ms.service: powerapps
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 1261a94d-4f5c-446d-8c29-a326e819696b
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="close-client-api-reference"></a>close (クライアントAPI参照) 



[!INCLUDE[./includes/close-description.md](./includes/close-description.md)]

## <a name="syntax"></a>構文

`formContext.ui.close();`

## <a name="remarks"></a>備考

HTML **Window.close** メソッドが抑制されます。 フォーム ウィンドウを閉じるには、このメソッドを使用する必要があります。 フォームに未保存の変更内容がある場合は、ウィンドウを閉じる前にユーザーに変更を保存するかどうかの確認メッセージが表示されます。

タブレット用 Microsoft Dynamics 365 では、このメソッドは、[戻る]ナビゲーションボタンの動作をまねます。

### <a name="related-topics"></a>関連トピック

[formContext.ui](../formContext-ui.md)

[formContext](../../clientapi-form-context.md)

