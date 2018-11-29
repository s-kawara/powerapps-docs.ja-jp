---
title: モデル駆動型アプリの getControl (クライアント API リファレンス) | Microsoft Docs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 34715e1f-35c0-4b7f-971e-e0a6518f0722
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getcontrol-client-api-reference"></a>getControl (クライアント API 参照)



フォーム上のコントロールを取得します。 

## <a name="syntax"></a>構文

`formContext.getControl(arg);`

**formContext.getControl(引数)** メソッドは、**formContext.ui.controls.get** にアクセスするためのショートカット メソッドです。

## <a name="parameter"></a>パラメーター

**引数**: オプション。 フォーム上のコントロールの**名前**または**インデックス値**のいずれかとして引数を渡すことで、フォーム上のコンとロールにアクセスできます。 たとえば、`formContext.getControl("firstname")` や `formContext.getControl(0)` などです。


## <a name="return-value"></a>戻り値

**種類**: オブジェクトまたはオブジェクト コレクション。

**説明** : パラメーターを指定してメソッドを使用する場合はオブジェクトであり、パラメーターなしでメソッドを使用する場合はオブジェクト コレクションです。



### <a name="related-topics"></a>関連トピック

[formContext](../../clientapi-form-Context.md)



