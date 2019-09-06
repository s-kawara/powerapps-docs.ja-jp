---
title: 'サンプル: 簡易接続のクイック スタート ( Common Data Service の開発者ガイド) | MicrosoftDocs'
description: 'この例では、CrmServiceClientを使用して Common Data Service Webサービスに接続し、エンティティに対して基本的な作成、更新、取得、削除の処理を実行する方法を説明します。 '
ms.custom: null
ms.date: 03/27/2019
author: Nkrb
ms.service: crm-online
ms.suite: null
ms.tgt_pltfrm: null
ms.topic: samples
applies_to:
  - Common Data Service (online)
ms.assetid: a4fb3634-948e-4bac-a32f-f626c78d83a0
caps.latest.revision: 29
ms.author: nabuthuk
manager: kvivek
search.audienceType:
  - developer
search.app:
  - D365CE
  - PowerApps
---
# <a name="sample-simplified-connection-quick-start-using-common-data-service"></a>サンプル: Common Data Service を使用した単純化接続のクイック スタート

この例では、 <xref:Microsoft.Xrm.Tooling.Connector.CrmServiceClient> を使用して Common Data Service Webサービスに接続し、エンティティーに対する基本的な作成、更新、取得、削除の処理を実行する方法を示します。 <xref:Microsoft.Xrm.Tooling.Connector.CrmServiceClient> の詳細については、 [CrmServiceClient コンストラクターを使用して Common Data Serviceに接続する](use-crmserviceclient-constructors-connect.md) を参照してください。

## <a name="requirements"></a>要件

完全なサンプル コードはこちら [サンプル: Common Data Service のクイック スタート](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/Xrm%20Tooling/QuickStartCS) 

サンプルを実行する前に、 Common Data Service インスタンスの接続情報を使用して `app.config` ファイルを変更する必要があります。 

## <a name="demonstrates"></a>説明

このサンプルでは、<xref:Microsoft.Xrm.Tooling.Connector.CrmServiceClient>およびメソッドを使って Common Data Service Web サービスでユーザーを認証します。 組織 Web サービスの参照を取得した後、このサンプルでは `account` エンティティで基本作成、更新、取得、削除を実行します。 サンプルでは、一般的な例外も処理します。 ヘルパー コードは、組織 Web サービスへのつながりの確立に使用されません。  

さらに、このサンプルでは `OAuth` 認証の種類および詳細な接続診断がサポートされています。 診断の使用に関する詳細については、「[XRMツールのトレースの構成](configure-tracing-xrm-tooling.md)」を参照してください。

## <a name="example"></a>例

以下にサンプル `app.config file` を示します。 これを使用するには、サーバーおよび組織に関連する行の、\<add … /> 行の始めにあるコメント文字列 “<!- -” および行の最後にある “- ->” を削除します。 次に、組織に適切な属性値に変更します。

```xml
<?xml version="1.0" encoding="utf-8"?>  
<configuration>  
  <connectionStrings>  
    <!-- Online using Office 365 -->  
    <!-- <add name="Server=CRM Online, organization=contoso, user=someone"  
         connectionString="Url=https://contoso.crm.dynamics.com; Username=someone@contoso.onmicrosoft.com; Password=password; authtype=Office365"/> -->  
  </connectionStrings>  
  <startup>  
    <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.6.2" />  
  </startup>  
<system.diagnostics>  
    <trace autoflush="true"/>  
    <sources>  
      <source name="Microsoft.Xrm.Tooling.Connector.CrmServiceClient" switchName="Microsoft.Xrm.Tooling.Connector.CrmServiceClient" switchType="System.Diagnostics.SourceSwitch">  
        <listeners>  
          <add name="console" type="System.Diagnostics.ConsoleTraceListener"/>  
          <add name="fileListener"/>  
        </listeners>  
      </source>  
      <source name="Microsoft.Xrm.Tooling.CrmConnectControl" switchName="Microsoft.Xrm.Tooling.CrmConnectControl" switchType="System.Diagnostics.SourceSwitch">  
        <listeners>  
          <add name="console" type="System.Diagnostics.ConsoleTraceListener"/>  
          <add name="fileListener"/>  
        </listeners>  
      </source>  
      <source name="CrmSvcUtil" switchName="CrmSvcUtil" switchType="System.Diagnostics.SourceSwitch">  
        <listeners>  
          <add name="console" type="System.Diagnostics.ConsoleTraceListener"/>  
          <add name="fileListener"/>  
        </listeners>  
      </source>  
    </sources>  
    <switches>  

      <!--Possible values for switches: Off, Error, Warning, Information, Verbose  
                        Verbose:      includes Error, Warning, Info, Trace levels  
                        Information:  includes Error, Warning, Info levels  
                        Warning:      includes Error, Warning levels  
                        Error:        includes Error level-->  

      <add name="Microsoft.Xrm.Tooling.CrmConnectControl" value="Off"/>  
      <add name="Microsoft.Xrm.Tooling.Connector.CrmServiceClient" value="Error"/>  
      <add name="CrmSvcUtil" value="Off"/>  
    </switches>  

    <sharedListeners>  
      <add name="fileListener" type="System.Diagnostics.TextWriterTraceListener" initializeData="CrmSvcUtil.log"/>  
    </sharedListeners>  

  </system.diagnostics>  
  <runtime>  
    <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
      <dependentAssembly>  
        <assemblyIdentity name="Microsoft.Xrm.Sdk" publicKeyToken="31bf3856ad364e35" culture="neutral" />  
        <bindingRedirect oldVersion="0.0.0.0-7.0.0.0" newVersion="8.0.0.0" />  
      </dependentAssembly>  
      <dependentAssembly>  
        <assemblyIdentity name="Microsoft.Xrm.Sdk.Deployment" publicKeyToken="31bf3856ad364e35" culture="neutral" />  
        <bindingRedirect oldVersion="0.0.0.0-7.0.0.0" newVersion="8.0.0.0" />  
      </dependentAssembly>  
      <dependentAssembly>  
        <assemblyIdentity name="Microsoft.ServiceBus" publicKeyToken="31bf3856ad364e35" culture="neutral" />  
        <bindingRedirect oldVersion="0.0.0.0-2.4.0.0" newVersion="2.4.0.0" />  
      </dependentAssembly>  
    </assemblyBinding>  
  </runtime>  
</configuration>  
```

## <a name="example"></a>例

```csharp
using Microsoft.Crm.Sdk.Messages;
using Microsoft.Xrm.Sdk;
using Microsoft.Xrm.Sdk.Query;
using Microsoft.Xrm.Tooling.Connector;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace PowerApps.Samples
{
   public partial class SampleProgram
    {
        [STAThread] // Added to support UX
        static void Main(string[] args)
        {
            CrmServiceClient service = null;

            try
            {
                service = SampleHelpers.Connect("Connect");
                if (service.IsReady)
                {
                    #region Sample Code
                    ////////////////////////////////////
                    #region Set up
                    SetUpSample(service);
                    #endregion Set up
                    #region Demonstrate
                    // Obtain information about the logged on user from the web service.
                    Guid userid = ((WhoAmIResponse)service.Execute(new WhoAmIRequest())).UserId;
                    SystemUser systemUser = (SystemUser)service.Retrieve("systemuser", userid,
                        new ColumnSet(new string[] { "firstname", "lastname" }));
                    Console.WriteLine("Logged on user is {0} {1}.", systemUser.FirstName, systemUser.LastName);

                    // Retrieve the version of Microsoft Dynamics CRM.
                    RetrieveVersionRequest versionRequest = new RetrieveVersionRequest();
                    RetrieveVersionResponse versionResponse =
                        (RetrieveVersionResponse)service.Execute(versionRequest);
                    Console.WriteLine("Microsoft Dynamics CRM version {0}.", versionResponse.Version);

                    // Instantiate an account object. Note the use of option set enumerations defined in OptionSets.cs.
                    // Refer to the Entity Metadata topic in the SDK documentation to determine which attributes must
                    // be set for each entity.
                    Account account = new Account { Name = "Fourth Coffee" };
                    account.AccountCategoryCode = new OptionSetValue((int)AccountAccountCategoryCode.PreferredCustomer);
                    account.CustomerTypeCode = new OptionSetValue((int)AccountCustomerTypeCode.Investor);

                    // Create an account record named Fourth Coffee.
                    _accountId = service.Create(account);

                    Console.Write("{0} {1} created, ", account.LogicalName, account.Name);

                    // Retrieve the several attributes from the new account.
                    ColumnSet cols = new ColumnSet(
                        new String[] { "name", "address1_postalcode", "lastusedincampaign" });

                    Account retrievedAccount = (Account)service.Retrieve("account", _accountId, cols);
                    Console.Write("retrieved, ");

                    // Update the postal code attribute.
                    retrievedAccount.Address1_PostalCode = "98052";

                    // The address 2 postal code was set accidentally, so set it to null.
                    retrievedAccount.Address2_PostalCode = null;

                    // Shows use of a Money value.
                    retrievedAccount.Revenue = new Money(5000000);

                    // Shows use of a Boolean value.
                    retrievedAccount.CreditOnHold = false;

                    // Update the account record.
                    service.Update(retrievedAccount);
                    Console.WriteLine("and updated.");

                #region Clean up
                CleanUpSample(service);
                    #endregion Clean up
                }
                #endregion Demonstrate
                #endregion Sample Code
                else
                {
                    const string UNABLE_TO_LOGIN_ERROR = "Unable to Login to Dynamics CRM";
                    if (service.LastCrmError.Equals(UNABLE_TO_LOGIN_ERROR))
                    {
                        Console.WriteLine("Check the connection string values in cds/App.config.");
                        throw new Exception(service.LastCrmError);
                    }
                    else
                    {
                        throw service.LastCrmException;
                    }
                }
            }
            catch (Exception ex)
            {
                SampleHelpers.HandleException(ex);
            }

            finally
            {
                if (service != null)
                    service.Dispose();

                Console.WriteLine("Press <Enter> to exit.");
                Console.ReadLine();
            }
        }
            }
}

```

### <a name="see-also"></a>関連項目

[XRMツールの接続文字列を使用して Common Data Serviceに接続する](use-connection-strings-xrm-tooling-connect.md)<br />
[サンプル: XRM ツール API のクイック スタート](sample-quick-start-xrm-tooling-api.md)<br />
