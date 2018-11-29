---
title: モデル駆動型アプリにおける isAvailableOffline (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: ea9eacc0-2e31-49f4-a329-dcdf430a5a7e
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="isavailableoffline-client-api-reference"></a>isAvailableOffline (クライアント API 参照)



[!INCLUDE[./includes/isAvailableOffline-description.md](./includes/isAvailableOffline-description.md)] 

## <a name="syntax"></a>構文

`Xrm.WebApi.offline.isAvailableOffline(entityLogicalName);`

## <a name="parameters"></a>パラメーター

<table style="width:100%">
<tr>
<th>Name</th>
<th>種類​​</th>
<th>必須出席者</th>
<th>内容</th>
</tr>
<tr>
<td>entityLogicalName</td>
<td>String</td>
<td>あり</td>
<td>エンティティの論理名。 たとえば、「account」。</td>
</tr>

</table>

## <a name="return-value"></a>戻り値

**種類**: ブール値。

**説明**: エンティティがユーザーのプロファイルにあり、オフライン モードで現在使用可能な場合は true です。それ以外の場合は false です。

[Xrm.WebApi.offline](offline.md)

[Xrm.WebApi](../xrm-webapi.md)




