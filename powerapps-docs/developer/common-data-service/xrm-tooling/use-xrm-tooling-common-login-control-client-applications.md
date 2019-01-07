---
title: クライアント アプリケーションで、XRM ツール共通ログイン コントロールを使用する (アプリ用 Common Data Service)| Microsoft Docs
description: アプリ用 CDS SDK では Visual Studio 用テンプレートが用意され、これによりクライアント アプリケーションで共通ログイン コントロールを使用できるようにできます。 アプリ用 CDS 認証、資格情報の保管および検索、および診断ロギングのためのコードがテンプレートに組み込まれ、自分のアプリ用 CDS 用 Windows クライアント アプリケーションで、これらの機能を素早く活用できます
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: crm-online
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
ms.assetid: f77b2a20-0a30-4211-a1d9-74923d3eeae1
caps.latest.revision: 27
author: MattB-msft
ms.author: kvivek
manager: kvivek
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="use-the-xrm-tooling-common-login-control-in-your-client-applications"></a>クライアント アプリケーションで、XRM ツール共通ログイン コントロールを使用する

Visual Studio 用テンプレートが用意されており、これによりクライアント アプリケーションで共通ログイン コントロールを使用できるようにできます。 アプリ用 CDS 認証、資格情報の保管および検索、および診断ロギングのためのコードがテンプレートに組み込まれ、自分のアプリ用 CDS 用 Windows クライアント アプリケーションで、これらの機能を素早く活用できます。 共通ログイン コントロールは <xref:Microsoft.Xrm.Tooling.CrmConnectControl> を導入したもので、コントロールは以下の画像のようなものです。  
  
 <!--TODO:
 ![XRM Tooling common login control](../media/crm-sdk-v6-commonlogincontrol.png "XRM Tooling common login control")   -->
  
<a name="Prereq"></a>

## <a name="prerequisites"></a>前提条件
  
- .NET Framework 4.5.2
- Visual Studio 2012 またはそれ以上
- Visual Studio のバージョンの Nuget Package Manager  
- プロジェクト テンプレート使用時に必要な Nuget パッケージをダウンロード/復元できるように、インターネットに接続していること。  
- 共通ログイン コントロール テンプレートを含む、Visual Studio の CRM SDK テンプレート。 Visual Studio ギャラリーから [Microsoft Dynamics CRM SDK テンプレート](http://go.microsoft.com/fwlink/p/?LinkId=400925) をダウンロードして `CRMSDKTemplates.vsix` ファイルをダブルクリックし、テンプレートを Visual Studio にインストールすることにより取得することができます。  
  
<a name="NewProjectUsingTemplate"></a>
   
## <a name="create-a-wpf-application-using-the-common-login-control-template"></a>共通ログイン コントロール テンプレートを使用した WPF アプリケーションの作成
  
 これは、認証、資格情報の保管と再利用、および既定のトレースまたはロギングのために、共通ログイン コントロールおよび基本コード活用する Windows Presentation Foundation (WPF) アプリケーションを、素早く作成する方法です。  
  
1.  Visual Studio を起動し、新しいプロジェクトを作成します。  
2.  **新しいプロジェクト** ダイアログ ボックスで以下を実行します。  
    1.  インストールされているテンプレートの一覧から、**Visual C#** を展開し、**アプリ用 CDS SDK のテンプレート**を選択します。  
    2.  **.NET Framework 4.6.2**が選択されていることを確認します。  
    3.  **Dynamics 365 用 WPF アプリケーション**を選択します。  
    4.  プロジェクトの名前と場所を指定し、**OK** をクリックします。  
  
 <!-- TODO:
 ![WPF Application for CDS for Apps template](../media/crm-sdk-v6-xrmtooling-newproject.png "WPF Application for CDS for Apps template")   -->
  
3.  プロジェクトをテストするには:  
  
    1.  プロジェクトを保存して F5 を押すか、**デバッグ** > **デバッグの開始**の順にクリックして、プロジェクトが正常に編集されるかどうか確認します。 コンパイルが成功すると、MainWindow が **Dynamics 365 にログイン**ボタンと共に表示されます。 ボタンをクリックして共通ログイン コントロールを表示します。  
  
    2.  アプリ用 CDS に接続するための資格情報を提供して認証をテストし、**ログイン**をクリックします。 メッセージにアプリ用 CDS 接続状況が表示されます。  
  
 アプリ用 CDS に接続して種々の操作を実行するための、共通ログイン コントロールのテンプレートを使用するサンプルについては、[サンプル: XRM ツール API のクイック スタート](sample-quick-start-xrm-tooling-api.md) を参照してください。  
  
<a name="Add"></a>

## <a name="add-the-common-login-control-template-to-your-existing-wpf-application"></a>共通ログイン コントロール テンプレートを既存の WPF アプリケーションに追加する

 既に WPF クライアント アプリケーションがある場合は、そのアプリケーションに共通ログイン コントロール テンプレートを簡単に追加して、アプリ用 CDS 認証、資格情報の格納と再利用、および既定のトレースおよびロギングのための、一貫性があるサインイン エクスペリエンスおよび基本コードを実行することができます。 このケースでは、共通ログイン コントロールを呼び出すために、既存のクライアント アプリケーションのユーザー インターフェースでコントロールを作成し、アプリ用 CDS 接続オブジェクトのインスタンスを作成し、その接続オブジェクトを使用してさまざま処理をアプリ用 CDS で実行します。  
  
1.  既存の WPF アプリケーション プロジェクトを Visual Studio でオープンします。 この例では、WPF アプリケーション プロジェクトの名前が SampleWPFApp であると仮定します。  
  
2.  共通ログイン コントロール テンプレートをプロジェクトに追加します。  
  
    1.  **ソリューション エクスプローラー**ウィンドウで、オブジェクト名を右クリックし、**追加** > **新しい項目**の順にクリックします。  
  
    2.  **新しい項目の追加**ダイアログ ボックスの、インストールされているテンプレートの一覧から、**Visual C#** を展開し、**アプリ用 CDS SDK のテンプレート**を選択します。 **WPF アプリケーション用のアプリ用 CDS ログオン フォーム** をクリックし、**OK** をクリックします。  
  
 <!--TODO:
 ![Add the common login control template](../media/crm-sdk-v6-xrmtooling-addtemplate01.png "Add the common login control template")   -->
  
3.  新たに追加された `CrmLoginForm1.xaml` ログイン コントロールは XAML デザイナー領域に表示されます。 表示されない場合は、**ソリューション エクスプローラー** ウィンドウで、`CrmLoginForm1.xaml` ファイルをダブルクリックします。  
  
 <!--TODO: 
![Verify that the login control renders properly](../media/crm-sdk-v6-xrmtooling-addtemplate03.png "Verify that the login control renders properly")   -->
  
4.  ここで、新しく追加したログイン コントロールを、アプリケーションから呼び出す必要があります。 それには、**ボタン**コントロールを `MainWindow.xaml` ファイルに追加し、名前とコンテンツを**btnSignIn**および**アプリ用 CDS にサインイン**それぞれに設定します。  
  
 <!--TODO:
 ![Add a control to call the login form](../media/crm-sdk-v6-xrmtooling-addtemplate02.png "Add a control to call the login form")   -->
  
5.  ボタンをダブルクリックして、`MainWindow.xaml.cs` ファイル内の **btnSignIn** ボタンのクリック イベントにコードを追加します。  
  
6.  以下のサンプル コードを**btnSignIn**ボタンのクリック イベントに追加して `CrmLoginForm1` コントロールを呼出し、アプリ用 CDS 接続オブジェクトのインスタンスを作成します。  
  
    ```csharp
    // Establish the Login control.  
    CRMLoginForm1 ctrl = new CRMLoginForm1();  
  
    // Wire event to login response.   
    ctrl.ConnectionToCrmCompleted += ctrl_ConnectionToCrmCompleted;  
  
    // Show the login control.   
    ctrl.ShowDialog();  
  
    // Handle the returned CRM connection object.  
    // On successful connection, display the CRM version and connected org name   
    if (ctrl.CrmConnectionMgr != null && ctrl.CrmConnectionMgr.CrmSvc != null && ctrl.CrmConnectionMgr.CrmSvc.IsReady)  
    {  
        MessageBox.Show("Connected to CRM! Version: " + ctrl.CrmConnectionMgr.CrmSvc.ConnectedOrgVersion.ToString() +   
        " Org: " + ctrl.CrmConnectionMgr.CrmSvc.ConnectedOrgUniqueName, "Connection Status");  
  
        // Perform your actions here  
    }  
    else  
    {  
        MessageBox.Show("Cannot connect; try again!", "Connection Status");  
    }  
    ```  
  
7.  ボタンのクリック イベントの下に、`ctrl_ConnectionToCrmCompleted` イベントの定義を追加します。  
  
    ```csharp  
    private void ctrl_ConnectionToCrmCompleted(object sender, EventArgs e)  
    {  
        if (sender is CRMLoginForm1)  
        {  
            this.Dispatcher.Invoke(() =>  
            {  
                ((CRMLoginForm1)sender).Close();  
            });  
        }  
    }  
    ```  
  
8.  これが、以前の 2 つの手順でコードを追加した後に、`MainWindow.xaml.cs` ファイルが表示される方法です。  
  
 <!--TODO: ![Sample code](../media/crm-sdk-v6-xrmtooling-addtemplate04.png "Sample code")   -->
  
9. プロジェクトをテストするには:  
  
    1.  プロジェクトを保存して F5 を押すか、**デバッグ** > **デバッグの開始**の順にクリックして、プロジェクトが正常に編集されるかどうか確認します。 コンパイルが成功すると、MainWindow が新しい **アプリ用 CDS にサインイン**ボタンと共に表示されます。 それをクリックして共通ログイン コントロールを表示します。  
  
    2.  アプリ用 CDS に接続するための資格情報を提供して認証をテストし、**ログイン**をクリックします。 成功した場合、バージョンおよび接続する組織名を示すメッセージが表示されます。 **[OK]** をクリックしてメッセージを閉じます。  
  
 <!--TODO:
 ![Project test results](../media/crm-sdk-v6-xrmtooling-addtemplate05.png "Project test results")   -->
  
    3.  再び **Dynamics 365 にサインイン**をクリックすると、アプリケーションから、最後のサインイン活動から保存された資格情報選択するか、新しい資格情報を再入力するように求められます。  
  
 <!--TODO:
 ![Stored credentials](../media/crm-sdk-v6-xrmtooling-addtemplate06.png "Stored credentials")   -->
  
### <a name="see-also"></a>関連項目  

[サンプル: XRM ツール API のクイック スタート](sample-quick-start-xrm-tooling-api.md)<br />
[XRM ツールを使用して Windows のクライアント アプリケーションを作成](build-windows-client-applications-xrm-tools.md)
