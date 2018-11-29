---
title: モデル駆動型アプリにおける save (Client API リファレンス) | Microsoft Docs
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
# <a name="save-client-api-reference"></a>save (クライアント API 参照)



[!INCLUDE[./includes/save-description.md](./includes/save-description.md)]

予定、定期的な予定、またはサービス活動に関連するレコードの処理方法を制御するオブジェクトを設定することもできます。

## <a name="syntax"></a>構文

`formContext.data.save(saveOptions).then(successCallback, errorCallback);`

## <a name="parameters"></a>パラメーター

|Name|種類​​|必須出席者|内容|
|--|--|--|--|
|saveOptions|オブジェクト|No|レコードを保存するオプションを指定するオブジェクト。  オブジェクトには、次の属性があります。<br/><br/>- **saveMode**: (任意) 数値。 保存イベントがどのように開始されたかを示す値を指定します。 サポートされるメッセージの一覧については、「[getSaveMode](../save-event-arguments/getsavemode.md) メソッドの戻り値」を参照してください。 **saveMode** を設定しても、対応するアクションは実行されません。保存操作の理由に関する情報が **OnSave** イベント ハンドラーに提供されます。<br/><br/>- **useSchedulingEngine**: (任意) ブール値。 **Create** または **Update** メッセージではなく、**Book** または **Reschedule** メッセージを使用するかどうかを示します。 このオプションは、予定、定期的な予定、またはサービス活動レコードに対して使用される場合にのみ適用されます。|
|successCallback|関数|No|処理が成功したときに呼び出す関数。|
|errorCallback|関数|無効化しない|処理が失敗したときに呼び出す関数。 次のプロパティを持つオブジェクトが渡されます。<br/><br/>- **errorCode**: 数値。 エラー コード。<br/><br/>- **message**: 文字列。 ローカライズされたエラー メッセージ。|


### <a name="related-topics"></a>関連トピック

[formContext.data.entity.save](../formContext-data-entity/save.md)

[formContext](../../clientapi-form-context.md)

