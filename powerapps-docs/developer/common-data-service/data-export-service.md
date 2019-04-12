---
title: データ エクスポート サービス (Common Data Service) | Microsoft Docs
description: データ エクスポート サービスの機能、前提条件、API、およびプログラミング。
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: sabinn-msft
ms.author: jdaly
manager: ryjones
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="data-export-service"></a>データ エクスポート サービス

データ エクスポートは顧客所有の Microsoft Azure サブスクリプションで、Common Data Service データを Microsoft Azure SQL データベース ストアに複製する機能を追加する Common Data Service ソリューションを使用可能にするアドオン サービスです。 サポートされている対象先は、Microsoft Azure SQL データベースと Microsoft Azure 仮想マシン上の Microsoft Azure SQL サーバーです。 データ エクスポートは Dynamics 365 スキーマとデータ全体をインテリジェントに同期処理し、その後、Dynamics 365 (オンライン) システムで変更 (差分変更) が発生すると、継続的に同期処理します。  
  
 データ エクスポート サービスでは、構成管理と Common Data Service 内からのサービスの継続的な管理のインターフェイスを提供します。  詳細については、[データのエクスポート](https://technet.microsoft.com/library/a70feedc-12b9-4a2d-baf0-f489cdcc177d) を参照してください。 このトピックでは、対応しているプログラム インターフェイスとこのサービスの問題を説明します。  
  
## <a name="prerequisites-for-using-the-data-export-service"></a>データ エクスポート サービスを使用するための前提条件  
 このサービスは Common Data Service から外部の Microsoft Azure SQL データベースへアクセスすることが必要であるため、このサービスに正常にアクセスするには、さまざまな前提条件を満たす必要があります。 次の前提条件は、[データ エクスポート サービスを使用するための前提条件](https://technet.microsoft.com/library/mt744592.aspx) のセクションで管理者の観点からより完全に説明されます。  
  
 Common Data Service サービスは次のように構成する必要があります:  
  
- エクスポートされるエンティティは、変更の追跡で有効になります。 詳細については、[変更の追跡を使用してデータを外部システムに同期](use-change-tracking-synchronize-data-external-systems.md) を参照してください。  
  
- コードは、システム管理者セキュリティ ロールを持つユーザーのコンテキストで実行されます。  
  
> [!NOTE]
>  このサービスにアクセスするプログラムは、データ エクスポートの管理ソリューションに関連付けられたインストールが必要では*ありません*ということに注意してください。  
  
 ターゲットの Azure SQL データベースは、次のように構成する必要があります:  
  
- サブスクリプションは Common Data Service インスタンスから複製されたデータ量をサポートする必要があります。  
  
- ファイアウォール設定は、データ エクスポート サービスの IP アドレスからアクセスを許可する必要があります。 詳細については、[Azure ポータルを使用する Azure SQL データベース サーバー レベルのファイアウォール ルールの構成](https://azure.microsoft.com/en-us/documentation/articles/sql-database-configure-firewall-settings/) を参照してください。  
  
- [azure services へのアクセスの許可] オプションを有効にすることをお勧めします。  
  
- データ エクスポート接続文字列で指定されたデータベース ユーザーは、ターゲット データベースで適切な作成、および変更アクセス許可を持っている必要があります。  少なくともこれらには次のものが含まれます: `CRTB`、`CRTY`、`CRVW`、`CRPR`、および `ALUS`。 詳細については、[アクセス許可 (データベース エンジン)](https://msdn.microsoft.com/en-us/library/ms191291.aspx) を参照してください。  
  
- 少なくとも1人のユーザーは、スキーマで全面的なアクセス許可があります。 次のスクリプトでは、新しいユーザーが作成されます。  
  
```sql  
  
USE MASTER;  
CREATE LOGIN NewUser WITH PASSWORD='newpassword';  
  
USE DESTINATIONDATABASE;  
CREATE USER NewUser FOR LOGIN NewUser  
GRANT CREATE TABLE, CREATE TYPE, CREATE VIEW, CREATE PROCEDURE, ALTER ANY USER to NewUser  
GRANT ALTER, REFERENCES, INSERT, DELETE, UPDATE, SELECT, EXECUTE ON SCHEMA::dbo TO NewUser  
  
```  
  
オンライン ソリューションとサービスの場合、Azure は、[Key Vault](https://azure.microsoft.com/en-us/services/key-vault/) サービスを使用して、暗号鍵、パスワード、およびその他の秘密を保護します。  Azure Key Vault を使用するには、アクセス許可が「Dynamics 365 データ エクスポート サービス」に与えられ、SQL Azure 接続文字列を安全に保存するために使用されるように、この顧客所有のサービスを設定する必要があります。 PowerShell スクリプトでこの構成を行うには、[Azure Key Vault の設定方法](https://technet.microsoft.com/library/mt744592.aspx) を参照してください。 また、このサービスは REST API を使用して管理できます。[Key Vault 管理](https://msdn.microsoft.com/library/azure/mt620024.aspx) を参照してください。  
  
ブラウザーの信頼済みサイトにドメイン https://discovery.crmreplication.azure.net/ を追加し、このサイトでポップアップを有効にすることもお勧めします。  
  
## <a name="programming-for-the-data-export-service"></a>データ エクスポート サービスのためのプログラミング  
 データ エクスポート サービスは 2 つのグループに分けられる REST ベース API を公開します: Common Data Service の組織構造、関連付け、および接続情報を調べるための `Metadata` 操作のセット; そして各データ レプリケーションを構成および管理するための `Profiles` 操作のセット。  この API は、次の [Swagger](http://swagger.io/) URL で完全に定義および文書化されています。  
  
|Swagger エンドポイント|説明|  
|----------------------|-----------------|  
|[https://discovery.crmreplication.azure.net/swagger/docs/2016-01-01](https://discovery.crmreplication.azure.net/swagger/docs/2016-01-01)|開発者ツールとを動的プロセスで使用するためのデータ エクスポート サービス API の JSON の定義|  
|[https://discovery.crmreplication.azure.net/swagger/ui/index#](https://discovery.crmreplication.azure.net/swagger/ui/index)|開発者リファレンスのためのこの API のユーザー フレンドリ バージョン|  
  
<a name="bk_ApiQuickReference"></a>   
### <a name="api-quick-reference"></a>API クイック リファレンス  
 読者の便宜のために、これらのインターフェイスは、次の表でまとめられています。  
  
 **メタデータ操作** (`https://discovery.crmreplication.azure.net/crm/exporter/metadata/`)  
  
|リソース|メソッド|説明|  
|--------------|-------------|-----------------|  
|組織|[GET](https://discovery.crmreplication.azure.net/swagger/ui/index#/Metadata/Metadata_GetOrganizations)|現在のユーザーが所属するすべての組織の組織情報を取得|  
|検出|[GET](https://discovery.crmreplication.azure.net/swagger/ui/index#/Metadata/Metadata_GetOrgDetails)|指定された組織の組織情報を取得|  
|コネクタ|[GET](https://discovery.crmreplication.azure.net/swagger/ui/index#/Metadata/Metadata_GetConnectorDetails)|指定された組織のコネクタ情報の取得|  
|エンティティ|[GET](https://discovery.crmreplication.azure.net/swagger/ui/index#/Metadata/Metadata_GetEntities)|指定された組織のエクスポート可能なすべての共有エンティティの取得|  
|関連付け|[GET](https://discovery.crmreplication.azure.net/swagger/ui/index#/Metadata/Metadata_GetRelationships)|指定された組織のエクスポート可能なすべての関連付けの取得|  
|hasorgacceptedprivacyterms|[GET](https://discovery.crmreplication.azure.net/swagger/ui/index#/Metadata/Metadata_HasOrgAcceptedPrivacyTerms)|関連組織がプライバシー条件を受け入れたかどうかを確認|  
|acceptprivacyterms|[POST](https://discovery.crmreplication.azure.net/swagger/ui/index#/Metadata/Metadata_AcceptOrgPrivacyTerms)|データ アクセスのための指定された組織の受け入れ|  
  
 **プロファイリング操作** (`[Organization-URI]/crm/exporter/`)  
  
|リソース|メソッド|説明|  
|--------------|-------------|-----------------|  
|プロファイル|[GET](https://discovery.crmreplication.azure.net/swagger/ui/index#/Profiles/Profiles_GetProfilesByOrganizationId)、[POST](https://discovery.crmreplication.azure.net/swagger/ui/index#/Profiles/Profiles_CreateProfile)|指定された組織のすべてのプロファイルを取得し、新しいエクスポート プロファイルを作成|  
|プロファイル/{id}|[GET](https://discovery.crmreplication.azure.net/swagger/ui/index#/Profiles/Profiles_GetProfileById)、[PUT](https://discovery.crmreplication.azure.net/swagger/ui/index#/Profiles/Profiles_UpdateProfile)、[DELETE](https://discovery.crmreplication.azure.net/swagger/ui/index#/Profiles/Profiles_DeleteProfileById)|特定のプロファイルを取得、更新、または削除|  
|プロファイル/{id}/アクティブ化|[POST](https://discovery.crmreplication.azure.net/swagger/ui/index#/Profiles/Profiles_Activate)|関連したメタデータとデータの両方のレプリケーションを開始するプロファイルのアクティブ化|  
|プロファイル/{id}/activatemetadata|[POST](https://discovery.crmreplication.azure.net/swagger/ui/index#/Profiles/Profiles_ActivateMetadata)|メタデータ レプリケーションのみのプロファイルをアクティブ化|  
|プロファイル/{id}/activatedata|[POST](https://discovery.crmreplication.azure.net/swagger/ui/index#/Profiles/Profiles_ActivateData)|データ レプリケーションのみのプロファイルをアクティブ化|  
|プロファイル/{id}/非アクティブ化|[POST](https://discovery.crmreplication.azure.net/swagger/ui/index#/Profiles/Profiles_Deactivate)|プロファイルの非アクティブ化|  
|プロファイル/{id}/テスト|[GET](https://discovery.crmreplication.azure.net/swagger/ui/index#/Profiles/Profiles_GetTestResultById)|既存のプロファイル上でのテスト操作のを実行|  
|プロファイル/検証|[POST](https://discovery.crmreplication.azure.net/swagger/ui/index#/Profiles/Profiles_ValidateBeforeProfileCreation)|プロファイル説明を作成する前にテスト操作を実行|  
|プロファイル/{id}/失敗|[GET](https://discovery.crmreplication.azure.net/swagger/ui/index#/Profiles/Profiles_GetProfileFailuresInfoById)|特定のプロファイルの失敗の詳細情報を含む BLOB に接続文字列を取得|  
  
### <a name="gain-access"></a>アクセスの取得  
Common Data Service システム管理者のみがデータ エクスポート操作の実行を許可されているため、これらの API は Azure Active Directory ([AAD](https://azure.microsoft.com/en-us/services/active-directory/)) [セキュリティ トークン](https://azure.microsoft.com/en-us/documentation/articles/active-directory-token-and-claims/) を使用して呼出し元の承認を強制します。 次のコード スニペットは、管理者の名前とパスワードを使用して、Web アプリケーションのトークンを生成する方法を示しています。   サービスに適した値で、`AppId`、`crmAdminUser`、`crmAdminPassword` に置き換える必要があります。 このアプローチは、開発、およびテストに使用できます。しかし、より安全な手段、Azure Key Vault の使用などを運用のために使用します。  
  
```csharp  
  
//Reference Azure AD authentication Library (ADAL)    
using Microsoft.IdentityModel.Clients.ActiveDirectory;  
   . . .  
    string yourAppClientID = "[app-associated-GUID]";   //Your AAD-registered AppId   
    string crmAdminUser = "admin1@contoso.com";  //Your CRM administrator user name  
    string crmAdminPassword = "Admin1Password";  //Your CRM administrator password;   
    //For interactive applications, there are overloads of AcquireTokenAsync() which prompt for password.   
    var authParam = AuthenticationParameters.CreateFromResourceUrlAsync(new   
        Uri("https://discovery.crmreplication.azure.net/crm/exporter/aad/challenge")).Result;  
    AuthenticationContext authContext = new AuthenticationContext(authParam.Authority, false);  
    string token = authContext.AcquireTokenAsync(authParam.Resource, yourAppClientID,   
        new UserCredential(crmAdminUser, crmAdminPassword)).Result.AccessToken;  
  
```  
  
`AppId` を取得する方法については、[OAuth 2.0 と Azure Active Directory を使用して Web アプリケーションへのアクセスを承認](https://azure.microsoft.com/en-us/documentation/articles/active-directory-protocols-oauth-code/) を参照してください。 Azure ユーザー セキュリティの詳細については、[Azure AD の認証シナリオ](https://azure.microsoft.com/en-us/documentation/articles/active-directory-authentication-scenarios/) を参照してください。  
  
### <a name="error-handling-and-failure-processing"></a>エラー処理および失敗の処理  
 プロファイルが正しく構成されると、通常、同期プロセスの信頼性が高くなります。 ただし、レコードの同期に失敗すると、次のエラー処理が適用されます。  
  
1. 再試行間隔が構成された後、レコードを同期させる別の試みが実行されます。 これは構成された再試行の最大数まで繰り返されます。  
  
2. レコードは処理済みとしてマークされます。  
  
3. 対応するエラー レコード エントリはエラー ログに書き込まれます。  
  
4. 次のレコードが処理されます。  
  
レコードが処理済みとしてマークされるため、その値またはスキーマが変更されるまでレコードを同期する試みは実行されません。 (エンティティ インスタンスに戻して記述された同じ値は、修正済みともマークすることに注意してください。)  
  
エラー ログでのエントリは書き込み専用です。 同じレコードの同期中の将来の成功または失敗は、このレコードに対する過去のエントリの改ざんが影響するわけではありません。 たとえば、レコードが後の同期サイクル中に正常に同期された後であっても、エラー ログでの失敗エントリは残ります。  
  
> [!CAUTION]
>  このエラー処理ロジックは、このサービスの今後のリリースによって変更されることがあります。  
  
これらの失敗エントリは [特定のプロファイルの失敗の詳細情報を取得](https://discovery.crmreplication.azure.net/swagger/ui/index) 要求を介して取得することができます。 応答は、失敗情報を含む Azure BLOB に URI を返します。  各行には次のコンマ区切りフィールド (明確にするために追加された改行) があります。  
  
```  
  
Entity: <entity-name>,   
RecordId: <”N/A” | guid>,   
NotificationTime: <datetime>,   
ChangeType: <sync-type>,  
FailureReason: <description>  
  
```  
  
たとえば、次のようになります。  
  
```  
  
Entity: lead,   
RecordId: N/A, NotificationTime: , ChangeType: Trigger Initial Export, FailureReason: There is already an object named 'hatest201_lead' in the database.  
Entity: account, RecordId: b2a19cdd-88df-e311-b8e5-6c3be5a8b200, NotificationTime: 8/31/2016 6:50:38 PM, ChangeType: New, FailureReason: Invalid object name 'dbo.hatest201_account'.  
```  
  
### <a name="see-also"></a>関連項目  
 [Dynamics 365 でデータを管理する](/dynamics365/customer-engagement/developer/manage-data)   
 [データのインポート](import-data.md)
