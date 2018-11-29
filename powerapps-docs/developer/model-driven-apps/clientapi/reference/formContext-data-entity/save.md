---
title: モデル駆動型アプリにおける save (Client API リファレンス) | Microsoft Docs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: a27f8267-9b24-42b7-a075-420a26db6693
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

## <a name="syntax"></a>構文

`formContext.data.entity.save(saveOption);`

## <a name="parameters"></a>パラメーター

|Name|種類​​|必須出席者|内容|
|--|--|--|--|
|saveOption|String|No|レコードを保存するためのオプションを指定します。 メソッドにパラメーターが含まれていない場合、レコードは保存されるだけです。 これは、**保存**コマンドを使うのと同じことです。<br/>次のいずれかの値を指定できます。<br/><br/>- **saveandclose**: これは、**保存して閉じる**コマンドを使うのと同じことです。<br/><br/>- **saveandnew**: これは、**保存して新規作成**コマンドを使うのと同じことです。|

## <a name="example"></a>例

保存完了後に新しいフォームを開くには、以下を行います。

`formContext.data.entity.save("saveandnew");`

### <a name="related-topics"></a>関連トピック

[formContext.data.save](../formContext-data/save.md)

[formContext](../../clientapi-form-context.md)

