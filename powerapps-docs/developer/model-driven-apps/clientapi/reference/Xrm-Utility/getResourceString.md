---
title: モデル駆動型アプリの getResourceString (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: d5e51eac-ce0a-4f4a-b7b6-495433e3f8c1
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getresourcestring-client-api-reference"></a>getResourceString (クライアント API 参照)



[!INCLUDE[./includes/getResourceString-description.md](./includes/getResourceString-description.md)] 

## <a name="syntax"></a>構文

`Xrm.Utility.getResourceString(webResourceName,key)` 

## <a name="parameters"></a>パラメーター

|Name |種類​​ |必須出席者 |内容 |
|---|---|---|---|
|webResourceName|String|あり|Web リソースの名前。|
|キー|String|あり|ローカライズされた文字列のキー。|

## <a name="return-value"></a>戻り値

ローカライズされた文字列。

## <a name="remarks"></a>備考

<!-- 
Content adapted from /developer/resx-web-resources 
If you change this, make sure that topic is in sync.
-->

RESX Web リソースを作成するときには、言語値を明示的に設定して、Web リソースの名前に適切な言語のロケール ID (LCID) を含める必要があります。 たとえば、`new_/strings/MyAppResources.1033.resx` には英語のリソースが含まれます。 LCID 値のリストについては、「[Microsoft ロケール ID 値](https://msdn.microsoft.com/library/ms912047(WinEmbedded.10).aspx)」を参照してください。

たとえば、`Xrm.Utility.getResourceString("new_/strings/MyAppResources","hello")` は、ユーザーの優先言語が英語である場合には、`new_/strings/MyAppResources.1033.resx` Web リソース内でリソース キーのローカライズされた文字列値 `hello` を返します。 関数は特定の言語または RESX Web リソースのフル ネームを参照しないことに注意してください。 この機能は、依存関係として呼び出し JavaScript Web リソースに関連付けられている RESX Web リソースに依存します。 詳細情報: [Web リソースの依存関係](../../../web-resource-dependencies.md)。

適切な文字列値は、各ユーザーの言語設定と組織で使用可能な言語によって決まります。 ローカライズされた文字列がユーザーの言語設定と一致しない場合、ローカライズされた文字列が組織の基本言語に自動的にフォールバックします。 組織の基本言語に一致するローカライズされた文字列が見つからない場合、null 値が返されます。

### <a name="related-topics"></a>関連トピック

[Xrm.Utility](../xrm-utility.md)<br />
[文字列 (RESX) Web リソース](../../../resx-web-resources.md)<br />
[Web リソースの依存関係](../../../web-resource-dependencies.md)



