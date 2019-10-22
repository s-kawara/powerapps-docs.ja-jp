---
title: 'チュートリアル: Azure Active Directory でアプリケーションを登録する (Common Data Service) | Microsoft Docs'
description: このチュートリアルでは、Common Data Service 環境に接続し、OAuth を使用して認証を行い、Web サービスにアクセスできるようにするために、アプリを Azure Active Directory に登録する方法について説明します。
keywords: ''
ms.date: 04/01/2019
ms.service: powerapps
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

# <a name="walkthrough-register-an-app-with-azure-active-directory"></a>チュートリアル: アプリを Azure Active Directory に登録します

このチュートリアルでは、PowerApps ユーザーアカウントを使用するユーザーが、、OAuth 認証を使用して外部クライアント アプリケーションから Common Data Service 環境に接続できるアプリケーションを Azure Active Directory に登録する方法について説明します。

> [!IMPORTANT]
> また、PowerApps には、外部アプリケーションから、および特別なアプリケーション ユーザー アカウントを使用するサービスからアプリ用 Common Data Service 環境のインスタンスに接続するためのサーバー間 (S2S) 認証オプションも用意されています。 S2S 認証は、Microsoft AppSource に登録されたアプリがサブスクライバーのデータにアクセスする際に使用する一般的な方法です。 詳細情報: [サーバー間 (S2S) 認証を使用して Web アプリケーションを作成する](build-web-applications-server-server-s2s-authentication.md)。

Azure Active Directory へのアプリの登録は一般的に、外部クライアント アプリケーションの開発を希望する ISV が Common Data Service でのデータの読み取りおよび書き込みを実行する際に行われます。 Azure Active Directory でのアプリケーションの登録では、ISV がクライアント アプリケーションの認証コードで使用できる**アプリケーション ID** および**リダイレクト URI** の値が提供されます。 エンド ユーザーが ISV のアプリケーションを使用して、自分たちの Common Data Service 資格情報で Common Data Service 環境に*初めて*接続するとき、同意フォームがエンド ユーザーに表示されます。 ISV のアプリケーションで Common Data Service アカウントの使用に同意した後、エンドユーザーは外部アプリケーションからCommon Data Service 環境に接続できます。 同意フォームは、ISV のアプリケーションの使用に既に同意している最初のユーザー以外のユーザーには再度表示されません。 Azure Active Directory に登録されているアプリケーションはマルチテナント型です。それはつまり、他のテナントの他の Common Data Service ユーザーが ISV アプリを使用してその環境に接続できることを意味しています。 

アプリ登録も、Common Data Service への接続およびそこでのデータの読み取り/書き込みを行うクライアント アプリケーションを作成しているアプリケーション開発者または個別のユーザーが実行することもできます。 登録済みのアプリケーションからの**アプリケーション ID**および**リダイレクト URI** の値をクライアント アプリケーションの認証コードで使用して、クライアント アプリケーションからのCommon Data Service 環境に接続して必要な操作を実行できます。 アプリケーションがCommon Data Service 環境と同じテナントに登録されている場合は、クライアント アプリケーションからCommon Data Service 環境に接続したとき、同意フォームが表示されないことに注意してください。

## <a name="prerequisites"></a>前提条件  

-   アプリケーションを登録するユーザーには、Office 365 のサブスクリプションのために、システム管理者セキュリティ ロールとグローバル管理者ロールを備えた ユーザー アカウントが必要です。  
  
-   アプリケーションの登録のための Azure サブスクリプション。 試用アカウントも有効です。  
  
## <a name="create-an-application-registration"></a>アプリケーション登録の作成 
  
1. 管理者権限を持つアカウントを使用して [Azure portal](https://go.microsoft.com/fwlink/?linkid=2083908) にサインインします。 アプリの登録に使用するものと同じ Office 365 サブスクリプション (テナント) のアカウントを使用する必要があります。 Office 365 [管理センター](https://admin.microsoft.com/adminportal) から Azure portal にアクセスするには、左側のナビゲーションウィンドウで **管理センター** の項目を展開し、 **Azure Active Directory**を選択します。  
  
   > [!NOTE]
   > Azure のテナント (取引先企業) がない場合、またはテナントがあるが、 Common Data Service のOffice365 サブスクリプションが Azure サブスクリプションで利用できない場合は、 [開発者サイトへの Azure Active Directory アクセスの設定](https://msdn.microsoft.com/office/office365/HowTo/setup-development-environment) トピックの手順に従って、2つの取引先企業を関連付けます。<br><br> アカウントがない場合は、クレジット カードを使用して、アカウントにサインアップすることができます。 ただし、このトピックの手順を実行して 1 つまたは複数のアプリケーションを登録する場合は、アカウントは無料なのでクレジット カードに請求はありません。 詳細: [Active Directory 価格設定詳細](http://azure.microsoft.com/pricing/details/active-directory/)  
  
2. Azure portal では、左側のウィンドウの **Azure Active Directory** を選択し、 **アプリの登録**を選択し、 **新規登録**をクリックします。
    
    ![Azure アプリの登録](media/azure-app-registrations-page.png "Azure アプリの登録")  

3. **アプリケーションの登録ページ**にて、アプリケーションの登録情報を入力します:
   - **名前** セクションで、ユーザーに表示するわかりやすいアプリケーションの名前を入力します。
   - **対応しているアカウントの種類** セクションで **組織ディレクトリ内のアカウント** オプションを選択します。
   - **リダイレクト URI** を設定します。
   - **登録** をクリックしてアプリケーションを作成します。

      ![新規アプリの登録ページ](media/new-app-registration-page.png "新規アプリの登録ページ")

5. アプリケーションの認証コード、または app.config ファイルで必要に応じて指定するため、アプリの **概要** ページで **アプリケーション (クライアント) ID** 値の上にカーソルを移動し、 **クリップボードにコピーする** アイコンを選択して値をコピーします。

    ![アプリケーション ID のコピー](media/app-registration-overview-page.png "アプリケーション ID のコピー")
  
5. **マニフェスト** タブを選択し、マニフェストエディタで *allowPublicClient**プロパティーを**true**に設定して**保存**をクリックします。
   
    ![アプリの登録マニフェスト](media/app-registration-manifest-page.png "アプリの登録マニフェスト")

6. **APIアクセス許可** タブを選択し、 **アクセス許可の追加** をクリックします。 

    ![アプリケーションのアクセス許可の追加](media/azure-api-permissions-page.png "アプリケーションのアクセス許可の追加")

7. **Microsoft API** タブ配下の **Dynamics CRM** を選択します。
    
    ![APIの選択](media/app-registration-select-api-page.png "APIの選択")    

8. **代理人のアクセス許可** をクリックし、オプションをチェックしてし、 **アクセス許可の追加**をクリックします。 
    
    ![代理人のアクセス許可](media/app-registration-delegate-permissions-page.png "代理人のアクセス許可")

これにより、Azure Active Directory でのアプリケーションの登録が完了します。

## <a name="additional-configuration-options"></a>その他の構成オプション

アプリケーションが CORS に依存する Single Page Application (SPA) である場合、暗黙的なフローをサポートするようにアプリ登録を構成する必要があります。 詳細: [チュートリアル: adal.js で SPA アプリケーションを登録および構成する](walkthrough-registering-configuring-simplespa-application-adal-js.md)

アプリケーションがサーバー間接続をサポートする場合は、[マルチ テナント型でのサーバー間認証の使用](use-multi-tenant-server-server-authentication.md) を参照してください
  
### <a name="see-also"></a>関連項目  
 [Azure Active Directoryで Azure アプリケーション登録](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)    
 [Common Data Service Web サービスでユーザーを認証する](authentication.md)
