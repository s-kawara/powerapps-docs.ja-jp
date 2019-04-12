---
title: OrganizationServiceContext の使用 (Common Data Service) | Microsoft Docs
description: OrganizationServiceContext クラスにより、変更を追跡し、ID およびリレーションシップを管理し、 LINQ プロバイダーにアクセスすることができます。
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: brandonsimons
ms.author: jdaly
manager: ryjones
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="use-organizationservicecontext"></a>OrganizationServiceContext の使用

Common Data Service では <xref:Microsoft.Xrm.Sdk.IOrganizationService> インターフェイスを実装する数個のクラスを使用して、Web サービスにアクセスできます。 または、コード生成ツールで生成された <xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext> を使用して、追加機能にアクセスできます。 `OrganizationServiceContext` クラスにより、変更を追跡し、ID およびリレーションシップを管理し、 LINQ プロバイダーにアクセスすることができます。 また、このクラスにはコンテキストが追跡するデータに対する変更の送信に使用する、<xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext><xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext.SaveChanges> メソッドも含まれています。 このクラスは、 Windows Communication Foundation (WCF) データ サービスの [DataServiceContext](/dotnet/api/system.data.services.client.dataservicecontext) クラスと同じ概念に基づいています。  
  
このクラスを生成するには、事前バインドの型を生成するときに `/serviceContextName` パラメーターの値を指定します。 コード生成ツールでは、この名前が生成したクラスの名前として使用されます。 コード生成ツールの使用方法に関する詳細については、「[組織サービスを使用して事前バインド プログラミングのクラスを生成す](generate-early-bound-classes.md)」を参照してください。 アプリケーション、プラグイン、およびワークフロー活動を開発する際に、組織サービス コンテキストを使用できます。  
  
<a name="how_to_use"></a>

## <a name="how-to-use-the-organizationservicecontext-class"></a>OrganizationServiceContext クラスの使用方法  

コンテキスト クラスのインスタンスを作成するには、クラス コンストラクターに <xref:Microsoft.Xrm.Sdk.IOrganizationService> インターフェイスを実装するオブジェクトを渡す必要があります。 1 つの方法として、<xref:Microsoft.Xrm.Tooling.Connector.CrmServiceClient> クラスのインスタンスを渡すことができます。 <xref:Microsoft.Xrm.Sdk.IOrganizationService> インターフェイスの詳細については、「[組織で IOrganizationService インターフェイスを使用する](iorganizationservice-interface.md)」を参照してください。
  
次のコード例は、コンテキスト クラスの新しいインスタンスを作成する方法を示しています。 この例では、コード生成ツールで `/serviceContextName` パラメーターを使用して名前を指定することによって、コンテキスト クラスに `AdventureWorksCycleServiceContext` という名前が付けられています。  
  
```csharp  
//For early bound types to work correctly, they have to be enabled on the proxy.  
_serviceProxy.EnableProxyTypes();  
AdventureWorksCycleServiceContext context = new AdventureWorksCycleServiceContext(svc);  
```  
  
組織サービス コンテキスト オブジェクトを作成すれば、エンティティの作成、変更、または削除の追跡を開始できます。 
  
組織サービス コンテキストは Common Data Service への送信対象となるあらゆるエンティティまたは関連付けを追跡する必要があります。 たとえば、LINQ クエリでレコードを取得してコンテキストでエンティティが追跡されるようにするか、<xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext>.<xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext.Attach(Microsoft.Xrm.Sdk.Entity)>  メソッドを使用してコンテキストによるエンティティの追跡を開始することができます。 クライアント アプリケーションのデータを使用し、新しいエンティティの作成、関連エンティティの作成、既存のエンティティの変更を行うことができますが、変更を Common Data Service にコミットするには追跡対象のエンティティで `SaveChanges` メソッドを呼び出す必要があります。  
  
<a name="track_changes"></a>

## <a name="track-changes"></a>変更の追跡
 
コンテキストによるエンティティの追跡方法を調べるには、エンティティ インスタンスの <xref:Microsoft.Xrm.Sdk.Entity.EntityState> プロパティを確認します。 さまざまなメソッドを呼び出すか、LINQ クエリを使用して、Common Data Service のエンティティを追跡するように組織サービス コンテキストに通知する必要があります。 LINQ クエリから返されるすべてのエンティティはサービス コンテキストによって追跡されます。  
  
サービス コンテキストにオブジェクトを追加するには、<xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext> で次のいずれかのメソッドを呼び出します。  
  
|方法|用途|  
|------------|---------|  
|<xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext.AddObject(Microsoft.Xrm.Sdk.Entity)>|組織サービス コンテキストが追跡するエンティティ セットにエンティティを追加します。 コンテキスト内のエンティティの状態は `Created` に設定されます。 <xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext.SaveChanges> メソッドを呼び出すと、このレコードが作成されるか、またはサーバーに追加されます。|  
|<xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext.Attach(Microsoft.Xrm.Sdk.Entity)>|組織サービス コンテキストが追跡するエンティティ セットにエンティティを追加します。 コンテキスト内のエンティティの状態は `Unchanged` に設定されます。 <xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext.SaveChanges> メソッドを呼び出しても、このエンティティは状態が変更されるまでサーバーに送信されません。|  
|<xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext.CreateQuery(System.String)>|組織サービス コンテキストが追跡するエンティティ セットにクエリの結果を追加します。|  
  
<a name="track_related"></a>

## <a name="track-related-objects"></a>関連オブジェクトの追跡

Common Data Service では、組織サービス コンテキストでエンティティ間の関連付けを作成および更新できます。 CrmSvcUtil.exe ツールで生成され、事前バインド クラスに配置されるナビゲーション プロパティで、関連エンティティのプロパティや関連付けへのアクセスや変更を行うことができます。 関連エンティティをサーバーで更新できるようにするには、組織サービス コンテキストで関連エンティティを追跡する必要があります。  
  
関連エンティティを操作する場合、およびサービス コンテキストにエンティティを追加する場合は、<xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext> で次のメソッドを使用します。  
  
|方法|用途|  
|------------|---------|  
|<xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext.AddRelatedObject(Microsoft.Xrm.Sdk.Entity,Microsoft.Xrm.Sdk.Relationship,Microsoft.Xrm.Sdk.Entity)>|コンテキストにターゲットを追加します。 ターゲット エンティティに対して <xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext.Attach(Microsoft.Xrm.Sdk.Entity)> メソッドを呼び出し、ソース エンティティとターゲット (関連) エンティティ間の <xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext.AddLink(Microsoft.Xrm.Sdk.Entity,Microsoft.Xrm.Sdk.Relationship,Microsoft.Xrm.Sdk.Entity)> メソッドを呼び出します。|  
|<xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext.AttachLink(Microsoft.Xrm.Sdk.Entity,Microsoft.Xrm.Sdk.Relationship,Microsoft.Xrm.Sdk.Entity)>|追跡を行うコンテキストに関連エンティティを追加します。 コンテキスト内のエンティティの状態は `Unchanged` に設定されます。|  
|<xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext.AddLink(Microsoft.Xrm.Sdk.Entity,Microsoft.Xrm.Sdk.Relationship,Microsoft.Xrm.Sdk.Entity)>|ソース エンティティとターゲット エンティティ間の関連付けを作成します。 コンテキストにターゲットを追加します。 コンテキスト内のターゲット エンティティの状態は `Created` に設定されます。|  
|<xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext.LoadProperty(Microsoft.Xrm.Sdk.Entity,System.String)>|指定した関連付けの関連エンティティ セットを読み込みます。 ナビゲーション プロパティを使用して関連エンティティにアクセスできるようになります。 親エンティティでナビゲーション プロパティを使用してエンティティにアクセスした後、関連エンティティで <xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext.AddObject(Microsoft.Xrm.Sdk.Entity)> メソッドを呼び出します。|  
|<xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext.UpdateObject(Microsoft.Xrm.Sdk.Entity)>|`OrganizationServiceContext` 内の指定したエンティティの状態が Modified に変更されます。|  
|<xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext.DeleteObject(Microsoft.Xrm.Sdk.Entity)>|`OrganizationServiceContext` 内の指定したエンティティの状態が Deleted に変更されます。|  
  
<a name="BKMK_LoadRelatedEntities"></a>

### <a name="load-related-entities-using-navigation-properties"></a>ナビゲーション プロパティを使用して関連エンティティの読み込み

LINQ を使用して取得したエンティティの関連エンティティは、<xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext.LoadProperty(Microsoft.Xrm.Sdk.Entity,Microsoft.Xrm.Sdk.Relationship)> を使用してそれらを取得するまでは null です。 次のサンプル コードは、特定の取引先担当者レコードに関連付けられているタスク レコードにアクセスする方法を示しています。  
  
```csharp  
Contact pam = context.ContactSet.Where(c => c.FirstName == "Pamela").FirstOrDefault();  
if (pam != null)  
{  
// pam.Contact_Tasks is null until you use LoadProperty  
    context.LoadProperty(pam, "Contact_Tasks");  
    Task firstTask = pam.Contact_Tasks.FirstOrDefault();  
}  
```  
  
<a name="save_changes"></a>

## <a name="save-changes"></a>変更の保存

組織サービス コンテキストは追跡中のエンティティのグラフを保持します。 組織サービス コンテキストがエンティティの変更を処理し、サーバーに送信する順序が重要です。 主エンティティの更新が処理された後に関連エンティティが処理されます。 関連エンティティによって主エンティティに値が設定されると、その値がサーバーでのデータの更新時に使用されます。  
  
エンティティ情報が保存されるときにエラーが発生する場合、<xref:Microsoft.Xrm.Sdk.SaveChangesResult> を含む新しい例外タイプが <xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext>.<xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext.SaveChanges> メソッドによりスローされます (メソッドに渡される <xref:Microsoft.Xrm.Sdk.Client.SaveChangesOptions> パラメーターの値にかかわらず)。  
  
<a name="virtual"></a>

## <a name="use-virtual-methods-when-the-context-is-changed"></a>コンテキストが変更された場合の仮想メソッドの使用

場合によっては、<xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext> の変更に基づいて操作を実行する必要があります。 この処理を簡素化するために、操作をインターセプトしたり、操作の通知を受けることができる仮想メソッドが用意されています。 仮想メソッドを利用するには、<xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext> を継承するか、生成された組織サービス コンテキストを変更する必要があります。仮想メソッドの一覧を次の表に示します。  
  
|方法|説明|  
|------------|-----------------|  
|<xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext.OnBeginEntityTracking(Microsoft.Xrm.Sdk.Entity)>|エンティティを `OrganizationServiceContext` にアタッチした後に呼び出します。|  
|<xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext.OnBeginLinkTracking(Microsoft.Xrm.Sdk.Entity,Microsoft.Xrm.Sdk.Relationship,Microsoft.Xrm.Sdk.Entity)>|リンクを `OrganizationServiceContext` にアタッチした後に呼び出します。|  
|<xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext.OnEndEntityTracking(Microsoft.Xrm.Sdk.Entity)>|エンティティを `OrganizationServiceContext` からデタッチした後に呼び出します。|  
|<xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext.OnEndEntityTracking(Microsoft.Xrm.Sdk.Entity)>|リンクを `OrganizationServiceContext` からデタッチした後に呼び出します。|  
|<xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext.OnExecuting(Microsoft.Xrm.Sdk.OrganizationRequest)>|要求を Common Data Service に送信する直前に呼び出します。|  
|<xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext.OnExecute(Microsoft.Xrm.Sdk.OrganizationRequest,Microsoft.Xrm.Sdk.OrganizationResponse)>|例外が発生したかどうかに関係なく、要求を Common Data Service に送信した直後に呼び出します。|  
|<xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext.OnSavingChanges(Microsoft.Xrm.Sdk.Client.SaveChangesOptions)>|`SaveChanges` を呼び出した後の操作の前に呼び出します。|  
|<xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext.OnSaveChanges(Microsoft.Xrm.Sdk.SaveChangesResultCollection)>|`SaveChanges` の呼び出しに関するすべての操作が完了したとき、またはエラーが発生したときに呼び出します。|  


<a name="use_context"></a>   

## <a name="data-operations"></a>データ操作

組織サービス コンテキストのオブジェクトを変更、作成、および削除でき、これらのオブジェクトに対して行った変更は Common Data Service によって追跡されます。 <xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext>.<xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext.SaveChanges> メソッドが呼び出されると、Common Data Service は、Common Data Service 内のデータに対して同等の挿入、更新、または削除ステートメント実行するコマンドを生成して実行します。  
  
事前バインド エンティティ クラスを操作する場合は、エンティティ名と属性スキーマ名を使用して、操作するエンティティまたは属性を指定します。 属性スキーマ名は、<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata>.<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata.SchemaName> および <xref:Microsoft.Xrm.Sdk.Metadata.AttributeMetadata>.<xref:Microsoft.Xrm.Sdk.Metadata.AttributeMetadata.SchemaName> で定義されるか、ユーザーがコード生成ファイルに示されるクラス名およびプロパティ名を使用することができます。次のサンプルでは、新しい連絡先インスタンスの電子メール属性に値を割り当てる方法を示します。  
  
```csharp  
Contact contact = new Contact();
contact.EMailAddress1 = “sonny@contoso.com”;  
```  
 
  
<a name="create_new"></a>   

## <a name="create-a-new-entity-record"></a>エンティティ レコードの新規作成

 エンティティ データ モデルを使用して Common Data Service にデータを挿入する場合は、エンティティの種類のインスタンスを作成し、組織サービス コンテキストにオブジェクトを追加する必要があります。 組織サービス コンテキストは、オブジェクトを Common Data Service に保存する前にオブジェクトを追跡する必要があります。  
  
 新規エンティティ レコードを作成する場合は、<xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext.AddObject(Microsoft.Xrm.Sdk.Entity)> を使用して、組織サービス コンテキストにオブジェクトを追加します。  メソッド。  
  
 次のサンプルでは、エンティティ データ モデルを使用して新しい連絡先レコードをインスタンス化および保存する方法を示します。 カスタム属性にアクセスする方法も示します。  
  
```csharp  
OrganizationServiceContext orgContext =new OrganizationServiceContext(svc);  
Contact contact = new Contact()     
 {  
   FirstName = "Charles",  
   LastName = "Brown",  
   Address1_Line1 = "123 Main St.",  
   Address1_City = "Des Moines",  
   Address1_StateOrProvince = "IA",  
   Address1_PostalCode = "21254",  
   new_twittername = "Chuck",  
   Telephone1 = "123-234-5678"  
 };   
orgContext.AddObject(contact);
orgContext.SaveChanges();  
```  

前述のコード例にはいくつかの注意点があります。 最初に新しい取引先担当者のインスタンスを作成した後、取引先担当者オブジェクトを <xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext>.<xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext.AddObject(Microsoft.Xrm.Sdk.Entity)> メソッドに渡し、コンテキストがオブジェクトの追跡を開始することができるようにします。 もう一つの注意点は、新しいオブジェクトをサーバーに保存するために <xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext>.<xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext.SaveChanges>   メソッド。  
  
オブジェクトをコンテキストに追加後、<xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext>.<xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext.SaveChanges> メソッドが呼び出される前に、コンテキストは新しいオブジェクトの ID を生成します。 Common Data Service データに対する更新が失敗した場合は、`SaveChangesResults` を含む例外が <xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext.SaveChanges> メソッドからスローされます。  
  
<a name="update"></a>   

## <a name="update-an-entity-record"></a>エンティティ レコードの更新  

Common Data Service は、組織サービス コンテキストに添付されているオブジェクトに対する変更を追跡します。 既存のエンティティ レコードを変更するには、最初にオブジェクトをコンテキストに追加する必要があります。 オブジェクトをコンテキストに追加するには、Common Data Service からエンティティ レコードを取得してから、<xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext.Attach(Microsoft.Xrm.Sdk.Entity)> メソッドを使用してオブジェクトをコンテキストに追加する必要があります。 オブジェクトがコンテキストによって追跡された後、エンティティの属性を設定することでレコードを更新できます。  
  
次のサンプルでは、事前バインド クラスを使用して取引先企業属性を更新する方法を示します。  
  
```csharp  
Account.EMailAddress1 = “Contoso-WebMaster@contoso.com”;  
```  
  
 次のサンプルでは、属性値を削除する方法を示します。  
  
```csharp  
Account.EMailAddress1 = null;  
```  
  
 各エンティティには、`OnPropertyChanging`および `OnPropertyChanged` という名前の 2 つの部分メソッドがあります。 これらのメソッドは、プロパティ セッターで呼び出されます。 これらのメソッドは、部分クラスを使用してカスタム ビジネス ロジックを挿入することで拡張できます。  
  
<a name="delete"></a>   

## <a name="delete-an-entity-record"></a>エンティティ レコードの削除   

エンティティ レコードを削除するには、組織サービス コンテキストでオブジェクトを追跡する必要があります。 オブジェクトがコンテキストに配置された後、<xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext.DeleteObject(Microsoft.Xrm.Sdk.Entity)> メソッドを使用して、コンテキスト上の削除するオブジェクトをマークできます。 Common Data Service のエンティティ レコードは、<xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext>.<xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext.SaveChanges> メソッドが呼び出されるまで削除されないことに注意してください。  
  
### <a name="see-also"></a>関連項目

[Common Data Service で OrganizationServiceContext を使用した LINQ クエリの例](linq-query-examples.md)<br />
[組織サービスを使用して事前バインド プログラミングのクラスを生成する](generate-early-bound-classes.md)<br />
<xref:Microsoft.Xrm.Sdk.IOrganizationService><br />
<xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext>