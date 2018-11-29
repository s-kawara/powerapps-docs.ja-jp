---
title: getValue (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: acc78a1e-212a-4eef-88c5-8272f9ba3009
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getvalue-client-api-reference"></a>getValue (クライアント API 参照)

属性のデータ値を取得します。

## <a name="attribute-types-supported"></a>サポートされる属性の種類

すべて

## <a name="syntax"></a>構文

`formContext.getAttribute(arg).getValue()`

## <a name="return-value"></a>戻り値

**種類**: 属性の種類によって異なります。 

| 属性の種類 | 返り値の種類| 
|----|-----|
| boolean | [Boolean](https://msdn.microsoft.com/library/t7bkhaz6.aspx) |
| datetime| [日付](https://msdn.microsoft.com/library/cd9w2te4.aspx)<br/> PowerApps ユーザー ロケール設定を使用してデータの文字列バージョンを取得するには [format](https://msdn.microsoft.com/library/bb384009.aspx) および [localeFormat](https://msdn.microsoft.com/library/bb383816.aspx) メソッドを使用します。 その他のメソッドは、ユーザーの PowerApps ロケール設定を使用する代わりに、オペレーティング システムを使用して日付の書式を設定します。 | 
| 小数| [番号](https://msdn.microsoft.com/library/dwab3ed2.aspx)| 
| Double | [番号](https://msdn.microsoft.com/library/dwab3ed2.aspx)| 
| integer | [番号](https://msdn.microsoft.com/library/dwab3ed2.aspx)|
| lookup | [Array](https://msdn.microsoft.com/library/k4h76zbx.aspx) <br/>検索オブジェクトの配列。<br/><br/>注意: 特定の検索を使用すると、\[宛先\]: 電子メール エンティティ レコードのフィールドなど、複数のレコードを検索と関連付けることができます。 したがって、1 つ以上のレコード参照を追加することを検索属性がサポートしていない場合でも、すべての検索データ値は検索オブジェクトの配列を使用します。 <br/><br/>各検索には以下のプロパティがあります。<br/>- *entityType*: 文字列。 検索に表示されているエンティティの名前です。<br/>- *id*: 文字列: 検索に表示されたコードの GUID 値を示す文字列です。<br/>- *name*: 文字列: 検索に表示するレコードを表すテキストです。|
| memo  | [文字列](https://msdn.microsoft.com/library/ecczf11c.aspx)  |
| 金額| [番号](https://msdn.microsoft.com/library/dwab3ed2.aspx)  |
| optionset | [番号](https://msdn.microsoft.com/library/dwab3ed2.aspx)  |
| 文字列 | [文字列](https://msdn.microsoft.com/library/ecczf11c.aspx) |


### <a name="related-topic"></a>関連項目
[setValue (クライアント API 参照)](setValue.md)
