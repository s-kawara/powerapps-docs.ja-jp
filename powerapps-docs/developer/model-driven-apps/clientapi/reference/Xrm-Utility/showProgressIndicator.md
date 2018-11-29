---
title: モデル駆動型アプリの showProgressIndicator (クライアント API 参照) | Microsoft Docs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 36e17a06-e381-4efd-b3a6-62391377b613
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="showprogressindicator-client-api-reference"></a>showProgressIndicator (クライアント API 参照)



[!INCLUDE[./includes/showProgressIndicator-description.md](./includes/showProgressIndicator-description.md)]

このメソッドを後で呼び出すと、既存の進行状況ダイアログに表示されたメッセージが最新のメソッド呼び出しで指定されたメッセージに更新されます。 

>[!WARNING]
>進行状況ダイアログは、[closeProgressIndicator](closeProgressIndicator.md) メソッドを使用して閉じられるまで UI をブロックします。 したがって、このメソッドを注意して使用する必要があります。

## <a name="syntax"></a>構文

`Xrm.Utility.showProgressIndicator(message)`

## <a name="parameters"></a>パラメーター 

|Name |種類​​ |必須出席者 |内容 |
|---|---|---|---|
|メッセージ|String|あり|進行状況ダイアログに表示されるメッセージ。|



### <a name="related-topics"></a>関連トピック

[closeProgressIndicator](closeProgressIndicator.md)

[Xrm.Utility](../xrm-utility.md)  



