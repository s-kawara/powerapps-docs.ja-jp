---
title: モデル駆動型アプリの getGlobalContext (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: d87e0614-f365-4ed1-992a-741575bb2b7e
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getglobalcontext-client-api-reference"></a>getGlobalContext (クライアント API 参照)



[!INCLUDE[./includes/getGlobalContext-description.md](./includes/getGlobalContext-description.md)]
 メソッドは、フォーム コンテキストを使用せずに、グローバル コンテキストへのアクセスを提供します。 それには、クライアント、組織またはユーザー固有の情報を取得するために、**Xrm.Page.context** オブジェクト (廃止予定) で使用可能なすべてのメソッドと同等の機能が含まれます。

> [!IMPORTANT]
> スタンドアロン HTML Web リソースのグローバル コンテキスト情報にアクセスするには、**ClientGlobalContext.js.aspx** に対する参照を Web リソースに含めてから、**GetGlobalContext** 関数を使用する必要があります。 詳細情報: [GetGlobalContext 関数および ClientGlobalContext.js.aspx](../GetGlobalContext-ClientGlobalContext.js.aspx.md) 

## <a name="properties-of-global-context-getglobalcontext"></a>グローバル コンテキストのプロパティ (getGlobalContext)

グローバル コンテキストの次のプロパティを使用して、クライアント、組織の設定、またはユーザー設定に関する情報を返します。

|プロパティ |内容 | 
|---|---|
|[client](getGlobalContext/client.md) | クライアントに関する情報を返します。|
|[organizationSettings](getGlobalContext/organizationSettings.md) | 現在の組織の設定に関する情報を返します。|
|[userSettings](getGlobalContext/userSettings.md) | 現在のユーザー設定に関する情報を返します。|


## <a name="methods-of-global-context-getglobalcontext"></a>グローバル コンテキストのメソッド (getGlobalContext)

|メソッド |内容 |
|---|---|
|[getAdvancedConfigSetting](getGlobalContext/getAdvancedConfigSetting.md) |組織の高度な構成設定に関する情報を返します。|
|[getClientUrl](getGlobalContext/getClientUrl.md) |アプリケーションへのアクセスに使用された基本 URL を返します。|
|[getCurrentAppName](getGlobalContext/getCurrentAppName.md) |モデル駆動型アプリで現在のビジネス アプリの名前を返します。|
|[getCurrentAppProperties](getGlobalContext/getCurrentAppProperties.md) |モデル駆動型アプリで現在のビジネス アプリのプロパティを返します。|
|[getCurrentAppUrl](getGlobalContext/getCurrentAppUrl.md) |モデル駆動型アプリで現在のビジネス アプリの URL を返します。|
|[getVersion](getGlobalContext/getVersion.md) |モデル駆動型アプリ インスタンスのバージョン番号を返します。|
|[isOnPremises](getGlobalContext/isOnPremises.md) |モデル駆動型アプリ インスタンスが設置型またはオンラインでホストされているかどうかを示すブール値を返します。|
|[prependOrgName](getGlobalContext/prependOrgName.md) |現在の組織の一意の名前を文字列、通常、URL パスの前につけます。|




 



