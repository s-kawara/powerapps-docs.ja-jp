---
title: getSubmitMode (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: a3231438-3821-4dce-b118-d63e6ce85e01
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getsubmitmode-client-api-reference"></a>getSubmitMode (クライアント API 参照)



レコードの保存時に、いつ属性からデータが送信されるか示す文字列を返します。 

## <a name="attribute-types-supported"></a>サポートされる属性の種類

すべて

## <a name="syntax"></a>構文

`formContext.getAttribute(arg).getSubmitMode()`

## <a name="return-value"></a>戻り値

**種類**: 文字列。 

**説明**: 次のいずれかの値を返します。
- 常時
- 未実行
- ダーティ

### <a name="related-topic"></a>関連項目
[setSubmitMode (クライアント API 参照)](setSubmitMode.md)

