---
title: 'チュートリアル: Azure Active Directory にアプリを登録する (Common Data Service) | Microsoft Docs'
description: このチュートリアルでは、Common Data Service に接続し、OAuth を使用して認証を行い、Web サービスにアクセスできるようにするために、アプリケーションを Azure Active Directory に登録する方法について説明します。
keywords: ''
ms.date: 10/31/2018
ms.service:
  - powerapps
ms.custom:
  - ''
ms.topic: article
ms.assetid: 86c4a8a8-7401-6d75-7979-3b04b506eb0c
author: paulliew
ms.author: jdaly
manager: ryjones
ms.reviewer: kvivek
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---

# <a name="walkthrough-register-an-app-with-azure-active-directory"></a>チュートリアル: Azure Active Directory にアプリを登録する

このチュートリアルでは、ユーザーが、PowerApps ユーザー アカウントで、OAuth 認証を使用して外部クライアント アプリケーションから Common Data Service 環境に接続できるようにするアプリケーションを Azure Active Directory に登録する方法について説明します。

> [!IMPORTANT]
> また、PowerApps には、外部アプリケーションから、および特別なアプリケーション ユーザー アカウントを使用するサービスから Common Data Service 環境のインスタンスに接続するためのサーバー間 (S2S) 認証オプションも用意されています。 S2S 認証は Microsoft AppSource に登録されたアプリがサブスクライバーのデータにアクセスする一般的な方法です。 次を参照してください。 詳細情報: [サーバー間 (S2S) 認証を使用して Web アプリケーションを作成する](build-web-applications-server-server-s2s-authentication.md)。


Azure Active Directory へのアプリケーションの登録は、Common Data Service でのデータの読み取りと書き込みを実行する外部クライアント アプリケーションを開発する ISV によって行われます。 Azure Active Directory アプリケーションの登録では、ISV がクライアント アプリケーションの認証コードで使用できる**アプリケーション ID** と**リダイレクト URI** の値が提供されます。 エンドユーザーが ISV のアプリケーションを使用して、自分たちの Common Data Service 資格情報で Common Data Service インスタンスに*初めて*接続するとき、同意フォームがエンドユーザーに表示されます。 ISV のアプリケーションでの Common Data Service アカウントの使用に同意すると、エンドユーザーは、外部アプリケーションから Common Data Service 環境に接続できます。 同意フォームは、ISV のアプリケーションの使用に既に同意している最初のユーザー以外のユーザーには再度表示されません。 Azure Active Directory に登録されているアプリケーションはマルチテナント型です。つまり、他のテナントの他の Common Data Service ユーザーが ISV アプリを使用して環境に接続できることを意味しています。 

アプリ登録も、Common Data Service への接続とそこでのデータの読み取り/書き込みを行うクライアント アプリケーションを作成しているアプリケーション開発者または個別のユーザーが実行することもできます。 登録済みのアプリケーションからの**アプリケーション ID** と**リダイレクト URI** の値をクライアント アプリケーションの認証コードで使用して、クライアント アプリケーションからの Common Data Service 環境に接続して必要な操作を実行できます。 アプリケーションが Common Data Service 環境と同じテナントに登録されている場合は、クライアント アプリケーションから Common Data Service 環境に接続したとき、同意フォームが表示されないことに注意してください。

## <a name="prerequisites"></a>前提条件  
-   アプリケーションを登録するユーザーには、Office 365 のサブスクリプションのために、システム管理者セキュリティ ロールとグローバル管理者ロールを備えたユーザー アカウントが必要です。  
  
-   アプリケーションの登録のための Azure サブスクリプション。 試用アカウントも有効です。  
  
    

## <a name="create-an-application-registration"></a>アプリケーション登録の作成 
  
1.  管理者権限を持つアカウントを使用して、Azure 管理ポータルに [サインイン](http://manage.windowsazure.com) します。 アプリの登録に使用するものと同じ Office 365 サブスクリプション (テナント) のアカウントを使用する必要があります。<br><br> 左のナビゲーション ウィンドウで**管理センター**アイテムを展開し、**Azure AD**を選択することによって、Office 365 [管理センター](https://admin.microsoft.com/adminportal) を通して Azure 管理ポータルにもアクセスできます。  
  
    > [!NOTE]
    > ユーザーが Azure テナント (アカウント) を持っていないか、または持っているが Dynamics 365 (online) での Office 365 サブスクリプションが Azure サブスクリプションで使用できない場合は、トピック [開発者サイトの Azure Active Directory のアクセスを設定](https://docs.microsoft.com/office/developer-program/office-365-developer-program) の手順に従って、2 つのアカウントを関連付けます。<br><br> アカウントがない場合は、クレジット カードを使用して、アカウントにサインアップすることができます。 ただし、このトピックの手順を実行して 1 つまたは複数のアプリケーションを登録する場合は、アカウントは無料なのでクレジット カードに請求はありません。 詳細: [Active Directory 価格設定詳細](http://azure.microsoft.com/pricing/details/active-directory/)  
  
1. Azure 管理ポータルで、Azure Active Directory 開発者ガイドの[アプリケーションの追加](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-an-application)セクションで説明した手順に従って、アプリケーションを作成します。 
  
1. Azure Active Directory でアプリケーションを作成するとき、ユーザーのアプリケーション用の一意の**アプリケーション ID** (以前は**クライアント ID** と呼ばれていた) が生成され、登録済みのアプリケーション ページに新しく登録したアプリケーションが表示されます。 そのアプリケーションをクリックして、情報ページを開きます。

1. [アプリケーション情報] ページで、アプリケーションの認証コードまたは app.config ファイルに**アプリケーション ID** (以前は**クライアント ID** と呼ばれていた) の値を指定する必要があるとき、その値の上にカーソルを置いて、**クリックしてコピー**アイコンを選択してその値をコピーします。

    ![アプリケーション ID のコピー](media/Azure-copy-app-id.png "アプリケーション ID のコピー")
  
1. アプリケーション ページで**設定**を選択し、**設定**ページで**リダイレクト URI** オプションを使用して、アプリケーションのためのリダイレクト URI 値をコピーします。 必要に応じて、追加の URI を変更または追加することもできます。 **Web アプリケーション / API** のアプリケーション タイプのアプリケーションの場合、**リダイレクト URI** オプションではなく、**応答 URL** オプションが表示されます。

## <a name="apply-permissions"></a>アクセス許可の適用

1. **設定**ページで、**必要なアクセス許可** > **追加**を選択して、登録したアプリケーションに対するアクセス許可を追加します。

    ![アプリケーションのアクセス許可の追加](media/Azure-add-app-permission.png "アプリケーションのアクセス許可の追加")
  
1. **API アクセスの追加**ページで、次の操作を行います。
    - **API の選択** > **Dynamics CRM Online** を順に選択してから、**選択**をクリックします。

      ![アプリケーションのアクセス許可の追加](media/Azure-add-api-access.png "アプリケーションのアクセス許可の追加")  
   
    - **アクセス許可の選択** > **組織のユーザーとして CRM Online にアクセスする**を選択してから、**選択**をクリックします。
  
      ![委任されたアクセス許可の追加](media/azure-add-permission.PNG "委任されたアクセス許可の追加")  

    - **完了**を選択して、登録したアプリケーションに委任されたアクセス許可を追加します。

これにより、Azure Active Directory でのアプリケーションの登録が完了します。

## <a name="additional-configuration-options"></a>その他の構成オプション

アプリケーションが CORS に依存する Single Page Application (SPA) である場合、暗黙的なフローをサポートするようにアプリ登録を構成する必要があります。 詳細: [チュートリアル: adal.js で SPA アプリケーションを登録および構成する](walkthrough-registering-configuring-simplespa-application-adal-js.md)

アプリケーションがサーバー間接続をサポートする場合は、[マルチ テナント型でのサーバー間認証の使用](use-multi-tenant-server-server-authentication.md) を参照してください

  
### <a name="see-also"></a>関連項目  
 [Azure Active Directory へのアプリケーションの登録](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)    
 [Dynamics 365 Web サービスでのユーザーの認証](authentication.md)