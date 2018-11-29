---
title: setValue (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 1324b465-6012-47d4-bf35-837df82014cb
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="setvalue-client-api-reference"></a>setValue (クライアント API 参照)

属性のデータ値を設定します。 

## <a name="attribute-types-supported"></a>サポートされる属性の種類

すべて

## <a name="syntax"></a>構文

`formContext.getAttribute(arg).setValue(value)`

# <a name="parameters"></a>パラメーター
属性の種類によって異なります。

<!-- TODO: 

Change type links from msdn to docs, i.e. https://msdn.microsoft.com/library/dwab3ed2.aspx to /scripting/javascript/reference/number-object-javascript 

or MDN https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number
-->

| 属性の種類|パラメーターの種類|
-------|------|
| boolean| [Boolean](https://msdn.microsoft.com/library/t7bkhaz6.aspx) |
| datetime|[日付](https://msdn.microsoft.com/library/cd9w2te4.aspx)|
| 小数| [番号](https://msdn.microsoft.com/library/dwab3ed2.aspx)|
| double| [番号](https://msdn.microsoft.com/library/dwab3ed2.aspx) |
| Integer|[番号](https://msdn.microsoft.com/library/dwab3ed2.aspx)|
| lookup  | [配列](https://msdn.microsoft.com/library/k4h76zbx.aspx) 検索オブジェクトの配列。 <br/><br/>「関係者リスト」検索と呼ばれる特定の検索を使用すると、**宛先:** 電子メール エンティティ レコードのフィールドなど、複数のレコードを検索と関連付けることができます。 したがって、1 つ以上のレコード参照を追加することを検索属性がサポートしていない場合でも、すべての検索データ値は検索オブジェクトの配列を使用します。<br/><br/>各検索には以下のプロパティがあります。<br/>- *entityType*: 文字列。 検索に表示されているエンティティの名前です。<br/>- *id*: 文字列: 検索に表示されたコードの GUID 値を示す文字列です。 値は、{XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX} の形式と一致する必要があります。<br/>- *name*: 文字列: 検索に表示するレコードを表すテキストです。|
| memo  | [文字列](https://msdn.microsoft.com/library/ecczf11c.aspx)  |
| 金額| [番号](https://msdn.microsoft.com/library/dwab3ed2.aspx)  |
| optionset | [番号](https://msdn.microsoft.com/library/dwab3ed2.aspx)  |
| 文字列 | [文字列](https://msdn.microsoft.com/library/ecczf11c.aspx)|
| memo | [文字列](https://msdn.microsoft.com/library/ecczf11c.aspx)|
| 金額|[番号](https://msdn.microsoft.com/library/dwab3ed2.aspx)|
| optionset、multiselectoptionset|[番号](https://msdn.microsoft.com/library/dwab3ed2.aspx)<br/><br/>[getOptions](getOptions.md) メソッドはオプション値を文字列として返します。 これらの値を使用してオプション セット属性の値を設定する前に、[parseInt](https://msdn.microsoft.com/library/x53yedee.aspx) を使用して、これらを数値に変換する必要があります。 statuscode (ステータスの理由) オプションはレコードの現在の状態コードにより異なります。 statecode (ステータス) フィールドはフォーム スクリプトで設定できません。 どの statecode 値が有効であるかを理解するため、属性のメタデータを参照してください。 <!-- See [Default status and status reason values](../../../customize/default-status-and-status-reason-values.md) for a list of default values for system entities. -->ユーザー定義エンティティの場合、エンティティ メタデータ ブラウザーを使用します。 最後に、フィールドに適用済みのカスタム状態の遷移を検討してください。 詳細: [ステータスの遷移の定義](/dynamics365/customer-engagement/customize/define-status-reason-transitions)。| 
| String| [文字列](https://msdn.microsoft.com/library/ecczf11c.aspx) <br/><br/> 電子メール形式の文字列フィールドでは、有効な電子メール アドレスを示す文字列が必要です。|


> [!NOTE]
> **setValue** を使用して属性を更新しても、**OnChange** イベント ハンドラーは実行されません。 **OnChange** イベント ハンドラーを実行するには、**setValue** に加えて [fireOnChange](../attributes/fireOnChange.md) を使用する必要があります。 <br/><br/>
タブレット用 Microsoft モデル駆動型アプリがサーバーに接続されていないときは、**setValue** が使用できません。<br/><br/>合成属性の値は設定できません。 詳細: [複合属性のスクリプトを記述する](../composite-attributes.md)。

### <a name="related-topic"></a>関連項目
[getValue (クライアント API 参照)](getValue.md)
