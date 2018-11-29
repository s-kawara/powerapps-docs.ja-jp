---
title: getFormat (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: e5f97552-4a48-4bf9-b460-6105442e2e6b
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getformat-client-api-reference"></a>getFormat (クライアント API 参照)



属性のフォーマット オプションを表す文字列値を返します。 

## <a name="attribute-types-supported"></a>サポートされる属性の種類

すべて

## <a name="syntax"></a>構文

`formContext.getAttribute(arg).getFormat()`

## <a name="return-value"></a>戻り値

このメソッドは、次の**文字列**値のいずれかまたは "null" を返します。

- 日付
- datetime
- 期間
- 電子メール
- 言語
- なし
- 電話
- テキスト
- textarea
- tickersymbol
- timezone
- url

> [!NOTE]
> この形式情報は、一般的に、アプリケーション フィールドの形式オプションを表します。 ブール値フィールドの形式オプションは用意されていません。

次の表では、属性のスキーマの種類および書式設定の各オプションのために予期される、書式形式の文字列の値をリストします。

| アプリケーションのフィールドの種類 | 書式設定のオプション | 属性の種類 | 書式設定値|
|----------------------------|-------------------|--------------------|------------------|
| 日付と時間              | 日付のみ         | datetime           | 日付             |
| 日付と時間              | 日付と時間     | datetime           | datetime         |
| 整数               | 期間          | integer            | 期間         |
| 1 行テキスト        | 電子メール            | 文字列             | 電子メール            |
| 整数               | 言語          | optionset          | 言語         |
| 整数               | なし​​              | integer            | なし             |
| 1 行テキスト        | テキスト領域         | 文字列             | textarea         |
| 1 行テキスト        | テキスト              | 文字列             | テキスト             |
| 1 行テキスト        | 株式銘柄コード     | 文字列             | tickersymbol     |
| 1 行テキスト        | 電話番号             | 文字列             | 電話            |
| 整数               | タイム ゾーン         | optionset          | timezone         |
| 1 行テキスト        | URL               | 文字列             | url 
