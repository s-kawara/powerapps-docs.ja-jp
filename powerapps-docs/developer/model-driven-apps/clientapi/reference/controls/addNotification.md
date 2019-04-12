---
title: モデル駆動型アプリにおける addNotification (クライアント API 参照) | Microsoft Docs
ms.date: 10/31/2018
ms.service: powerapps
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 4d025f92-db16-440c-9f82-e40d71e09862
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="addnotification-client-api-reference"></a>addNotification (クライアントAPI参照)



エラー または 推奨 通知をコントロールに対して表示し、通知に基づいて実行するアクションを指定することができます。 通知のエラーの種類を指定するときは、赤の "X" アイコンはコントロールの横に表示されます。 通知の推奨の種類を指定するときは、"i" アイコンはコントロールの横に表示されます。 Dynamics 365 モバイル クライアント上でアイコンをタップすると、メッセージが表示され、**適用**ボタンをクリックするまたはメッセージを閉じることによって、設定済みのアクションを実行することができます。 

## <a name="control-types-supported"></a>サポートされているコントロールの種類

すべて

## <a name="syntax"></a>構文

`formContext.getControl(arg).addNotification(notification);`

## <a name="parameters"></a>パラメーター

<table style="width:100%">
<tr>
<th>Name</th>
<th>種類​​</th>
<th>必須出席者</th>
<th>内容</th>
</tr>
<tr>
<td>通知</td>
<td>オブジェクト</td>
<td>あり</td>
<td>追加する通知。 オブジェクトには、次の属性が含まれています。
<ul>
<li><b>操作</b>: (任意) オブジェクトの配列。 次の属性を含むオブジェクトのコレクションです:
<ul>
<li><b>メッセージ</b>: (オプション) 文字列。 ユーザーに表示される通知の本文です。 最適な結果を得るため、メッセージは 100 文字に制限します。</li>
<li><b>操作</b>: (任意) 関数の配列。 メッセージに対応するアクションです。</li>
</ul>
<li><b>メッセージ</b>: 文字列の配列。 通知で表示されるメッセージ。 現在のリリースでは、配列で指定され最初のメッセージのみが表示されます。 ここで指定する文字列は太字のテキストとして通知に表示され、通常、通知のタイトルまたは件名に使用されます。 最適な結果を得るため、メッセージは 50 文字に制限する必要があります。</li>
<li><b>notificationLevel</b>: 文字列。 通知の種類を定義します。 有効な値は、エラーまたはレコメンデーションです。</li>
<li><b>uniqueId</b>: 文字列。 <b>clearNotification</b> メソッドを使用する場合にこの通知をクリアする ID。</li>
</ul></td>
</tr>

</table>

## <a name="return-value"></a>戻り値

**種類**: ブール値

**説明**: メソッドが成功したかどうかを示します。


## <a name="remarks"></a>備考

**addNotification** メソッドには指定したメッセージと共に通知と次の 2 つの標準ボタンが表示されます: **適用**および**解除**。 **適用**をクリックすると定義するアクションが実行されます。**解除**をクリックし、通知メッセージをクローズします。 

## <a name="example"></a>例

**取引先企業名**フィールドに "Microsoft" が含まれ、株式銘柄コードが "MSFT" に設定されていない場合は、次のサンプル コードによって取引先企業フォームの**取引先企業名**フィールド上で通知が表示され、**株式銘柄コード**を設定します。 通知で**適用**をクリックすると**株式銘柄コード**フィールドは "MSFT" に設定されます。

```JavaScript
function addTickerSymbolRecommendation(executionContext) {
    var formContext = executionContext.getFormContext();
    var myControl = formContext.getControl('name');
    var accountName = formContext.data.entity.attributes.get('name');
    var tickerSymbol = formContext.data.entity.attributes.get('tickersymbol');

    if (accountName.getValue() == 'Microsoft' && tickerSymbol.getValue() != 'MSFT') {
        var actionCollection = {
            message: 'Set the Ticker Symbol to MSFT?',
            actions: null
        };

        actionCollection.actions = [function () {
            tickerSymbol.setValue('MSFT');
            myControl.clearNotification('my_unique_id');
        }];

        myControl.addNotification({
            messages: ['Set Ticker Symbol'],
            notificationLevel: 'RECOMMENDATION',
            uniqueId: 'my_unique_id',
            actions: [actionCollection]
        });
    }
    else
        console.log("Notification not set");
}
```

### <a name="related-topics"></a>関連トピック

[clearNotification](clearNotification.md)

[setNotification](setNotification.md)



