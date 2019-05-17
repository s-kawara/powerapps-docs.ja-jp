---
title: クライアント アプリケーションで、XRM ツール共通ログイン コントロールを使用する (Common Data Service)| Microsoft Docs
description: Common Data Service SDK では Visual Studio 用テンプレートが用意され、これによりクライアント アプリケーションで共通ログイン コントロールを使用できるようにできます。 Common Data Service 認証、資格情報の保管および検索、および診断ロギングのためのコードがテンプレートに組み込まれ、自分の Common Data Service 用 Windows クライアント アプリケーションで、これらの機能を素早く活用できます。
ms.custom: ''
ms.date: 03/27/2019
ms.reviewer: ''
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
ms.assetid: f77b2a20-0a30-4211-a1d9-74923d3eeae1
caps.latest.revision: 27
author: MattB-msft
ms.author: nabuthuk
manager: kvivek
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="use-the-xrm-tooling-common-login-control-in-your-client-applications"></a>クライアント アプリケーションで、XRM ツール共通ログイン コントロールを使用する

Visual Studio 用テンプレートが用意されており、これによりクライアント アプリケーションで共通ログイン コントロールを使用できるようにできます。 Common Data Service 認証、資格情報の保管および検索、および診断ロギングのためのコードがテンプレートに組み込まれ、自分の Common Data Service 用 Windows クライアント アプリケーションで、これらの機能を素早く活用できます。 共通ログイン コントロールは <xref:Microsoft.Xrm.Tooling.CrmConnectControl> を導入したもので、コントロールは以下の画像のようなものです。  
  
![XRM ツール共通ログイン コントロール](../media/crm-sdk-v6-commonlogincontrol.png "XRM ツール共通ログイン コントロール")
  
<a name="Prereq"></a>

## <a name="prerequisites"></a>前提条件
  
- .NET Framework 4.6.2 以上。
- Visual Studio 2017 (推奨)
- プロジェクト テンプレート使用時に必要な Nuget パッケージをダウンロード/復元できるように、インターネットに接続していること。  
  
<a name="NewProjectUsingTemplate"></a>
   
## <a name="create-a-wpf-application-using-the-common-login-control-template"></a>共通ログイン コントロール テンプレートを使用した WPF アプリケーションの作成
  
これは、認証、資格情報の保管と再利用、および既定のトレースまたはロギングのために、共通ログイン コントロールおよび基本コード活用する **Windows Presentation Foundation (WPF)** アプリケーションを、素早く作成する方法です。  
  
1.  Visual Studio を起動し、新しいプロジェクトを作成します。  
2.  **新しいプロジェクト** ダイアログ ボックスで以下を実行します。  
    1.  インストールされたテンプレートの一覧から **Visual C#** を展開して、**Common Data Service SDK のテンプレート** を選択します。  
    2.  **.NET Framework 4.6.2** が選択されていることを確認します。  
    3.  **Dynamics 365 用 WPF アプリケーション**を選択します。  
    4.  プロジェクトの名前と場所を指定し、**OK** をクリックします。  
  
     > [!div class="mx-imgBorder"]
     > ![Common Data Service テンプレート用の WPF アプリケーション](../media/crm-sdk-v6-xrm-tooling-newproject.png "Common Data Service テンプレート用の WPF アプリケーション")   

> [!NOTE]
> **Visual Studio 2015 に関する既知の問題**
> 
> VS 2015 のデバッグモードでプロジェクト/ソリューションを実行していると、接続できなくなることがあります。 これは、4.6.2 以降のターゲットフレームワークを使用しているかどうかにかかわらず発生します。 これは、Visual Studio ホスティングプロセスが .NET 4.5 に対してコンパイルされているために発生します。これは既定で TLS 1.2 がサポートされていないことを意味します。 回避策として、Visual Studio ホスティング プロセスを無効にできます。 
>
> Visual Studio でプロジェクトの名前を右クリックしてから、**プロパティ**をクリックします。 **デバッグ**タブで、**Visual Studio ホスティング プロセスの無効化**オプションをオフにできます。 
>
> これは、VS 2015 のデバッグ エクスペリエンスにのみ影響を与えます。 これは構築されるバイナリまたは実行可能ファイルには影響しません。 同じ問題は、Visual Studio 2017 では発生しません。
  
3. プロジェクトをテストするには:
  
    1. プロジェクトを保存して **F5** を押すか、**デバッグ** > **デバッグの開始** の順にクリックして、プロジェクトが正常にコンパイルされるか確認します。 コンパイルが成功すると、MainWindow が **Dynamics 365 にログイン**ボタンと共に表示されます。 ボタンをクリックして共通ログイン コントロールを表示します。  

    2.  Common Data Service に接続するための資格情報を提供して認証をテストし、**ログイン** をクリックします。 メッセージに Common Data Service の接続状態が表示されます。  

  
 Common Data Service に接続して種々の操作を実行する共通ログイン コントロールのテンプレートを使用するサンプルについては、[サンプル: XRM ツール API のクイック スタート](sample-quick-start-xrm-tooling-api.md) を参照してください。  
  
<a name="Add"></a>

## <a name="add-the-common-login-control-template-to-your-existing-wpf-application"></a>共通ログイン コントロール テンプレートを既存の WPF アプリケーションに追加する

 既に WPF クライアント アプリケーションがある場合は、そのアプリケーションに共通ログイン コントロール テンプレートを簡単に追加して、Common Data Service 認証、資格情報の格納と再利用、および既定のトレースおよびロギングのための、一貫性があるサインイン エクスペリエンスおよび基本コードを実行することができます。 このケースでは、共通ログイン コントロールを呼び出すために、既存のクライアント アプリケーションのユーザー インターフェースでコントロールを作成し、Common Data Service 接続オブジェクトのインスタンスを作成し、その接続オブジェクトを使用してさまざま処理を Common Data Service で実行します。  
  
1. 既存の WPF アプリケーション プロジェクトを Visual Studio でオープンします。 この例では、WPF アプリケーション プロジェクトの名前が `SampleWPFApp` であると仮定します。  
  
2. 共通ログイン コントロール テンプレートをプロジェクトに追加します。  
  
    1. **ソリューション エクスプローラー**ウィンドウで、オブジェクト名を右クリックし、**追加** > **新しい項目**の順にクリックします。  
  

    2.  **新しい項目の追加** ダイアログ ボックスの、インストールされているテンプレートの一覧から、**Visual C#** を展開し、**Common Data Service SDK のテンプレート** を選択します。 **WPF アプリケーション用 Common Data Service のログイン フォーム** をクリックし、**OK** をクリックします。  

          > [!div class="mx-imgBorder"]
          > ![共通ログイン コントロール テンプレートの追加](../media/crm-sdk-v6-xrmtooling-addtemplate01.png "共通ログイン コントロール テンプレートの追加")
  
3. 新たに追加された `CrmLoginForm1.xaml` ログイン コントロールは XAML デザイナー領域に表示されます。 表示されない場合は、**ソリューション エクスプローラー**ウィンドウで、`CrmLoginForm1.xaml` ファイルをダブルクリックします。  
  
    > [!div class="mx-imgBorder"]
    > ![ログインのコントロールが適切に表示されるか検証](../media/crm-sdk-v6-xrmtooling-addtemplate03.png "ログインのコントロールが適切に表示されるか検証")
  

4.  ここで、新しく追加したログイン コントロールを、アプリケーションから呼び出す必要があります。 それには、**ボタン** コントロールを `MainWindow.xaml` ファイルに追加し、名前とコンテンツを **btnSignIn** および **Common Data Service にサインイン** それぞれに設定します。  
 
     > [!div class="mx-imgBorder"]
     > ![ログイン フォームを呼び出すコントロールを追加](../media/crm-sdk-v6-xrmtooling-addtemplate02.png "ログイン フォームを呼び出すコントロールを追加")
  
5. ボタンをダブルクリックして、`MainWindow.xaml.cs` ファイル内の **btnSignIn** ボタンのクリック イベントにコードを追加します。  
  
6.  以下のサンプル コードを **btnSignIn** ボタンのクリック イベントに追加して `CrmLoginForm1` コントロールを呼び出し、Common Data Service 接続オブジェクトのインスタンスを作成します。  
 
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
  
7. ボタンのクリック イベントの下に、`ctrl_ConnectionToCrmCompleted` イベントの定義を追加します。  
  
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
  
8. これが、以前の 2 つの手順でコードを追加した後に、`MainWindow.xaml.cs` ファイルが表示される方法です。

    > [!div class="mx-imgBorder"]
    > ![サンプル コード](../media/crm-sdk-v6-xrmtooling-addtemplate04.png "サンプル コード")
  
9. プロジェクトをテストするには:  
  
    1.  プロジェクトを保存して F5 を押すか、**デバッグ** > **デバッグの開始**の順にクリックして、プロジェクトが正常に編集されるかどうか確認します。 コンパイルが成功すると、MainWindow が新しい **Common Data Service にサインイン** ボタンと共に表示されます。 それをクリックして共通ログイン コントロールを表示します。  
  
    2.  Common Data Service に接続するための資格情報を提供して認証をテストし、**ログイン** をクリックします。 成功した場合、バージョンおよび接続する組織名を示すメッセージが表示されます。 **OK** をクリックしてメッセージを閉じます。  
  
 
    > [!div class="mx-imgBorder"]
    > ![プロジェクトのテスト結果](../media/crm-sdk-v6-xrmtooling-addtemplate05.png "プロジェクトのテスト結果") 

  
    3. 再び **Dynamics 365 にサインイン**をクリックすると、アプリケーションから、最後のサインイン活動から保存された資格情報選択するか、新しい資格情報を再入力するように求められます。  
  
        > [!div class="mx-imgBorder"]
        > ![保存された資格情報](../media/crm-sdk-v6-xrmtooling-addtemplate06.png "保存された資格情報")
  
### <a name="see-also"></a>関連項目  

[サンプル: XRM ツール API のクイック スタート](sample-quick-start-xrm-tooling-api.md)<br />
[XRM ツールを使用して Windows のクライアント アプリケーションを作成](build-windows-client-applications-xrm-tools.md)
