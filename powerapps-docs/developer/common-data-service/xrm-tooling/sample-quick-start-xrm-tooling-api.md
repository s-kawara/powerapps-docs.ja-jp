---
title: 'サンプル: XRM ツール API のクイック スタート (Common Data Service)| Microsoft Docs'
description: ''
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: samples
applies_to:
  - Dynamics 365 (online)
ms.assetid: 060d45bb-b7fd-48bd-ab8f-629c1b8bc1dc
caps.latest.revision: 20
author: MattB-msft
ms.author: kvivek
manager: kvivek
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="sample-quick-start-for-xrm-tooling-api"></a>サンプル: XRM ツール API のクイック スタート

クイックスタート サンプルは、XRM ツール API を使用して Common Data Service インスタンスに接続し、作成、更新、取得、削除などエンティティでの基本的な操作方法を表す .NET Framework マネージド コード サンプルです。 XRM ツールの詳細については、「[XRM ツールを使用して Windows のクライアント アプリケーションを作成](build-windows-client-applications-xrm-tools.md)」を参照してください。

サンプルのダウンロード: [XRM ツール API に関する作業](https://code.msdn.microsoft.com/XRM-Tooling-Sample-24a5c55c)。

## <a name="prerequisites"></a>前提条件

[!INCLUDE [sdk-prerequisite](../../../includes/sdk-prerequisite.md)]
  
## <a name="requirements"></a>要件

Common Data Service 環境にアクセスする必要があります。

## <a name="demonstrates"></a>説明

- このサンプル コードは、共通ログイン コントロールに対して認証と資格情報のキャッシュと再利用の組み込みのサポートを提供する、**CRM 用 WPF アプリケーション** SDK テンプレートを使用して作成されます。 Visual Studio の共通ログイン コントロールおよび SDK テンプレートの使用方法の詳細については、[XRM ツール共通ログイン コントロールを使用する](use-xrm-tooling-common-login-control-client-applications.md)を参照してください。  
- ヘルパー コードは、Common Data Service への接続を確立するために使用されません。  
- Common Data Service に接続後、このサンプルは、取引先企業エンティティに対して、基本的な作成、更新、取得、および削除操作を行います。  
- サンプルが初めて実行されるとき、ユーザーの資格情報を `c:\Users\`*`<username>`*`\AppData\Roaming\Microsoft\QuickStartXRMToolingWPFClient` フォルダーの構成ファイル (`Default_QuickStartXRMToolingWPFClient.exe.config`) に保存し、その後、Common Data Service にサインインするために、ユーザーが保存された資格情報を使用するか、新しい資格情報を使用するかを実行時に求めます。  
- 問題が発生した場合、トラブルシューティングを助けるために、次のログ ファイルを生成します。  
- Login_ErrorLog.log: サインイン エラーを報告するため。 このファイルは、`C:\Users\`*`<username>`*`\AppData\Roaming\Microsoft\QuickStartXRMToolingWPFClient` にあります。  
- QuickStartXRMToolingWPFClient.log: 操作エラーを報告するため。 このファイルは、実行可能ファイルと同じ場所の、自分の Visual Studio プロジェクトのデバッグ フォルダーで使用できます。  

## <a name="to-run-the-sample"></a>サンプルを実行するには

1. サンプルをダウンロードし、展開します。  
1. `Quick start for XRM Tooling\C#\QuickStartXRMToolingWPFClient.sln` ファイル Visual Studio で開きます。  
2. **F5** キーを押して、プログラムをコンパイルして実行します。  

## <a name="example"></a>例

```csharp  
using System;  
using System.Collections.Generic;  
using System.Linq;  
using System.Text;  
using System.Threading.Tasks;  
using System.Windows;  
using System.Windows.Controls;  
using System.Windows.Data;  
using System.Windows.Documents;  
using System.Windows.Input;  
using System.Windows.Media;  
using System.Windows.Media.Imaging;  
using System.Windows.Navigation;  
using System.Windows.Shapes;  
  
// This namespace is automatically added for using   
// components in LoginWindow\CrmLogin.xaml (common login control).  
using QuickStartXRMToolingWPFClient.LoginWindow;  
  
// Add this namespace for performing   
// various operations in CRM.  
using Microsoft.Xrm.Tooling.Connector;  
  
namespace QuickStartXRMToolingWPFClient  
{  
    /// <summary>  
    /// Demonstrates how to do basic entity operations like create, retrieve,  
    /// update, and delete using the XRM Tooling APIs and the common login  
    /// control.</summary>  
    /// <remarks>  
    /// At run-time, you will be given the option to delete all the  
    /// database records created by this program.</remarks>  
    public partial class MainWindow : Window  
    {  
        public MainWindow()  
        {  
            InitializeComponent();  
            btnDelete.Visibility = Visibility.Hidden;  
        }  
  
        #region Class Level Members  
  
        private CrmLogin _ctrl = null;  
        private Guid _accountId;  
  
        #endregion Class Level Members  
  
        #region How To Sample Code  
  
        /// <summary>  
        /// Connect to Microsoft CRM, and get an instance of CRMServiceClient   
        /// </summary>  
  
        private void LoginButton_Click(object sender, RoutedEventArgs e)  
        {  
            // Create an instance of the XRM Tooling common login control  
            _ctrl = new CrmLogin();  
  
            /// Wire event to the CRM sign-in response.   
            _ctrl.ConnectionToCrmCompleted += ctrl_ConnectionToCrmCompleted;  
            UpdateStatus("Initiating connection to CRM...");  
  
            /// Show the XRM Tooling common login control.   
            _ctrl.ShowDialog();  
  
            /// Validate if you are connected to CRM   
            if (_ctrl.CrmConnectionMgr != null && _ctrl.CrmConnectionMgr.CrmSvc != null && _ctrl.CrmConnectionMgr.CrmSvc.IsReady)  
            {  
                UpdateStatus("Connected to CRM! (Version: " + _ctrl.CrmConnectionMgr.CrmSvc.ConnectedOrgVersion.ToString() +   
                    "; Org: " + _ctrl.CrmConnectionMgr.CrmSvc.ConnectedOrgUniqueName.ToString() + ")");  
                UpdateStatus("***************************************");  
                UpdateStatus("Click Start to create, retrieve, update, and delete (optional) an account record.");  
                btnSignIn.IsEnabled = false;  
                btnCRUD.IsEnabled = true;  
            }  
            // If you are not connected to CRM; display the last error and last CRM excption  
            else  
            {  
                UpdateStatus("The connection to CRM failed or was cancelled by the user.");              
            }              
        }  
  
        private void btnCRUD_Click(object sender, RoutedEventArgs e)  
        {  
            // Create an account record  
            Dictionary<string, CrmDataTypeWrapper> inData = new Dictionary<string, CrmDataTypeWrapper>();  
            inData.Add("name", new CrmDataTypeWrapper("Sample Account Name", CrmFieldType.String));  
            inData.Add("address1_city", new CrmDataTypeWrapper("Redmond", CrmFieldType.String));  
            inData.Add("telephone1", new CrmDataTypeWrapper("555-0160", CrmFieldType.String));  
            _accountId = _ctrl.CrmConnectionMgr.CrmSvc.CreateNewRecord("account", inData);  
  
            // Validate if the account is created, and then retrieve it  
            if (_accountId != Guid.Empty)  
            {  
                UpdateStatus("***************************************");  
                UpdateStatus(DateTime.Now.ToString() + ": Created an account with the following" + "\n" + "details, and retrieved it:");  
                Dictionary<string, object> data = _ctrl.CrmConnectionMgr.CrmSvc.GetEntityDataById("account", _accountId, null);  
                foreach (var pair in data)  
                {  
                    if ((pair.Key == "name") || (pair.Key == "address1_city") || (pair.Key == "telephone1"))  
                    {  
                        UpdateStatus(pair.Key.ToUpper() + ": " + pair.Value);  
                    }  
                }  
                btnCRUD.IsEnabled = false;  
            }  
            else  
            {  
                UpdateStatus("***************************************");  
                UpdateStatus("Could not create the account.");  
            }  
  
            // Update the account record  
            Dictionary<string, CrmDataTypeWrapper> updateData = new Dictionary<string, CrmDataTypeWrapper>();  
            updateData.Add("name", new CrmDataTypeWrapper("Updated Sample Account Name", CrmFieldType.String));  
            updateData.Add("address1_city", new CrmDataTypeWrapper("Boston", CrmFieldType.String));  
            updateData.Add("telephone1", new CrmDataTypeWrapper("555-0161", CrmFieldType.String));   
            bool updateAccountStatus = _ctrl.CrmConnectionMgr.CrmSvc.UpdateEntity("account","accountid",_accountId,updateData);  
  
            // Validate if the account record was updated successfully, and then display the updated information  
            if (updateAccountStatus == true)  
            {  
                UpdateStatus("***************************************");  
                UpdateStatus(DateTime.Now.ToString() + ": Updated the account details as follows:");  
                Dictionary<string, object> data = _ctrl.CrmConnectionMgr.CrmSvc.GetEntityDataById("account", _accountId, null);  
                foreach (var pair in data)  
                {  
                    if ((pair.Key == "name") || (pair.Key == "address1_city") || (pair.Key == "telephone1"))  
                    {  
                        UpdateStatus(pair.Key.ToUpper() + ": " + pair.Value);  
                    }  
                }  
            }  
            else  
            {  
                UpdateStatus("***************************************");  
                UpdateStatus("Could not update the account.");  
            }  
  
            // Prompt the user to delete the account record created in the sample  
            UpdateStatus("***************************************");  
            UpdateStatus("To delete the account record created by the sample, click Delete Record.");  
            UpdateStatus("Otherwise, click Exit to close the sample application.");  
            btnDelete.Visibility = Visibility.Visible;          
        }  
  
        // Delete the account record created in this sample.  
        private void btnDelete_Click(object sender, RoutedEventArgs e)  
        {  
            btnDelete.IsEnabled = false;  
            _ctrl.CrmConnectionMgr.CrmSvc.DeleteEntity("account", _accountId);  
            UpdateStatus("***************************************");  
            UpdateStatus(DateTime.Now.ToString() + ": Deleted the account record.");  
            UpdateStatus("Click Exit to close the sample application.");  
        }  
  
        // Exit the sample application  
        private void btnExit_Click(object sender, RoutedEventArgs e)  
        {  
            this.Close();  
        }  
  
        /// <summary>  
        /// Progressively displays the status messages about the actions  
        /// performed during the running of the sample.  
        /// <param name="updateText">Indicates the status string that needs to be   
        /// displayed to the user.</param>  
        /// </summary>  
        public void UpdateStatus(string updateText)  
        {  
            if (lblStatus.Content.ToString() != String.Empty)  
            {  
                lblStatus.Content = lblStatus.Content + "\n" + updateText;  
            }  
            else  
            {  
                lblStatus.Content = updateText;  
            }  
        }  
  
        /// <summary>  
        /// Raised when the login process is completed.  
        /// </summary>  
        private void ctrl_ConnectionToCrmCompleted(object sender, EventArgs e)  
        {  
            if (sender is CrmLogin)  
            {  
                this.Dispatcher.Invoke(() =>  
                {  
                    ((CrmLogin)sender).Close();  
                });  
            }  
        }  
    }  
    #endregion How To Sample Code  
  
}  
```

### <a name="see-also"></a>関連項目

[XRM ツール共通ログイン コントロールを使用する](use-xrm-tooling-common-login-control-client-applications.md)<br />
[XRM ツールを使用して Windows のクライアント アプリケーションを作成する](build-windows-client-applications-xrm-tools.md)<br />
<!-- TODO:
[Tutorials for Learning About Common Data Service Development](../tutorials-resources-sdk.md)<br /> -->
