---
title: 'アプリ用 Common Data Service Web API Helper Library (C#) を使用する (アプリ用 Common Data Service) | Microsoft Docs'
description: アプリ用 Common Data Service Web API Helper Library は、アプリケーションの構成、アプリ用 Common Data Service に対する認証、HTTP 応答エラー処理など、一般的なタスクの実行に役立ちます
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: crm-online
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
ms.assetid: ba9d94fe-d189-4873-aef5-0010f3ccecba
caps.latest.revision: 7
author: brandonsimons
ms.author: jdaly
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="use-the-common-data-service-for-apps-web-api-helper-library-c"></a>アプリ用 Common Data Service Web API Helper Library (C#) の使用

この SDK で解説するアプリ用 Common Data Service Web API C# コードサンプルのほとんどは、アプリケーション構成、アプリ用 Common Data Service のサービスに対する認証、HTTP応答エラー処理のような、一般的なタスクの実行を支援するために  *アプリ用 Common Data Service Web API Helper Library* を使用します。 このヘルパー コードは .Net Framework ベースのプロジェクトでも役立ちます。  
  
## <a name="obtain-and-use-the-helper-library"></a>ヘルパー ライブラリーの取得と使用

アプリ用 Common Data Service Web API Helper Library は、NuGet パッケージ [Microsoft.CrmSdk.WebApi.Samples.HelperCode](https://www.nuget.org/packages/Microsoft.CrmSdk.WebApi.Samples.HelperCode) として配布されます。 Visual Studio プロジェクトで、NuGet パッケージのダウンロード、およびインストールに慣れていない場合は、「[必要なすべてのリソースをプロジェクトに追加する](start-web-api-project-visual-studio-csharp.md#bkmk_addAllRequiredResources)」を参照してください。  
  
> [!WARNING]
>  この Nuget パッケージは、ヘルパー ライブラリーの権限あるソースです。  便利性のため、このセクションのトピックでは、このライブラリの各クラスのコード一覧を含みます。 ただし、次の一覧は、完全、または最新であることが保証されないので、プロジェクトで使用することはできません。  
  
## <a name="in-this-section"></a>このセクションの内容 
 
[ヘルパー コード: 構成クラス](web-api-helper-code-configuration-classes.md)<br />
[ヘルパー コード: 認証クラス](web-api-helper-code-authentication-class.md)<br /> 
[ヘルパー コード: CrmHttpResponseException クラス](web-api-helper-code-crmhttpresponseexception-class.md)  
  
### <a name="see-also"></a>関連項目
 
[Web API (C#) を開始する](get-started-dynamics-365-web-api-csharp.md)<br />
[Visual Studio (C#) で Web API プロジェクトを起動する](start-web-api-project-visual-studio-csharp.md)<br />
[Web API を使用して演算を実行する](perform-operations-web-api.md)
