---
title: モデル駆動型アプリケーションの getValue (クライアント API 参照)| MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
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
# <a name="getvalue-client-api-reference"></a>getValue (クライアント API 参照)



ユーザーが特定のテキスト フィールドまたは数値フィールドに文字を入力したときに、コントロールの最新の値を取得します。 このメソッドでは、データを検証し、コントロールに文字を入力するときにユーザーに警告することによって、インタラクティブなエクスペリエンスを作成できます。

getValue メソッドは、属性の [getValue](../attributes/getvalue.md) メソッドとは異なります。コントロール メソッドはユーザーがコントロールに入力するときにコントロールから値を取得するのに対し、属性の getValue メソッドはユーザーがフィールドをコミット (保存) した後に値を取得します。 

## <a name="syntax"></a>構文

`formContext.getControl(arg).getValue();`

## <a name="return-value"></a>戻り値

**種類**: 文字列

**説明**: コントロールの最新のデータ値です。

