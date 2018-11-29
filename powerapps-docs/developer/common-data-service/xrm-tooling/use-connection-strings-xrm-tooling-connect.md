---
title: XRM ツールの接続文字列を使用して、アプリ用 Common Data Serviceに接続する (アプリ用 Common Data Service) | Microsoft Docs
description: XRM ツールは接続文字列を使用することで、アプリ用 Common Data Service の環境に接続することができます
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: crm-online
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
ms.assetid: a98b2fce-df49-4b60-91f4-a4446aa61cd3
caps.latest.revision: 21
author: MattB-msft
ms.author: kvivek
manager: kvivek
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="use-connection-strings-in-xrm-tooling-to-connect-to-common-data-service-for-apps"></a>XRM ツールの接続文字列を使用してアプリ用 Common Data Service に接続する

アプリ用 CDS と共にXRM ツールは、接続文字列を使用してアプリ用 Common Data Service 環境に接続することができます。 これは SQL Server で使用される接続文字列の概念と似ています。 接続文字列は、最大限のセキュリティを得るために構成セクションを暗号化する機能を含むネイティブ サポートを、構成ファイルに備えています。 これによりアプリ用 CDS との接続を展開時に構成することができ、またアプリケーションにハード コーディングすることなくアプリ用 CDS 環境へ接続できます。  
  
<a name="Create"></a> 

## <a name="create-a-connection-string"></a>接続文字列の作成

 以下の例のように、この接続文字列をプロジェクトの app.config または web.config ファイルで指定します。  
  
```xml  
<connectionStrings>  
    <add name="MyCDSServer" connectionString="AuthType=AD;Url=http://contoso:8080/Test;" />  
</connectionStrings>  
```  
  
> [!IMPORTANT]
>  app.config ファイルまたは web.config ファイルにアカウント パスワードなどの機密情報を追加する場合は、適切なセキュリティ対策を講じてその情報を保護してください。  
  
 接続文字列を作成したら、それを使用して <xref:Microsoft.Xrm.Tooling.Connector.CrmServiceClient> オブジェクトを作成します。  
  
```csharp  
//Use the connection string named "MyCDSServer"  
//from the configuration file  
CrmServiceClient crmSvc = new CrmServiceClient(ConfigurationManager.ConnectionStrings["MyCDSServer"].ConnectionString);  
```  
  
> [!NOTE]
>  コード内の以下の `using` ディレクティブを使用して、`System.Configuration` 名前空間を参照し、コード内の接続文字列にアクセスする必要があります: `using System.Configuration;`  
  
 <xref:Microsoft.Xrm.Tooling.Connector.CrmServiceClient> オブジェクトを作成すると、そのオブジェクトを使用してアプリ用 CDS のアクションを実行することができます。 詳細: [XRM ツールを使用してアプリ用 CDS のアクションを実行する](use-xrm-tooling-execute-actions.md)  
  
<a name="Parameters"></a>

## <a name="connection-string-parameters"></a>接続文字列パラメーター

 接続文字列には、セミコロンで区切られた一連の名前=値の組が含まれまています。 次の表は、任意の受注で入力できる、サポートされるパラメーターを一覧表示しています。  
  
|パラメーター名|内容|  
|--------------------|-----------------|  
|ServiceUri、サービス URI、URL、またはサーバー|アプリ用 CDS 環境用にURLを指定します。 URL は、http または https プロトコルを使用することができ、ポートはオプションです。 http プロトコルの既定ポートは 80 で、https プロトコルの既定ポートは 443 です。 サーバー URL の形式は通常 `https://`*`<organization-name>`*`.crm.dynamics.com`です。<br /><br /> 組織名は必須です。|  
|ドメイン|ユーザーの資格情報を検証するドメインを指定します。|  
|UserName、ユーザー名、UserId、または ユーザー ID|資格情報に関連付けられたユーザーの ID 名を指定します。|  
|パスワード|資格情報に関連付けられたユーザー名のパスワードを指定します。|  
|HomeRealmUri またはホームレルムのUri|ホーム レルムの Uri を指定します。|  
|AuthenticationType または AuthType|アプリ用 CDS 環境に接続するために認証の種類を指定します。 有効な値は次のとおりです: `AD`, `IFD` (AD FS 有効化)、`OAuth` または `Office365`。<br /><br /> -   `AD` および `IFD` はアプリ用 CDS の設置型環境でのみ許可されます。<br />-   `OAuth` はアプリ用 CDS および設置型環境で許可されます。<br />-   `Office365` はアプリ用 CDS 環境でのみ許可されます。|  
|RequireNewenvironment|接続がまだアクティブの間に再呼び出しされた場合に、既存の接続を再利用するかどうかを指定します。 既定値は既存の接続が再利用されることを示す `false` です。 `true` に設定した場合、これによりシステムは強制的に固有の接続を作成します。|  
|ClientId、AppId または ApplicationId|Azure Active Directory または Active Directory フェデレーション サービス (AD FS) にアプリケーションを登録したとき割り当てた `ClientID` を指定します。<br /><br /> このパラメータは認証の種類が `OAuth` として指定されている場合にのみ適用されます。|  
|RedirectUri または ReplyUrl|Azure Active Directory または Active Directory フェデレーション サービス (AD FS) に登録したときの、アプリケーションのリダイレクト URI を指定します。<br /><br /> このパラメータは認証の種類が `OAuth` として指定されている場合にのみ適用されます。|  
|TokenCacheStorePath|ユーザー トークンのキャッシュに保存する必要がある場所の完全なパスを指定します。 実行プロセスには指定されたパスへのアクセス権があるべきです。 このパスを設定し構成することが、このプロセスの役割です。<br /><br /> このパラメータは認証の種類が `OAuth` として指定されている場合にのみ適用されます。|  
|LoginPrompt|資格情報が提供されていない場合に資格情報の入力を促すかどうかを指定します。 有効な値は:<br /><br /> -   `Always`: 常に資格情報を指定するようユーザーを促す。<br />-   `Auto`: プロンプトを表示するかどうかを、ログイン コントロール インターフェイスで選択することをユーザーに許可する。<br />-   `Never`: 資格情報を指定するようユーザーを促さない。 使用している接続方法にユーザー インターフェースがない場合は、この値を使用してください。<br /><br /> このパラメータは認証の種類が `OAuth` として指定されている場合にのみ適用されます。|  
|CertStoreName|コンピュータ上でサムプリントが渡された証明書が存在する場所の名前を指定します。 このパラメータは認証の種類が `Certificate` として指定されている場合にのみ適用されます。|
|CertThumbPrint| 使用する証明書のサムプリントを指定します。 このパラメータは認証の種類が `Certificate` として指定されている場合にのみ適用されます。|
|SkipDiscovery|パラメータを true に設定した場合、サービス URI は直接使用してください。| 
  
<a name="Examples"></a>

## <a name="connection-string-examples"></a>接続文字列の例
 
次の例は、別の展開および認証シナリオに接続するための接続文字列の使用方法を示しています。  

<!-- TODO: Get rid of on-premises examples & settings? or just comment them out? -->

<!-- ### Integrated on-premises authentication  
  
```xml
<add name="MyCRMServer" connectionString="AuthType=AD;Url=http://contoso:8080/Test;" />  
```  
  
### Named account using on-premises authentication  
  
```xml  
<add name="MyCRMServer" connectionString="AuthType=AD;Url=http://contoso:8080/Test; Domain=CONTOSO; Username=jsmith; Password=passcode" />  
```  
   -->
### <a name="named-account-using-office-365"></a>Office 365 を使用している取引先企業  
  
```xml
<add name="MyCDSServer" 
 connectionString="
  AuthType=Office365;
  Username=jsmith@contoso.onmicrosoft.com; 
  Password=passcode;
  Url=https://contoso.crm.dynamics.com"/>  
```  
  
### <a name="oauth-using-named-account-in-office-365-with-ux-to-prompt-for-authentication"></a>認証のプロンプトに Office 365 で UX と一緒に取引先企業を使用している OAth  
  
```xml
<add name="MyCDSServer"
 connectionString="
  AuthType=OAuth;
  Username=jsmith@contoso.onmicrosoft.com;
  Password=passcode;
  Url=https://contosotest.crm.dynamics.com;
  AppId=<GUID>;
  RedirectUri =app://<GUID>;
  TokenCacheStorePath =c:\MyTokenCache;
  LoginPrompt=Auto"/>  
```  
  
<!-- ### OAuth using named account in CDS for Apps on-premises with UX to prompt for authentication  
  
```xml
<add name="MyCRMServer" connectionString="AuthType=OAuth;Username=jsmith@contoso.onmicrosoft.com; Password=passcode;Url=https://contoso:8080/Test;AppId=<GUID>;RedirectUri=app://<GUID>;TokenCacheStorePath =c:\MyTokenCache;LoginPrompt=Auto"/>  
```  
  
### IFD using a named account with delegation to a sub realm  
  
```xml
<add name="MyCRMServer" connectionString="AuthType=IFD;Url=http://contoso:8080/Test; HomeRealmUri=https://server-1.server.com/adfs/services/trust/mex/;Domain=CONTOSO; Username=jsmith; Password=passcode" />  
```   -->

### <a name="certificate-based-authentication"></a>クレームベース認証

```xml
<add name="MyCDSServer" 
  connectionString="
  AuthType=Certificate;
  SkipDiscovery=true;
  url={InstanceUri};
  thumbprint={CertThumbPrintId};
  ClientId={AppId};
  RequireNewInstance=true"
  />
```

  
<a name="ConnectionStatus"></a>

## <a name="determine-your-connection-status"></a>接続状態を決定する

 接続要求が成功したかどうかを決定するには、<xref:Microsoft.Xrm.Tooling.Connector.CrmServiceClient><xref:Microsoft.Xrm.Tooling.Connector.CrmServiceClient.IsReady>  プロパティ。 **true** の場合、接続が成功し、実行する準備ができています。 それ以外の場合は、接続失敗の原因として、<xref:Microsoft.Xrm.Tooling.Connector.CrmServiceClient>.<xref:Microsoft.Xrm.Tooling.Connector.CrmServiceClient.LastCrmError> および <xref:Microsoft.Xrm.Tooling.Connector.CrmServiceClient>.<xref:Microsoft.Xrm.Tooling.Connector.CrmServiceClient.LastCrmException> プロパティの値を確認します。  
  
### <a name="see-also"></a>関連項目

[XRM ツールを使用して Windows のクライアント アプリケーションを作成する](build-windows-client-applications-xrm-tools.md)<br />
[CrmServiceClient コンストラクターを使用したアプリ用 CDS への接続](use-crmserviceclient-constructors-connect.md)<br />
[XRM ツールを使用してアプリ用 CDS のアクションを実行する](use-xrm-tooling-execute-actions.md)<br />
<xref:Microsoft.Xrm.Tooling.Connector.CrmServiceClient>
