---
title: モデル駆動型アプリの getSaveMode (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 03e970ee-7ed3-4df2-9670-222d76a479fd
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getsavemode-client-api-reference"></a>getSaveMode (クライアント API 参照)



[!INCLUDE[./includes/getSaveMode-description.md](./includes/getSaveMode-description.md)]

## <a name="syntax"></a>構文

`executionContext.getEventArgs().getSaveMode()`

## <a name="return-value"></a>戻り値

**種類**: 数値

**説明**: 次の表は、エンティティ レコードがユーザーによって保存されたさまざまな方法を検出するのに返される、サポートされている値を示しています。

|Value |保存モード |Entity|
|---|---|---|
|1|上書き保存​​|すべて|
|2|保存して閉じる|すべて|
|5|非アクティブ化します|すべて|
|6|再アクティブ化|すべて|
|7|送信​​|電子メールの送信|
|15|見込みなしと評価|リード​​|
|16|見込みありと評価|リード​​|
|47|割り当て​​|ユーザーまたはチームが所有するエンティティ|
|58|進捗状況を終了にして保存|活動 |
|59|保存して新規作成|すべて|
|70|自動保存|すべて|

## <a name="remarks"></a>備考

このメソッドは、組織のほとんどのフォームに自動保存を有効化し、特定のフォームでは無効にする場合に重要です。  

## <a name="example"></a>例

渡された実行コンテキストと共に **OnSave** イベントに登録されている次のコードは、ユーザーが自ら実行する保存は自動保存されないようにしますが、他のすべては許可します。 自動保存が有効にされると、フォームから移動すると**保存して閉じる**ことになります。 このコードは、30秒タイマーによって開始された保存、ユーザーがフォームから移動する際に保存していないデータを保存するのを防ぎます。

```JavaScript
function preventAutoSave(executionContext) {
    var eventArgs = executionContext.getEventArgs();
    if (eventArgs.getSaveMode() == 70 || eventArgs.getSaveMode() == 2) {
        eventArgs.preventDefault();
    }
}
```

レコードを保存するには、フォームの下部の**保存**アイコンか、コマンド バーに追加するカスタム**保存**コマンドをクリックする必要があります。

### <a name="related-topics"></a>関連トピック

[isDefaultPrevented](isDefaultPrevented.md)

[preventDefault](preventDefault.md)

