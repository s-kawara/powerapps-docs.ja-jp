---
title: モデル駆動型アプリにおけるクライアント API Xrm オブジェクト | Microsoft Docs
description: このトピックでは、モデル駆動型アプリのクライアント API 参照を提供します。
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: conceptual
applies_to:
  - Dynamics 365 (online)
ms.assetid: 15272ad9-25d7-499e-9361-a65f789daf20
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---

# <a name="client-api-xrm-object"></a>クライアントAPI Xrmオブジェクト



**Xrm** オブジェクトは、グローバルに利用可能であり、クライアント APIの実行コンテキストを使用する必要なくコードで使用できます。

## <a name="xrm-object-model"></a>Xrmオブジェクト モデル 

次の図はXrmオブジェクト モデルを表しています:

![Xrmオブジェクト モデル](../media/ClientAPI-XrmModel.png)

Xrmオブジェクトの各ネームスペースについての情報はこちら:

|名前空間  |内容  |
---------|---------------
|[Xrm.Device](reference/xrm-device.md)|モバイル デバイスのネイティブデバイス機能を使用するメソッドを提供します。|
|[Xrm.Encoding](reference/xrm-encoding.md)|文字列をエンコードするためのメソッドを提供します。|
|[Xrm.Navigation](reference/xrm-navigation.md)|モデル駆動型アプリのフォームおよびアイテムを操作するためのメソッドを提供します。|
|[Xrm.Panel](reference/xrm-panel.md)|モデル駆動型アプリ フォームのサイド ウインドウで Web ページを表示するメソッドを提供します。|
|[Xrm.Utility](reference/xrm-utility.md)|有用なメソッドのコンテナを提供します。|
|[Xrm.WebApi](reference/xrm-webapi.md)|Web API を使用してレコードを作成および管理し、Web API アクションおよび関数を実行するメソッドを提供します。<br/><br/>[Xrm.WebApi.offline](reference/xrm-webapi/offline.md): *オフライン*モードを使用中にモデル駆動型アプリ モバイル クライアントのレコードを作成および管理するメソッドを提供します。<br/><br/>[Xrm.WebApi.online](reference/xrm-webapi/online.md): サーバーに接続しているときに、Web API を使用してレコードを作成および管理し、Web API アクションおよび関数を実行するメソッドを提供します。|

## <a name="client-api-global-context"></a>クライアントAPIグローバルコンテキスト

**Xrm.Utility**.[getGlobalContext](reference/xrm-utility/getGlobalContext.md) メソッドをフォームで使用して、フォーム実行コンテキストを経由せずにスクリプトが実行される組織、ユーザー、またはクライアント固有の情報を取得します。 これは、 **Xrm.Page.context**を使用してグローバルコンテキストを取得するために、フォームコンテキストを使用する必要があった以前のバージョンからの変更です。

> [!NOTE]
> **Xrm.Page.context** は現在のリリースで [廃止され](/dynamics365/get-started/whats-new/customer-engagement/important-changes-coming#some-client-apis-are-deprecated)、バージョン 9.0 またはそれ以降を対象とするコード内のグローバル コンテキストを取得するために、新しい **Xrm.Utility.**[getGlobalContext](reference/xrm-utility/getGlobalContext.md) メソッドを使用する必要があります。 

スタンドアロン HTML Web リソースのグローバル コンテキスト情報にアクセスするには、**ClientGlobalContext.js.aspx** に対する参照を Web リソースに含めてから、**GetGlobalContext** 関数を使用する必要があります。 詳細情報: [GetGlobalContext 関数および ClientGlobalContext.js.aspx](reference/GetGlobalContext-ClientGlobalContext.js.aspx.md)

### <a name="related-topics"></a>関連トピック

[クライアント API オブジェクト モデルについて](understand-clientapi-object-model.md)<br/>
[廃止されたクライアント API](/dynamics365/get-started/whats-new/customer-engagement/important-changes-coming#some-client-apis-are-deprecated)
