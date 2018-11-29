---
title: モデル駆動型アプリにおける Xrm.WebApi.offline (クライアント API リファレンス) | Microsoft Docs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 848c277b-bd44-4388-852a-0f59a3a15538
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="xrmwebapioffline-client-api-reference"></a>Xrm.WebApi.offline (クライアント API 参照)



[!INCLUDE[./includes/offline-description.md](./includes/offline-description.md)] 

モバイル オフライン機能の詳細については、「[Mobile offline 同期を構成してモバイル デバイス上のオフライン モードの作業をユーザーに許可する](/dynamics365/customer-engagement/mobile-app/configure-mobile-offline-synchronization-dynamics-365-phones-tablets)」を参照してください

`var offlineWebApi = Xrm.WebApi.offline;`

> [!NOTE]
> [廃止された](/dynamics365/get-started/whats-new/customer-engagement/important-changes-coming#some-client-apis-are-deprecated) **Xrm.Mobile.Offline** 名前空間ではなく、**Xrm.WebApi.offline** 名前空間を使用して、オフライン モードを使用中にモバイル クライアントのレコードを作成および管理します。

**offlineWebApi** オブジェクトは、次のメソッドを提供しています。 オフライン モード時、これらのメソッドはモバイル オフライン同期で有効化されて現在のユーザーのモバイル オフライン プロファイルで利用可能なエンティティに対してのみ動作します。

- [createRecord](createRecord.md)
- [deleteRecord](deleteRecord.md)
- [isAvailableOffline](isAvailableOffline.md)
- [retrieveRecord](retrieveRecord.md)
- [retrieveMultipleRecords](retrieveMultipleRecords.md)
- [updateRecord](updateRecord.md)

> [!IMPORTANT]
> オフライン モードでレコードを作成、または更新する場合、基本的な検証のみが入力データで実行されます。 基本的な検証には指定されたエンティティ属性の名前が小文字であることおよびエンティティに存在すること、指定された属性値がデータ タイプと一致しないこと、同じ GUID 値でレコードが作成されないこと、関連するエンティティを取得する際に関連するエンティティがオフラインで有効になるかどうか、取得、更新、削除するレコードが実際にオフライン データ ストアに存在するかどうかを検証します。 ビジネス レベルでは、サーバーに接続してデータを同期した場合のみ検証されます。 入力データが完全に有効な場合にのみ、レコードが作成または更新されます。

### <a name="related-topics"></a>関連トピック

[Xrm.WebApi.online](online.md)

[Xrm.WebApi](../xrm-webapi.md)



