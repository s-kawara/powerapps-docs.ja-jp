---
title: OAuth を使用するクロス オリジン リソース共有を使用して単一ページのアプリケーションへ接続する (Common Data Service) | MicrosoftDocs
description: OAuth を使用するクロス オリジン リソース共有を使用して単一ページのアプリケーションへ接続する方法について説明します。
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: get-started-article
applies_to:
  - Dynamics 365 (online)
ms.assetid: oauth-cross-origin-resource-sharing-connect-single-page-application
caps.latest.revision: 11
author: paulliew
ms.author: jdaly
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
<!-- https://docs.microsoft.com/dynamics365/customer-engagement/developer/oauth-cross-origin-resource-sharing-connect-single-page-application 

-->
# <a name="use-oauth-with-cross-origin-resource-sharing-to-connect-a-single-page-application"></a>OAuth を使用するクロス オリジン リソース共有を使用して、単一のページ アプリケーションに接続する

JavaScriptを使用して Common Data Service データと連携する単一ページのアプリ (SPA) を作成できます。 これを実現するために、クロス オリジン リソース共有 (CORS) が有効化され SPA がクロス ドメインの境界を横切る要求を通常防ぐブラウザー制限が回避されます。  
  
> [!NOTE]
>  Web API を使用している場合にのみ CORS がサポートされます。 組織サービスまたは廃止された組織データ サービスは使用できません。  
  
<a name="bkmk_Spas_and_same_origin_policy"></a> 
  
## <a name="spas-and-same-origin-policy"></a>SPA と同一取得元ポリシー  

SPA は、関連するクライアント側の JavaScript を全面的に使用して、新しいページを読み込む必要はない 1 つのページを作成します。 代わりに、XMLHTTPRequests を使用してサーバーからデータおよび他のリソースを取得します。 SPA は、データおよびリソースがアプリケーションと同じドメインに存在する場合に適しています。 ただし、他のドメインのデータおよびリソースへのアクセスを保護するには、モダンなブラウザーのすべてが同一取得元ポリシーを強制的に使用して、異なるドメインのサイトのデータおよびリソースの使用からサイトを保護する必要があります。 CORS は別ドメインのリソースへアクセスするための方法を提供します。 CORS なしで Common Data Service のデータにアクセスする SPA を作成することは実行可能なオプションではありません。  
  
<a name="bkmk_use_cors"></a>

## <a name="use-cors-with-common-data-service"></a>Common Data Service での CORS の使用 
 
[クロス オリジン リソース共有仕様](http://www.w3.org/TR/cors/) は、CORS の実装と使用方法についての詳細な説明を提供します。 CORS が作動するために適応する必要がある、さまざまなヘッダーおよび事前に要求される事柄に関してすべてを説明します。 良いニュースは Common Data Service では CORS のエキスパートになる必要がないことです。 サーバー側の設定は既に完了しており、必要なのは使用方法を知ることだけです。  Common Data Service では CORS の内部構造についてをすべて理解する必要はありません。 代わりに [Azure Active Directory 認証ライブラリ (JavaScript)](https://github.com/AzureAD/azure-activedirectory-library-for-js) (adal.js) を使用することにより、CORS の複雑さからかなり解放されます。 Common Data Service が Azure Active Directory を使用して認証されるので、ADAL.js は SPA ユーザーを認証するためにサポートされている方法です。  
  
<a name="bkmk_how_adaljs_works"></a>

## <a name="how-adaljs-works"></a>adal.js の仕組み

コア ライブラリは、`adal.js` です。 このライブラリの最小化バージョンには、「[https://secure.aadcdn.microsoftonline-p.com/lib/1.0.0/js/adal.min.js](https://secure.aadcdn.microsoftonline-p.com/lib/1.0.0/js/adal.min.js)」からアクセスできます。 Github プロジェクトとドキュメントは、「[https://github.com/AzureAD/azure-activedirectory-library-for-js](https://github.com/AzureAD/azure-activedirectory-library-for-js)」にあります。  
  
adal.js ライブラリには OAuth2 を使用して認証するための下位レベルの機能があります。 Adal.js は、他のフレームワークと共に使用できるように設計されています。たとえば `adal-angular.js` ライブラリは Angular フレームワークと共に使用するように設計されています。このライブラリを使用するには、ある構成プロパティを設定し、次にやり取りのフローがトリガーされるまで待機させることです。 これは、`login` 関数を単純に呼び出すか、またはアプリケーションがルーティングの動作をしている場合は、そのルートのコントローラーが構成されている方法によって認証を開始できます。  
  
認証が必要な場合は、ユーザーが資格情報を入力するサインイン ページが表示されます。 正常に認証された後に、ユーザーは URL のフラグメントとして (`#` を使用して) トークン情報が添付された呼び出し元ページにリダイレクトされます。 こうすることにより、SPA がトークンを取得して、ブラウザーのローカルまたはセッション記憶域にキャッシュすることができます。 つまり、ページ全体が認証後に再ロードされるが、今回は認証されたユーザーに関する情報が使用可能で、アプリケーションが Common Data Service Web API または他のリソースの呼び出しに進むことができることを意味します。  
  
Common Data Service Web API を呼び出す場合、XMLHTPPRequest を含めた承認ヘッダーにトークン値を含める必要があります。 しかし、トークンには有効期限があるので、ユーザーが SPA を使用している間に有効期限が切れないことを確認する必要があります。 新しい資格情報を入力する場合、SPA ページのコンテンツすべてがサインイン ページに転送されることに注意してください。 ユーザーが何かをしている間にこれが発生すると、ユーザー エクスペリエンスがとても低下する可能性があります。 これが発生しないようにするためには、Web API コールを `acquireToken` 機能内にラップし、必要であればユーザーがサインイン ページに戻されることなく、トークンの有効性が確認および更新されるようにします。  
  
<a name="bkmk_preparing_to_use_adaljs"></a>

## <a name="preparing-to-use-adaljs-with-a-spa"></a>SPA と共に ADAL.js を使用する準備

 SPA を adal.js と共に使用するように構成するには:  
  
1.  Azure Active Directory テナント用にアプリケーションを登録します。  
2.  登録されたアプリケーション マニフェストをエクスポートし、OAuth2 の暗黙的なフローを許可するように編集し、JSON ファイルをアプリケーション登録のためにインポートして戻します。  
3.  その登録からの情報と共に SPA の構成変数を設定します。  
     次を含む必要があります。  
  
    -   Common Data Service 組織への URL  
    -   組織が認証で使用する Active Directory テナントの名前  
    -   アプリケーションの登録時に入手したクライアント ID  
    -   SPA が展開されるか、または開発中にデバッグされる URL  


 必要な設定の手順は「[チュートリアル: adal.js で SPA アプリケーションを登録および構成する](walkthrough-registering-configuring-simplespa-application-adal-js.md)」で説明されています。  
  
### <a name="see-also"></a>関連項目

[OAuth を使用して Common Data Service Web サービスに接続する](connect-web-services-using-oauth.md)   


