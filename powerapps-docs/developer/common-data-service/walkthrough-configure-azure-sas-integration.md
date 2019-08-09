---
title: 'チュートリアル: 統合用の Microsoft Azure (SAS) の構成 (Common Data Service)| Microsoft Docs'
description: このチュートリアルは、Azure Service Bus に投稿される Common Data Service のメッセージをリスナー アプリケーションが読み取れるように、Azure Service Bus の発行者、スコープ、およびルールを構成する方法を説明します。
keywords: ''
ms.date: 10/31/2018
ms.service: powerapps
ms.custom:
  - ''
ms.topic: article
ms.assetid: d7b24b11-57f0-ab05-4bec-0b64efee178d
author: brandonsimons
ms.author: jdaly
manager: ryjones
ms.reviewer: null
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---

# <a name="tutorial-configure-azure-sas-for-integration-with-common-data-service"></a>チュートリアル: 統合用の Azure (SAS) の構成Common Data Service

<!-- https://docs.microsoft.com/dynamics365/customer-engagement/developer/walkthrough-configure-azure-sas-integration -->

このチュートリアルは、Azure Service Bus に投稿される Common Data Service のメッセージをリスナー アプリケーションが読み取れるように、Azure Service Bus の発行者、スコープ、およびルールを構成する方法を説明します。  
  
> [!NOTE]
>  このチュートリアルは、Azure メッセージングに SAS 認証を使用するとき、Common Data Service の展開に適用されます。 Azure Service Bus 認証の詳細については、 [Service Bus の認証および承認](https://azure.microsoft.com/documentation/articles/service-bus-authentication-and-authorization/) を参照してください。  
>   
> プラグイン登録ツールを使用する必要があります。 プラグイン登録ツールをダウンロードするには、[NuGetからのツールのダウンロード](download-tools-NuGet.md)参照してください。
  
## <a name="prerequisites"></a>前提条件  
  
-   Service Bus エンティティを作成するライセンスを持つ Azure アカウント。
  
-   SAS 構成されたサービス バスの名前空間。
  
-   SAS 構成されたサービス バス メッセージング エンティティ: キュー、トピック、リレー、またはイベント ハブ。
  
-   メッセージング エンティティは、少なくとも `Send` ポリシー アクセス許可を持つ必要があります。 双方向リレーの場合は、このポリシーは `Listen` アクセス許可も持つ必要があります。  
-  メッセージング エンティティの承認接続文字列。 
  
 ![Azure のポリシー権限の定義](media/policy-permissions.png "Azure のポリシー権限の定義")  
  
 Service Bus の名前空間とメッセージング エンティティの作成方法の説明については、[Azure ポータルを使用して Service Bus 名前空間を作成する](/azure/service-bus-messaging/service-bus-create-namespace-portal) を参照してください。  
  
## <a name="create-a-service-endpoint"></a>サービス エンドポイントの作成

[ServiceEndpoint エンティティ](reference/entities/serviceendpoint.md) には、Azure Service Bus ソリューション エンドポイントによる外部メッセージングに必要な構成データが格納されます。 プラグイン登録ツールを使用して、Common Data Service 組織内にサービス エンドポイント エンティティを簡単に作成して、サービス バス エンドポイントの発行者、スコープ、およびルールを構成することができます。
  
### <a name="register-a-service-endpoint"></a>サービス エンドポイントの登録  
  
1.  プラグイン登録ツールを実行して、ターゲットの Common Data Service 組織にログインします。  
  
2.  **登録、新しいサービス エンドポイントの登録**を順に選択します。  
  
3.  **Azure Service Bus ポータルからの接続文字列で始めます**をオンにして、サービス バス メッセージング エンティティの接続文字列を貼り付けます。  
  
 ![認証接続文字列の表示](media/sas-connection-string.PNG "認証接続文字列の表示")  
  
4.  **次へ**を選択します。  
  
5.  **指定の種類**、**メッセージ形式**のフィールドに入力し、また必要に応じて**送信ユーザー情報**、**説明**フィールドに入力することによって、**サービス エンドポイントの登録**フォームの書き込みを完成します  
  
 ![エンドポイント登録のサービス](media/service-endpoint-registration.PNG "エンドポイント登録のサービス")  
  
   メッセージ形式の詳細については、「[Azure ソリューション用リスナー アプリケーションの記述](write-listener-application-azure-solution.md)」を参照してください。  
  
6.  **保存**を選びます。  
  
7.  数秒ほどしてから、**登録されたプラグインおよびユーザー定義のワークフロー活動**の一覧に新しいサービス エンドポイントが表示されます。  
  
 ![新しいサービス エンドポイント](media/new-service-endpoint.PNG "新しいサービス エンドポイント")  
  
### <a name="see-also"></a>関連項目

[Azure 統合](azure-integration.md)<br />
[Azure Service Bus](/azure/service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)
