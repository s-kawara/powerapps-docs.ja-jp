---
title: モデル駆動型アプリにおける moveNext (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 97640c6a-816b-4d18-9b0b-e79411787c1a
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="movenext-client-api-reference"></a>moveNext (クライアント API 参照)



[!INCLUDE[./includes/moveNext-description.md](./includes/moveNext-description.md)]

別のエンティティ内の次のステージに移動することもできます。 

## <a name="syntax"></a>構文

`formContext.data.process.moveNext(callbackFunction);`

## <a name="parameters"></a>パラメーター

<table style="width:100%">
<tr>
<th>Name</th>
<th>種類​​</th>
<th>必須出席者</th>
<th>内容</th>
</tr>
<tr>
<td>callbackFunction</td>
<td>関数</td>
<td>No</td>
<td>操作が完了したときに呼び出す関数。 このコールバック関数には、操作の状態を示すために次のいずれかの文字列値が渡されます。
<table>
<tr>
<th>Value</th>
<th>理由</th>
</tr>
<tr>
<td>成功</td>
<td>操作が成功しました。</td>
</tr>
<tr>
<td>crossEntity</td>
<td>次のステージは別のエンティティ用です。</td>
</tr>
<tr>
<td>end</td>
<td>アクティブ ステージはアクティブ パスの最後のステージです。</td>
</tr>
<tr>
<td>invalid</td>
<td>選択したステージがアクティブ ステージと同じではないため、操作が失敗しました。</td>
</tr>
<tr>
<td>dirtyForm</td>
<td>この値は、ページ内のデータが保存されない場合に返されます。</td>
</tr>
</table>
</td>
</tr>
</table>

>[!IMPORTANT]
>このメソッドを使用できるのは、選択したステージとアクティブ ステージが同じである場合のみです。 [OnStageChange](../../events/onstagechange.md) イベントからコードが起動されるときは、現在のステージが選択されます。 コードが [OnStageSelected](../../events/onstageselected.md) イベントから起動されるときは、[getActiveStage](../activestage/getActiveStage.md) メソッドを使用して、選択したステージがアクティブなステージであるかも確認する必要があります。 その他すべてのフォーム イベントでは、どのステージが現在選択されているかを判断することはできません。 最善の結果を得るには、[OnStageChange](../../events/onstagechange.md) イベントと [OnStageSelected](../../events/onstageselected.md) イベントによって起動される関数で呼び出されるコードでのみ、このメソッドを使用する必要があります。

## <a name="remarks"></a>備考

このメソッドは、[OnStageChange](../../events/onstagechange.md) イベントを発生します。

### <a name="related-topics"></a>関連トピック

[movePrevious](movePrevious.md)

[formContext.data.process](../../formContext-data-process.md)
 


