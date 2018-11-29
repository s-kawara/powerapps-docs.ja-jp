---
title: モデル駆動型アプリにおける openSearchResult (Client API リファレンス) | Microsoft Docs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 1f9169ce-cba3-4bb6-af20-f86140139cfe
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="opensearchresult-client-api-reference"></a>openSearchResult (クライアント API 参照)



結果の数を指定することによって検索コントロールの検索結果を開きます。 

## <a name="control-types-supported"></a>サポートされているコントロールの種類

サポート情報検索コントロール

## <a name="syntax"></a>構文

```
var kbSearchControl = formContext.getControl("<name>");
var openResultStatus = kbSearchControl.openSearchResult(resultNumber, mode);
```

## <a name="parameter"></a>パラメーター

|Name|種類​​|必須出席者|内容|
|--|--|--|--|
|resultNumber|数値|あり|開く結果の数を指定する数値。 結果の数は 1 から始まります。|
|モード|String|No|「インライン」または「ポップアウト」を指定します。 引数の値を指定しない場合、既定 ("インライン") のオプションが使用されます。<br/><br/>"インライン" モードは、参照パネルの場合の参照パネル タブまたはコントロールの閲覧ウィンドウのいずれかで結果インラインを開きます。 "ポップアウト" モードはポップアップ ウィンドウで結果を開きます。|

## <a name="return-value"></a>戻り値

**種類:** ブール値

**説明**: 指定した検索結果の開始の状態。 成功の場合には 1 を返し、失敗の場合には 0 を返します。 メソッドが -1 を返すのは、指定された resultNumber 値が存在しない場合、または指定されたモード値が無効な場合です。