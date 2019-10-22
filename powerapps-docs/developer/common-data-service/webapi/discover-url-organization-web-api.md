---
title: Web APIを使用した組織のURLの検出 (Common Data Service)| Microsoft Docs
description: 組織、またはログオン ユーザーが属するインスタンスを実行時に検出するために Web API を使用する方法を学習します。
ms.custom: ''
ms.date: 04/22/2019
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
ms.assetid: 2db13b4e-0e7c-4f25-b7be-70a612fb96e2
caps.latest.revision: 18
author: brandonsimons
ms.author: jdaly
ms.reviewer: susikka
manager: annbe
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="discover-the-url-for-your-organization-using-the-web-api"></a>Web API を使用して組織の URL を検出します

[!INCLUDE [cc-discovery-service-description](../includes/cc-discovery-service-description.md)]

Web API の検出サービスで、標準 `$filter` および `$select` パラメーターを Web API サービス要求に使用して、返されたインスタンス データのリストをカスタマイズできます。
<!-- TODO should only talk about the global discovery service -->

## <a name="global-discovery-service"></a>グローバル探索サービス

データセンター固有の探索サービスに加え、2011 (SOAP) エンドポイントで、Web API を通じて、すべての運用データセンター全体にまたがる Web API のみのグローバル探索サービスもあります。 2011 エンドポイントの検出サービスの詳細については、[検出サービス](../org-service/discovery-service.md) を参照してください。

> [!NOTE]
> ユーザーは従来の地域の探索サービス (`https://disco.crm.dynamics.com`) からグローバル探索サービス (`https://globaldisco.crm.dynamics.com`) に切り替えることをお勧めします。
> 
> Dynamics 365 US Government ユーザーの場合、グローバル検出サービスは **GCC** および **GCC High** ユーザーが利用でき、URLが通常のグローバル検出サービスのURLとは異なります。 詳細情報: [Dynamics 365 Government の URL](https://docs.microsoft.com/dynamics365/customer-engagement/admin/government/microsoft-dynamics-365-government#dynamics-365-us-government-urls)。

  
## <a name="information-provided-by-the-discovery-service"></a>探索サービスによって提供された情報 
 
 組織情報は、探索サービスの `Instance` エンティティに保存されます。  そのエンティティに含まれている情報を表示するには、まずインスタンスの 1 つのサービスに HTTP GET 要求を送信します。  
  
```http  
GET https://globaldisco.crm.dynamics.com/api/discovery/v1.0/Instances(UniqueName='myorg')  
```  
  
上の例では、Common Data Service のグローバル探索サービスを使用して、「myorg」という一意の名前のインスタンスの組織情報を取得します。 この要求に関する詳細については、このトピックの後半で詳しく説明します。  

 

  
### <a name="scope-of-the-returned-information"></a>返される情報のスコープ

グローバル探索サービスの場合、`Instances` エンティティ セットは、フィルターが適用されない場合、すべての地域のユーザーがアクセスするインスタンスのセットを返します。   次の説明に従って、返されたデータのスコープがあります。  
  
-   主権あるクラウド インスタンスが返されないことを除き、ユーザーに対してプロビジョニングされ、有効化された商用クラウド内のすべてのインスタンスが含まれます
-   ユーザー アカウントが無効の場合、インスタンスは含まれません。
-   インスタンス セキュリティ グループに基づいて、ユーザーがフィルターによって除外された場合、インスタンスは含まれません。
-   ユーザーが代理管理者であるためアクセス権を持っている場合、インスタンスは含まれません。
-   呼び出し元ユーザーがインスタンスへのアクセス権を持っていない場合は、応答は、空のリストを返します。

## <a name="how-to-access-the-discovery-services"></a>探索サービスへのアクセス方法

一般に、探索サービスの Web API アドレスには、次の形式があります。 `<service base address>/api/discovery/`。  展開の種類ごとのアドレスは以下のように識別します。 **設定 > カスタマイズ > 開発者リソース**に移動して、Common Data Service Web アプリケーションで、展開の Web API アドレスおよびバージョン番号を簡単に検索できます。  
  
### <a name="common-data-service-discovery-services"></a>Common Data Service 探索サービス  

グローバル検索サービスのサービス ベース アドレスは、`https://globaldisco.crm.dynamics.com/` です。 この結果、`https://globaldisco.crm.dynamics.com/api/discovery/` のサービス アドレスになります。  
  
## <a name="using-the-discovery-service"></a>探索サービスの使用  

`Instances` という名前のエンティティ セットを使用して、インスタンス情報を取得します。 返されたデータをフィルター処理するようにセットされたインスタンス エンティティで`$select` と `$filter` を使用できます。 または `$metadata` を使用して、サービスのメタデータ ドキュメントを取得できます。  
  
### <a name="authentication"></a>認証

探索サービスの Common Data Service Web API インスタンスは、OAuth アクセス トークンを使用した証明書が必要です。

探索サービスが、OAuth 認証用に構成されている場合、アクセス トークンなしでサービス Web API に送信される要求は、共通エンドポイントの権限およびサービスのリソース ID と共にベアラー チャレンジをトリガーします。
### <a name="cors-support"></a>CORS のサポート

DiscoveryサービスのWeb APIは、Web APIと同様にクロス オリジンアクセスの CORS 標準企画に対応しています。  CORS のサポートに関する詳細については、 [OAuthを使用してクロスオリジンリソース共有で単一ページアプリケーションに接続する](../oauth-cross-origin-resource-sharing-connect-single-page-application.md)を参照してください。  
  
### <a name="examples"></a>例  
  
-   特定のインスタンスの詳細を取得します。 GUID を省くと、認証されたユーザーがアクセスできるすべてのインスタンスが返されます。  
  
    ```http      
    GET https://globaldisco.crm.dynamics.com/api/discovery/v1.0/Instances(<guid>)
    GET https://disco.crm.dynamics.com/api/discovery/v9.0/Instances(<guid>)  
    ```  
  
-   代替キーとして UniqueName 属性を使用できます。  
  
    ```http  
    GET https://globaldisco.crm.dynamics.com/api/discovery/v1.0/Instances(UniqueName='myorg')  
    ```  
  
-   運用の種類によってフィルター処理された、利用可能なインスタンスのリストを取得します。  
  
    ```http  
    GET https://globaldisco.crm.dynamics.com/api/discovery/v1.0/Instances?$select=DisplayName,Description&$filter=Type+eq+0   
    ```  
  
-   特定のインスタンスの ID プロパティの値を取得します。  
  
    ```http  
    GET https://disco.crm.dynamics.com/api/discovery/v9.0/Instances(UniqueName='myorg')/Id/$value  
    ```

## <a name="see-also"></a>関連項目

[Web API グローバル検索サービスのサンプル (C#)](samples/global-discovery-service-csharp.md)

