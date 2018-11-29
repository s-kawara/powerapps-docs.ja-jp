---
title: setSubmitMode (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: d0728377-4365-4571-97af-9b99b2a39b65
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="setsubmitmode-client-api-reference"></a>setSubmitMode (クライアント API 参照)



レコードを保存する際に属性からデータが送信されるかどうか設定します。 

## <a name="attribute-types-supported"></a>サポートされる属性の種類

すべて

## <a name="syntax"></a>構文

`formContext.getAttribute(arg).setSubmitMode(mode)`

## <a name="parameters"></a>パラメーター

**種類**: 文字列。 

**説明**: 次のいずれかのモードの値を設定します。
- **always**: データは保存時に常に送信されます。
- **never**: データは保存時に送信されません。 これが使用されるとき、この属性のフォーム内のフィールは編集できません。
- **dirty**: 既定の動作。 データの変更時に保存されて送信されます。
 
## <a name="remarks"></a>備考
このメソッドを使用して、レコードの作成時や保存時に、属性のデータの送信日時を制御できます。 たとえば、フォーム内の論理のコントロールを目的とした、フォーム上のフィールドがあるとします。 内部データの取得は考慮しません。 データが保存されないように設定するとします。 または、常に含まれている値に応じて、プラグインを持つ場合もあります。 属性が常に含まれるように設定するかもしれません。 

**createdby** などのレコードを、初期保存後に属性が更新されないように設定し、保存時に送信されないようにします。 変更されたかどうかを表す属性値を強制的に送信するには、このメソッドを使用して*モード* パラメーターを "always" に設定します。

### <a name="related-topic"></a>関連項目
[getSubmitMode (クライアント API 参照)](getSubmitMode.md)

