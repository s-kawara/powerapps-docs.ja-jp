---
title: CrmServiceClient コンストラクターを使用してアプリ用 CDS に接続する (アプリ用 Common Data Service) | Microsoft Docs
description: CrmServiceClient クラスのインスタンスを作成すると、コンストラクターの 1 つを使用してアプリ用 Common Data Service に接続できます。
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: crm-online
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
ms.assetid: 74862506-a955-4846-a148-ac266f65592f
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
# <a name="use-crmserviceclient-constructors-to-connect-to-cds-for-apps"></a>CrmServiceClient コンストラクターを使用したアプリ用 CDS への接続

アプリ用 CDS に接続するには <xref:Microsoft.Xrm.Tooling.Connector.CrmServiceClient> クラスのインスタンスを作成し、そのコンストラクターの 1 つを使用して接続します。 <xref:Microsoft.Xrm.Tooling.Connector.CrmServiceClient> クラスを使用したアプリ用 CDS への呼び出しはすべてスレッド セーフです。  
  
このトピックで言及したコンストラクター以外にも、 <xref:Microsoft.Xrm.Tooling.Connector.CrmServiceClient> と共に接続文字列を使用してアプリ用 CDS に接続することもできます。 詳細: [XRM ツールの接続文字列を使用してアプリ用 CDS に接続する](use-connection-strings-xrm-tooling-connect.md)  
  
<a name="orgServiceproxy"></a>

## <a name="connect-to-cds-for-apps-using-organizationserviceproxy"></a>OrganizationServiceProxy を使用してアプリ用 CDS に接続する

 ユーザーが提供した <xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceProxy> インスタンスで次のコンストラクタを使用し、アプリ用 CDS に接続する。  
  
```csharp
CrmServiceClient crmSvc = new CrmServiceClient(<externalOrgServiceProxy>);  
```  
  
<a name="orgWebProxyClient"></a>

## <a name="connect-to-cds-for-apps-using-organizationwebproxyclient"></a>OrganizationWebProxyClient を使用してアプリ用 CDS に接続する

 ユーザーが提供した <xref:Microsoft.Xrm.Sdk.WebServiceClient.OrganizationWebProxyClient> インスタンスで次のコンストラクタを使用し、アプリ用 CDS に接続する。  
  
```csharp
CrmServiceClient crmSvc = new CrmServiceClient(<externalOrgWebProxyClient>);  
```  
  
<a name="Office365"></a>

## <a name="connect-to-cds-for-apps-office-365"></a>アプリ用 CDS (Office 365) に接続します

 次のコンストラクターを使用して Office 365 の アプリ用 CDS インスタンスに接続します。  
  
```csharp  
CrmServiceClient crmSvc = new CrmServiceClient("<crmUserId>", CrmServiceClient.MakeSecureString("<crmPassword>"), "<crmRegion>", "<orgName>", useUniqueInstance:false, useSsl:false, <orgDetail>, isOffice365:false);  
```  
  
 `<crmRegion>` パラメーターの有効な値は、`NorthAmerica`、`EMEA`、`APAC`、`SouthAmerica`、`Oceania`、`JPN`、`CAN`、`IND`、および `NorthAmerica2` です。 これを `String.Empty` に設定すると、アプリ用 CDS の組織がすべての領域のサーバーから検索されます。 `<orgName>` パラメーターについては、一意の名前またはわかりやすい名前を指定できます。  
  
 次のパラメーターは任意です。`useUniqueInstance`、`useSsl`、および`orgDetail`。  
  
<a name="Office365oAuth"></a>

## <a name="connect-to-cds-for-apps-office-365-using-oauth"></a>OAuth を使用してアプリ用 CDS (Office 365) に接続する
 
 OAuth プロトコルで Office 365 のアプリ用 CDS インスタンスに接続するには、次のコンストラクターを使用します。 OAuth サポートはアプリ用 CDS で導入されています。  
  
> [!NOTE]
>  グローバル検索は現在すべてのインスタンスを検索し、地域とグローバルをサポートしています。 `OAuth` 認証の種類に対して、 `crmRegion` パラメーター値のグローバルは地域の特別ルールが要求される場所を除きデフォルトで `Online Region  = Don't Know` に設定されます。 ドイツと北米 2 は `Online Region = Don't Know` が選択されている場合にスキャンされません。

```csharp  
CrmServiceClient crmSvc = new CrmServiceClient("<crmUserId>", CrmServiceClient.MakeSecureString("<crmPassword>"), "<crmRegion>", "<orgName>", useUniqueInstance:false, <orgDetail>,  
                  <user>, <clientId>, <redirectUri>, <tokenCachePath>, <externalOrgWebProxyClient>, PromptBehavior.Auto);  
```  
  
 このコンストラクターは、[Microsoft Azure Active Directory 認証ライブラリ (ADAL)](/azure/active-directory/develop/active-directory-authentication-libraries) を使用してユーザーを認証します。 ユーザーの資格情報 (ユーザー名とパスワード) が指定されていない場合は、コンストラクターで指定された `PromptBehavior` パラメーター (任意) に応じて ADAL はユーザーに資格情報を指定するように求めます。 ADAL は OAuth プロトコルを使用して資格情報を認証し、Azure Active Directory からアクセスおよびリフレッシュ トークンを取得します。そしてそのアクセス トークンを使用してアプリ用 CDS に要求を行います。  
  
 `<crmRegion>` パラメーターの有効な値は、`NorthAmerica`、`EMEA`、`APAC`、`SouthAmerica`、`Oceania`、`JPN`、`CAN`、`IND`、および `NorthAmerica2` です。 これを **String.Empty** に設定すると、アプリ用 CDS の組織がすべての領域のサーバーから検索されます。 `<orgName>` パラメーターについては、一意の名前またはわかりやすい名前を指定できます。  
  
<!-- No on-premises or IFD enabled for this version yet
<a name="ActiveDirectory"></a>

## Connect to CDS for Apps on-premises (Active Directory)

Use the following constructor to connect to an on-premises instance with Active Directory authentication.  
  
```csharp  
CrmServiceClient crmSvc = new CrmServiceClient(new System.Net.NetworkCredential("<credential>"), authType, "<hostName>", "<port>", "<orgName>", useUniqueInstance:false, useSsl:false, <orgDetail>);  
  
```  
  
 This will run an Active Directory authentication based on the specified domain. For the `<hostName>` parameter, specify the host name of your CDS for Apps server, for example: `cdstest`. For the `<orgName>` parameter, you can specify either the unique or friendly name.  
The following parameters are optional: `useUniqueInstance`, `useSsl`, and `orgDetail`.  
  
<a name="IFD"></a> 
  
## Connect to CDS for Apps Internet-facing deployment (IFD) 
 
 Use the following constructor to connect to a CDS for Apps IFD instance.  
  
```csharp
CrmServiceClient crmSvc = new CrmServiceClient(new System.Net.NetworkCredential("<credential>"), authType, "<hostName>", "<port>", "<orgName>", useUniqueInstance:false, useSsl:false, <orgDetail>);  
  
```  
  
 This will run a claims-based authentication based on the specified local domain. This is useful for customers that use AD FS, and have configured their CDS for Apps server as claims, where the user population lives in the same AD FS domain as the CDS for Apps server. For the `<hostName>` parameter, specify the host name of your CDS for Apps server, for example, `cdstest`. For the `<orgName>` parameter, you can specify either the unique or friendly name.  
  
 The following parameters are optional: `useUniqueInstance`,  `useSsl`, and `orgDetail`.  
  
<a name="OPoAuth"></a> 

## Connect to CDS for Apps Internet-facing deployment (IFD) using OAuth

 Use the following constructor to use the OAuth protocol in Active Directory Federation Services (AD FS) in Windows Server 2012 R2 to connect to a CDS for Apps IFD instance. For this constructor to work, the computer where CDS for Apps is installed must have been configured to use AD FS 2.2 as the security token service (STS).  
  
```csharp
CrmServiceClient crmSvc = new CrmServiceClient("<crmUserId>", CrmServiceClient.MakeSecureString("<crmPassword>"), "<domain>","<homeRealm>", "<hostName>", "<port>", "<orgName>", useSsl, useUniqueInstance,   
                        <orgDetail>, <user>, <clientId>, <redirectUri>, <tokenCachePath>, externalOrgWebProxyClient, PromptBehavior.Auto);  
  
```  
 The `clientId` and `redirectUri` values for the application supporting OAuth should be registered in the IFD server.  
  
 If the user credentials (user name and password) aren’t specified, ADAL prompts the user to provide the credentials depending on the `PromptBehavior` parameter (optional) specified in the constructor. ADAL authenticates the user using the security token from AD FS, and uses the token to perform actions in CDS for Apps.  
  
<a name="ClaimsBased"></a>
   
## Connect to CDS for Apps (claims-based)
  
 Use the following constructor to use claims-based authentication.  
  
```  
CrmServiceClient crmSvc = new CrmServiceClient(new System.Net.NetworkCredential("<UserId>", "<password>", “<domain>”, "<homeRealm>"),"<hostName>", "<port>", "<orgName>");    
```  
  
 This will run a claims-based authentication against the specified Home realm. This is useful for customers that use AD FS, and have configured their CDS for Apps server as claims, where the user population lives in the same AD FS domain as the CDS for Apps server. For the `<hostName>` parameter, specify the host name of your CDS for Apps server, for example, `cdstest`. For the `<orgName>` parameter, you can specify either the unique or friendly name.  
   -->
  
 ## <a name="connect-to-dynamics-365-online-using-certificate-based-authentication"></a>証明書ベースの認証を使用して Dynamics 365 (online) に接続する
 証明書ベースの認証を使用するには次のコンストラクターを使用します。
 
 ```csharp
 CrmServiceClient CrmSvc = new CrmServiceClient("<certificate>", "<certificateStoreName>", "<certificateThumbPrint>", "<instanceUrl>", <useUniqueInstance>, <orgDetail>, <clientId>, <redirectUri>, <tokenCachePath>);
 ```
 これで証明書ベースの認証を実行します。 アプリケーションの `clientId` と `redirectUri` の値は **Azure Portal** にアプリを登録する際に提供されます。 
 
 次のパラメーターは任意です。`useUniqueInstance`、`useSsl`、および`orgDetail`。
 
<a name="Determine"></a>

## <a name="determine-your-connection-status"></a>接続状態を決定する
 
 接続要求が成功したかどうかを決定するには、<xref:Microsoft.Xrm.Tooling.Connector.CrmServiceClient><xref:Microsoft.Xrm.Tooling.Connector.CrmServiceClient.IsReady>  プロパティ。 **true** の場合、接続が成功し、実行する準備ができています。 それ以外の場合は、接続失敗の原因として、<xref:Microsoft.Xrm.Tooling.Connector.CrmServiceClient>. <xref:Microsoft.Xrm.Tooling.Connector.CrmServiceClient.LastCrmError> および <xref:Microsoft.Xrm.Tooling.Connector.CrmServiceClient>.<xref:Microsoft.Xrm.Tooling.Connector.CrmServiceClient.LastCrmException> プロパティの値を確認します。  
  
### <a name="see-also"></a>関連項目

[XRM ツールの接続文字列を使用してアプリ用 CDS に接続する](use-connection-strings-xrm-tooling-connect.md)<br />
[XRM ツールの Windows PowerShell コマンドレットを使用してアプリ用 CDS に接続する](use-powershell-cmdlets-xrm-tooling-connect.md)<br />
[XRM ツール API を使用してアプリ用 CDS のアクションを実行する](use-xrm-tooling-execute-actions.md)
<xref:Microsoft.Xrm.Tooling.Connector.AuthenticationType><br />
[XRM ツールを使用して Windows のクライアント アプリケーションを作成する](build-windows-client-applications-xrm-tools.md)
<!-- TODO:[Sample: Quick Start for CDS for Apps](../sample-quick-start.md)-->

