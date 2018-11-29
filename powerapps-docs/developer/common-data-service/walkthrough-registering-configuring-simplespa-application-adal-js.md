---
title: 'チュートリアル: adal.js で SimpleSPA アプリケーションを登録および構成する (アプリ用 Common Data Service for Apps) | Microsoft Docs'
description: このチュートリアルでは、adal.js および Cross-origin Resource Sharing (CORS) を使用して Dynamics 365 Customer Engagement のデータをアクセスするために、最も単純化された Single Page Application (SPA) の登録および構成プロセスについて説明されます。
keywords: ''
ms.date: 10/31/2018
ms.service:
  - powerapps
ms.custom:
  - ''
ms.topic: article
ms.assetid: a327d2ff-e252-61cf-1190-6a974130ef19
author: paulliew
ms.author: jdaly
manager: ryjones
ms.reviewer: null
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---

# <a name="walkthrough-registering-and-configuring-a-spa-application-with-adaljs"></a>チュートリアル: adal.js で SPA アプリケーションを登録および構成する

<!-- https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/walkthrough-registering-configuring-simplespa-application-adal-js -->

このチュートリアルでは、adal.js および Cross-origin Resource Sharing (CORS) を使用して Dynamics 365 アプリ用 Common Data Service のデータをアクセスするために、最も単純化された Single Page Application (SPA) の登録および構成プロセスについて説明されます。 詳細: [OAuth を使用するクロス オリジン リソース共有を使用して Dynamics 365 (online) の単一ページのアプリケーションへ接続する](oauth-cross-origin-resource-sharing-connect-single-page-application.md)。
  
## <a name="prerequisites"></a>前提条件  
  
- Dynamics 365  
  
-   Office 365 には、管理者ロールを持つ Dynamics 365 (online) システム ユーザー アカウントが必要です。  
  
-   アプリケーションの登録のための Azure サブスクリプション。 試用アカウントも有効です。  
  
- Visual Studio 2015  
  
<a name="bkmk_goal"></a>

## <a name="goal-of-this-walkthrough"></a>このチュートリアルの目標

このチュートリアルを完了すると、Visual Studio を使用して simple SPA アプリケーションを実行できるようになり、ユーザーが認証でき、Dynamics 365 (online) からのデータを取得できる機能が提供されます。 このアプリケーションは、単一の HTML ページで構成されています。  

アプリケーションをデバッグする場合、最初に**ログイン**ボタンのみが表示されます。  

**ログイン**をクリックすると、サインイン ページにリダイレクトされ、資格情報を入力します。  

資格情報を入力した後は、HTML ページに戻り、そこでは**ログイン**ボタンが非表示となり、**ログアウト**ボタンと**取引先企業の取得**ボタンが表示されるようになります。 また、ユーザー アカウントからの情報を使用した挨拶も表示されるようになります。  

**取引先企業の取得**ボタンをクリックし、Dynamics 365 組織から 10 件の取引先企業レコードの一覧を取得します。 次のスクリーンショットに示すとおり、**取引先企業の取得**ボタンが無効になります:  
  
![SimpleSPA ページ](media/simple-spa.png "SimpleSPA ページ")  

> [!NOTE]
>  認証をサポートする操作がなされるため、Dynamics 365 からのデータの最初の読み込みが遅くなる場合がありますが、後続の操作はさらに速くなります。  

そして、**ログアウト**ボタンをクリックし、ログアウトします。  

> [!NOTE]
>  この SPA アプリケーションは、堅牢な SPA アプリケーションを開発するパターンを表記することを目的としたものではありません。 アプリケーションの登録および構成におけるプロセスにフォーカスを設定することが簡素化されています。  
  
### <a name="create-a-web-application-project"></a>Web アプリケーション プロジェクトの作成  
  
1.  Visual Studio 2015 を使用して、新しい**ASP.NET Web アプリケーション**プロジェクトを作成し、**空**テンプレートを使用します。 プロジェクトに任意の名前を付けることがでます。  
  
    Visual Studio の以前のバージョンも使用できる必要がありますが、これらのステップでは Visual Studio 2015 の使用が説明されます。  
  
2.  SimpleSPA.html という名前の新しい HTML ページをプロジェクトに追加し、次のコードを貼り付けます:  
  
    ```html  
    <!DOCTYPE html>  
    <html>  
    <head>  
     <title>Simple SPA</title>  
     <meta charset="utf-8" />  
     <script src="https://secure.aadcdn.microsoftonline-p.com/lib/1.0.0/js/adal.min.js"></script>  
     <script type="text/javascript">  
      "use strict";  
  
      //Set these variables to match your environment  
      var organizationURI = "https:// [organization name].crm.dynamics.com"; //The URL to connect to CRM (online)  
      var tenant = "[xxx.onmicrosoft.com]"; //The name of the Azure AD organization you use  
      var clientId = "[client id]"; //The ClientId you got when you registered the application  
      var pageUrl = "http://localhost: [PORT #]/SimpleSPA.html"; //The URL of this page in your development environment when debugging.  
  
      var user, authContext, message, errorMessage, loginButton, logoutButton, getAccountsButton, accountsTable, accountsTableBody;  
  
      //Configuration data for AuthenticationContext  
      var endpoints = {  
       orgUri: organizationURI  
      };  
  
      window.config = {  
       tenant: tenant,  
       clientId: clientId,  
       postLogoutRedirectUri: pageUrl,  
       endpoints: endpoints,  
       cacheLocation: 'localStorage', // enable this for IE, as sessionStorage does not work for localhost.  
      };  
  
      document.onreadystatechange = function () {  
       if (document.readyState == "complete") {  
  
        //Set DOM elements referenced by scripts  
        message = document.getElementById("message");  
        errorMessage = document.getElementById("errorMessage");  
        loginButton = document.getElementById("login");  
        logoutButton = document.getElementById("logout");  
        getAccountsButton = document.getElementById("getAccounts");  
        accountsTable = document.getElementById("accountsTable");  
        accountsTableBody = document.getElementById("accountsTableBody");  
  
        //Event handlers on DOM elements  
        loginButton.addEventListener("click", login);  
        logoutButton.addEventListener("click", logout);  
        getAccountsButton.addEventListener("click", getAccounts);  
  
        //call authentication function  
        authenticate();  
  
        if (user) {  
         loginButton.style.display = "none";  
         logoutButton.style.display = "block";  
         getAccountsButton.style.display = "block";  
  
         var helloMessage = document.createElement("p");  
         helloMessage.textContent = "Hello " + user.profile.name;  
         message.appendChild(helloMessage)  
  
        }  
        else {  
         loginButton.style.display = "block";  
         logoutButton.style.display = "none";  
         getAccountsButton.style.display = "none";  
        }  
  
       }  
      }  
  
      // Function that manages authentication  
      function authenticate() {  
       //OAuth context  
       authContext = new AuthenticationContext(config);  
  
       // Check For & Handle Redirect From AAD After Login  
       var isCallback = authContext.isCallback(window.location.hash);  
       if (isCallback) {  
        authContext.handleWindowCallback();  
       }  
       var loginError = authContext.getLoginError();  
  
       if (isCallback && !loginError) {  
        window.location = authContext._getItem(authContext.CONSTANTS.STORAGE.LOGIN_REQUEST);  
       }  
       else {  
        errorMessage.textContent = loginError;  
       }  
       user = authContext.getCachedUser();  
  
      }  
  
      //function that logs in the user  
      function login() {  
       authContext.login();  
      }  
      //function that logs out the user  
      function logout() {  
       authContext.logOut();  
       accountsTable.style.display = "none";  
       accountsTableBody.innerHTML = "";  
      }  
  
    //function that initiates retrieval of accounts  
      function getAccounts() {  
  
       getAccountsButton.disabled = true;  
       var retrievingAccountsMessage = document.createElement("p");  
       retrievingAccountsMessage.textContent = "Retrieving 10 accounts from " + organizationURI + "/api/data/v8.0/accounts";  
       message.appendChild(retrievingAccountsMessage)  
  
       // Function to perform operation is passed as a parameter to the aquireToken method  
       authContext.acquireToken(organizationURI, retrieveAccounts)  
  
      }  
  
    //Function that actually retrieves the accounts  
      function retrieveAccounts(error, token) {  
       // Handle ADAL Errors.  
       if (error || !token) {  
        errorMessage.textContent = 'ADAL error occurred: ' + error;  
        return;  
       }  
  
       var req = new XMLHttpRequest()  
       req.open("GET", encodeURI(organizationURI + "/api/data/v8.0/accounts?$select=name,address1_city&$top=10"), true);  
       //Set Bearer token  
       req.setRequestHeader("Authorization", "Bearer " + token);  
       req.setRequestHeader("Accept", "application/json");  
       req.setRequestHeader("Content-Type", "application/json; charset=utf-8");  
       req.setRequestHeader("OData-MaxVersion", "4.0");  
       req.setRequestHeader("OData-Version", "4.0");  
       req.onreadystatechange = function () {  
        if (this.readyState == 4 /* complete */) {  
         req.onreadystatechange = null;  
         if (this.status == 200) {  
          var accounts = JSON.parse(this.response).value;  
          renderAccounts(accounts);  
         }  
         else {  
          var error = JSON.parse(this.response).error;  
          console.log(error.message);  
          errorMessage.textContent = error.message;  
         }  
        }  
       };  
       req.send();  
      }  
      //Function that writes account data to the accountsTable  
      function renderAccounts(accounts) {  
       accounts.forEach(function (account) {  
        var name = account.name;  
        var city = account.address1_city;  
        var nameCell = document.createElement("td");  
        nameCell.textContent = name;  
        var cityCell = document.createElement("td");  
        cityCell.textContent = city;  
        var row = document.createElement("tr");  
        row.appendChild(nameCell);  
        row.appendChild(cityCell);  
        accountsTableBody.appendChild(row);  
       });  
       accountsTable.style.display = "block";  
      }  
  
     </script>  
     <style>  
      body {  
       font-family: 'Segoe UI';  
      }  
  
      table {  
       border-collapse: collapse;  
      }  
  
      td, th {  
       border: 1px solid black;  
      }  
  
      #errorMessage {  
       color: red;  
      }  
  
      #message {  
       color: green;  
      }  
     </style>  
    </head>  
    <body>  
     <button id="login">Login</button>  
     <button id="logout" style="display:none;">Logout</button>  
     <button id="getAccounts" style="display:none;">Get Accounts</button>  
     <div id="errorMessage"></div>  
     <div id="message"></div>  
     <table id="accountsTable" style="display:none;">  
      <thead><tr><th>Name</th><th>City</th></tr></thead>  
      <tbody id="accountsTableBody"></tbody>  
     </table>  
    </body>  
    </html>  
  
    ```  
  
3.  このページをプロジェクトの開始ページとして設定します。  
  
4.  プロジェクトのプロパティでは、**Web** を選択し、**サーバー**では、**Project URL** を記録します。 `http://localhost:46575/` のようになる必要があります。 生成されるポート番号を記録します。 次の手順でこれが必要になります。  
  
5.  SimpleSPA.html ページ内では、次の構成変数を見つけ、それに応じて設定します。 チュートリアルの次の部分が完了した後に、`clientId` が設定できるようになります。  
  
    ```javascript  
    //Set these variables to match your environment  
    var organizationURI = "https://[organization name].crm.dynamics.com"; //The URL to connect to CRM (online)  
    var tenant = "[xxx.onmicrosoft.com]"; //The name of the Azure AD organization you use  
    var clientId = "[client id]"; //The ClientId you got when you registered the application  
    var pageUrl = "http://localhost:[PORT #]/SimpleSPA.html"; //The URL of this page in your development environment when debugging.  
  
    ```  
  
### <a name="register-the-application"></a>アプリケーションの登録  
  
1.  管理者権限を持つアカウントを使用して、Azure 管理ポータルに [サインイン](http://manage.windowsazure.com) します。 アプリの登録に使用するものと同じ Office 365 サブスクリプション (テナント) のアカウントを使用する必要があります。 左のナビゲーション ウィンドウで**管理**アイテムを展開し、**Azure AD**を選択することによって、Office 365 管理センター を通して Azure 管理ポータルにもアクセスできます。  
  
     ユーザーが Azure テナント (アカウント) を持っていないか、または持っているが Dynamics 365 (online) での Office 365 サブスクリプションが Azure サブスクリプションで使用できない場合は、トピック [開発者サイトの Azure Active Directory のアクセスを設定](https://docs.microsoft.com/en-us/office/developer-program/office-365-developer-program) の手順に従って、2 つのアカウントを関連付けます。  
  
     アカウントがない場合は、クレジット カードを使用して、アカウントにサインアップすることができます。 ただし、このトピックの手順を実行して 1 つまたは複数のアプリケーションを登録する場合は、アカウントは無料なのでクレジット カードに請求はありません。 詳細: [Active Directory 価格設定詳細](http://azure.microsoft.com/pricing/details/active-directory/)  
  
2.  ページの左側の列で、**Active Directory** をクリックします。 左側の列をスクロールして、**Active Directory** アイコンとラベルを参照する必要がある場合があります。  
  
3.  ディレクトリ一覧で、必要なテナント ディレクトリをクリックします。  
  
    ![利用可能なアクティブ ディクショナリ エントリの一覧](media/azure-active-directory.PNG "利用可能なアクティブ ディクショナリ エントリの一覧")  
  
    Azure テナント ディレクトリがディレクトリの一覧に表示されない場合は、**追加**をクリックし、ダイアログ ボックスの**既存のディレクトリ**を使用するを選択します。 表示されるプロンプトと指示に従い、次にステップ 1 に戻ります。  
  
4.  ターゲット ディレクトリを選択して、**アプリケーション** (ページの上部付近にある) をクリックし、**追加**をクリックします。  
  
5.  **実行する内容**ダイアログ ボックスで、**組織が開発しているアプリケーションを追加する**をクリックします。  
  
6.  画面の指示に従って、例えば、「SimpleSPA」など、アプリケーションの名前を入力し、**Web アプリケーションや Web API** からタイプを選択し、右向きの矢印を選択して続行します。 疑問符 **?** をクリック 各入力フィールドの該当する値の詳細について。  
  
7.  次の情報を入力します:  
  
    **サインオン URL**  
    これは、ユーザーがサインインした後にリダイレクトされる URL です。 Visual Studio でデバッグするため、その URL は**Web アプリケーション プロジェクトの作成**手順のステップ 4 から取得したポート番号 #### を表記する `http://localhost:####/SimpleSPA.html` となります。  
  
    **アプリ ID URI**  
    これは、アプリケーションの一意の識別子である必要があります。 XXXX が Active Directory テナントである `https://XXXX.onmicrosoft.com/SimpleSPA` を使用します。  
  
8.  新しく登録したアプリケーションのタブを選択して、**構成**をクリックし、**クライアント ID** を見つけ、それをコピーします。  
  
    この値に対して、SimpleSPA.html ページの `clientId` 変数を設定します。 **Web アプリケーション プロジェクトの作成**手順の 5 を参照してください。  
  
9. ページの下部までスクロールし、**アプリケーションの追加**をクリックします。 ダイアログ ボックスで、**Dynamics 365 Online** を選択し、ダイアログ ボックスを閉じます。  
  
10. その他のアプリケーションへの許可により、**Dynamics 365 Online** および**委任されたアクセス許可: 0** の行が示されます。 これを選択し、**組織のユーザーとして Dynamics 365 (online) にアクセスする**を追加します。  
  
11. アプリケーションの登録の保存  
  
12. 下部で、**マニフェストの管理**を選択し、**マニフェストのダウンロード**を選択します。  
  
13. ダウンロード済みの JSON ファイルを開き、`"oauth2AllowImplicitFlow": false,` という行を見つけ、`false` から `true` に変更し、ファイルを保存します。  
  
14. 再度、**マニフェストの管理**に戻ります。 **マニフェストのアップロード**を選択し、先ほど保存した JSON ファイルをアップロードします。  
  
### <a name="debugging-the-application"></a>アプリケーションのデバッグ  
  
1.  Microsoft Edge、Google Chrome、または Mozilla Firefox を使用してブラウザーを設定します。  
  
    > [!NOTE]
    > Internet Explorer ではこの状況でのデバッグに対応していません。  
  
2.  [F5] キーを押して、デバッグを開始します。 [チュートリアルのゴール](walkthrough-registering-configuring-simplespa-application-adal-js.md#bkmk_goal) で、説明する動作を考慮する必要があります。  
  
     予期している結果が得られない場合は、アプリケーションの登録時および SimpleSPA.html コードの構成時にセットしたときの値を再確認します。  
  
### <a name="see-also"></a>関連項目  
 [OAuth を使用するクロス オリジン リソース共有を使用して Dynamics 365 の単一ページのアプリケーションへ接続する (オンライン)](oauth-cross-origin-resource-sharing-connect-single-page-application.md)