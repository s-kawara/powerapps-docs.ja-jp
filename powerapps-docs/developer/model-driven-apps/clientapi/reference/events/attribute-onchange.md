---
title: モデル駆動型アプリにおける属性 OnChange イベント | Microsoft Docs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 89123cde-7c66-4c7d-94e4-e287285019f8
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="attribute-onchange-event-client-api-reference"></a>属性 OnChange イベント (クライアント API 参照)



`OnChange` イベントは、以下の状況で発生します:
- フォーム フィールドのデータが変更され、フォーカスが失われます。 ラジオ ボタンまたはチェック ボックスを使用するように設定される、2 つのオプション (ブール値) に適用される、この動作の例外があります。 これらの場合、イベントは、ただちに実行されます。
- レコードの保存後などの、フォームのリフレッシュ時に、サーバー上のデータの変更は取得されてフィールドを更新します。
- 属性。[fireOnchange](../attributes/fireOnChange.md) メソッドが使用されます。

すべてのフィールドは、`OnChange`イベントはをサポートしています。 フィールドのデータは、`OnChange` イベントの前後に検証されます。

`OnChange` イベントは、属性 [setValue](../attributes/setValue.md) メソッドを使用してプログラム的にフィールドが変更される場合も発生しません。 値を設定したあとに `OnChange` イベントのイベント ハンドラーを実行したい場合、コードで `formContext.data.entity attribute.`[fireOnchange](../attributes/fireOnChange.md) メソッドを使用する必要があります。 

> [!NOTE]
> **ステータス**フィールドは `OnChange` イベントをサポートしますが、フィールドはフォームでは読み取り専用で、イベントはユーザーとの対話では発生しません。 別のスクリプトは、フィールドで [fireOnchange](../attributes/fireOnChange.md) メソッドを使用してこのイベントを発生させる場合があります。

## <a name="methods-supported-for-this-event"></a>このイベントをサポートする方法
属性の `OnChange` イベントを操作できる次の 3 つのメソッドがあります。
- [addOnChange](../attributes/addOnChange.md)
- [fireOnChange](../attributes/fireOnChange.md)
- [removeOnChange](../attributes/removeOnChange.md)

### <a name="related-topics"></a>関連トピック
[属性 (クライアントAPI参照) ](../attributes.md)
 



