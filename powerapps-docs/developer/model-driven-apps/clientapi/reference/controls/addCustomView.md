---
title: モデル駆動型アプリにおける addCustomView (クライアント API 参照) | Microsoft Docs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 482b8cd4-e643-48ea-8a54-d8601271ec81
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="addcustomview-client-api-reference"></a>addCustomView (クライアント API 参照)



検索ダイアログ ボックスに新しいビューを追加します。 

## <a name="control-types-supported"></a>サポートされているコントロールの種類

検索

## <a name="syntax"></a>構文

`formContext.getControl(arg).addCustomView(viewId, entityName, viewDisplayName, fetchXml, layoutXml, isDefault)`

## <a name="parameters"></a>パラメーター

- **viewId**: 文字列。 ビューの GUID 列を表す文字列。
    > [!NOTE]
    > この値は保存されず、検索で利用できる他のビュー内で一意である必要があります。 有効ではない GUID 用の文字列は、“00000000-0000-0000-0000-000000000001” などの形をとります。 有効な GUID を生成するため、**guidgen.exe** などのツールを使用することをお勧めします。  

- **entityName**: 文字列。 エンティティの名前。
- **viewDisplayName**: 文字列。 ビューの名前です。
- **fetchXml**: 文字列。 ビューの fetchXml クエリ。
- **layoutXml**: 文字列。 ビューのレイアウトを定義する XML。
- **isDefault**: ブール型: ビューを既定のビューにする必要があるかどうかを示します。

## <a name="remarks"></a>備考

このメソッドは、**所有者**検索では使用できません。 所有者検索は、ユーザー所有レコードの割り当てに使用されます。
