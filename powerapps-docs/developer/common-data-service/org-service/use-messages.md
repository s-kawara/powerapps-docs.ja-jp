---
title: 組織サービスと共にメッセージを使用する (アプリ用 Common Data Service) | Microsoft Docs
description: 組織サービスを使って操作を呼び出すためにメッセージを使用する方法を理解します。
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
# <a name="use-messages-with-the-organization-service"></a>メッセージを組織サービスと共に使用する

組織サービスのすべてのデータ操作はメッセージとして定義されます。 <xref:Microsoft.Xrm.Sdk.IOrganizationService> はデータ操作を行う次の 7 つのメソッドを提供する。 (<xref:Microsoft.Xrm.Sdk.IOrganizationService.Create*>、 <xref:Microsoft.Xrm.Sdk.IOrganizationService.Retrieve*>、 <xref:Microsoft.Xrm.Sdk.IOrganizationService.RetrieveMultiple*>、 <xref:Microsoft.Xrm.Sdk.IOrganizationService.Update*>、 <xref:Microsoft.Xrm.Sdk.IOrganizationService.Delete*>、 <xref:Microsoft.Xrm.Sdk.IOrganizationService.Associate*> および <xref:Microsoft.Xrm.Sdk.IOrganizationService.Disassociate*> ) これらのメソッドはそれぞれ基になるメッセージまわりの便利なサッパーで、最終的に <xref:Microsoft.Xrm.Sdk.IOrganizationService.Execute*> メソッドを使用して呼び出されます。 基礎となる組織サービスのみが <xref:Microsoft.Xrm.Sdk.IOrganizationService.Execute*> メソッドを 1 つのパラメーターとしてを持ち、それは <xref:Microsoft.Xrm.Sdk.OrganizationRequest> クラスのインスタンスです。 `Execute` メソッドによって返される値は <xref:Microsoft.Xrm.Sdk.OrganizationResponse> クラスのインスタンスです。

コードを記述する際のエクスペリエンス向上のため、すべての標準システム データ操作には SDK アセンブリで定義されている `*Request` および `*Response` クラスのペアがあります。 これらのクラスはそれぞれが <xref:Microsoft.Xrm.Sdk.OrganizationRequest> および <xref:Microsoft.Xrm.Sdk.OrganizationResponse> の各クラスを継承しており、コーディングの際に生産性のより高いエクスペリエンスを提供します。

次の例は取引先企業のエンティティ レコードを作成するための 3 つの異なる方法を示します:

```csharp
var account = new Account();
account.Name = "Test account";
```

<xref:Microsoft.Xrm.Sdk.IOrganizationService>、<xref:Microsoft.Xrm.Sdk.IOrganizationService.Create*>の使用

```csharp
var id = svc.Create(account);
```

<xref:Microsoft.Xrm.Sdk.IOrganizationService>および<xref:Microsoft.Xrm.Sdk.IOrganizationService.Execute*>と共に <xref:Microsoft.Xrm.Sdk.Messages.CreateRequest> を使用する

```csharp
CreateRequest request = new CreateRequest()
{ Target = account };
var id = ((CreateResponse)svc.Execute(request)).id;
```

<xref:Microsoft.Xrm.Sdk.IOrganizationService>および<xref:Microsoft.Xrm.Sdk.IOrganizationService.Execute*>と共に <xref:Microsoft.Xrm.Sdk.OrganizationRequest> を使用する

```csharp
ParameterCollection parameters = new ParameterCollection();
parameters.Add("Target", account);

OrganizationRequest request = new OrganizationRequest() {
RequestName = "Create",
Parameters = parameters
};

OrganizationResponse response = svc.Execute(request);

var id = (Guid)response.Results["id"];
```

このように一般的なデータ操作は <xref:Microsoft.Xrm.Sdk.IOrganizationService> メソッドを使用して効率化され、システム メッセージは SDK アセンブリの `*Request` および `*Response` クラスで簡素化されています。 下記のケースを除くほとんどの場合、基になる <xref:Microsoft.Xrm.Sdk.OrganizationRequest> および <xref:Microsoft.Xrm.Sdk.OrganizationResponse> クラスを使用する必要はありません。

## <a name="working-with-messages-in-plug-ins"></a>プラグインのメッセージの操作

プラグインでの操作を示すデータは次の形式をとります <xref:Microsoft.Xrm.Sdk.IExecutionContext>、<xref:Microsoft.Xrm.Sdk.IExecutionContext.InputParameters> および <xref:Microsoft.Xrm.Sdk.IExecutionContext>、<xref:Microsoft.Xrm.Sdk.IExecutionContext.OutputParameters>。 これら <xref:Microsoft.Xrm.Sdk.ParameterCollection> のプロパティは、イベント実行パイプラインの最初 2 つのステージにおいては <xref:Microsoft.Xrm.Sdk.OrganizationRequest> 、メイン操作の後のステージでは <xref:Microsoft.Xrm.Sdk.OrganizationResponse> クラスで使用される値を格納します。

メッセージの構造を知ることはプラグイン内で確認や変更が必要なデータがどこにあるか理解するのに役立ちます。

詳細: 

- [ビジネス プロセスを拡張するためのプラグインを記述する](../plug-ins.md)
- [イベント フレームワーク](../event-framework.md)

## <a name="using-custom-actions"></a>ユーザー定義アクションを使用する

ユーザー定義のアクションを使用すると SDK アセンブリにこれらの操作に対するクラスはありません。 コード生成ツール `CrmSvcUtil.exe` でパラメータ `generateActions` を使用するとこれらのクラスを生成することがでできます。またはクラスを生成せずに使うには <xref:Microsoft.Xrm.Sdk.OrganizationRequest> をインスタンス化して <xref:Microsoft.Xrm.Sdk.OrganizationRequest.RequestName> および <xref:Microsoft.Xrm.Sdk.OrganizationRequest.Parameters> をセットします。 その結果を使用するには <xref:Microsoft.Xrm.Sdk.OrganizationResponse>、<xref:Microsoft.Xrm.Sdk.OrganizationResponse.Results>から返される値を解析する必要があります。 プロパティに設定します。

詳細: 

- [組織サービスを使用して事前バインド プログラミングのクラスを生成する](generate-early-bound-classes.md)
- [ユーザー定義アクション](../custom-actions.md)

## <a name="passing-optional-parameters-with-a-request"></a>要求のオプション パラメーターを渡す

SDK アセンブリのすべての *Request メッセージ クラスに対して公開されているプロパティ <xref:Microsoft.Xrm.Sdk.OrganizationRequest.Parameters> を使用して、メッセージのオプション パラメーターを渡すことができます。 メッセージで渡す事ができるオプション パラメータは 2 つあります

|`Parameter`|説明|[メッセージ]|  
|-----------------|-----------------|--------------|  
|`SolutionUniqueName`|操作が適用されるソリューションの一意の名前を指定する `String` です。 詳細: [ソリューション コンポーネントの依存関係の追跡](../dependency-tracking-solution-components.md)。|<xref:Microsoft.Crm.Sdk.Messages.AddPrivilegesRoleRequest> <br /> <xref:Microsoft.Xrm.Sdk.Messages.CreateRequest> <br /> <xref:Microsoft.Xrm.Sdk.Messages.DeleteRequest> <br /> <xref:Microsoft.Crm.Sdk.Messages.MakeAvailableToOrganizationTemplateRequest> <br /> <xref:Microsoft.Xrm.Sdk.Messages.UpdateRequest>|  
|`SuppressDuplicateDetection`|作成操作または更新操作で、重複データの検出を無効にするために使用する `Boolean` です。 詳細: [レコードを作成または更新するときにエラーをスローする SuppressDuplicateDetection パラメータを使用する](detect-duplicate-data.md#use-suppressduplicatedetection-parameter-to-throw-errors-when-you-create-or-update-record) 。|<xref:Microsoft.Xrm.Sdk.Messages.CreateRequest> <br /> <xref:Microsoft.Xrm.Sdk.Messages.UpdateRequest>|  
  
 次のサンプルは、オプション パラメーターを渡す方法を示しています。  
  
```csharp  
Account account = new Account();  
account.Name = "Fabrikam";  
CreateRequest req = new CreateRequest();  
req.Target = account;  
req["SuppressDuplicateDetection"] = true;  
CreateResponse response = (CreateResponse)svc.Execute(req);  
```  

### <a name="see-also"></a>関連項目

[組織サービスを使用したエンティティ操作](entity-operations.md)<br />
[ExecuteAsync を使用する](use-executeAsync.md)<br />
[ExecuteTransaction を使用する](use-executetransaction.md)<br />
[組織サービスを使用して複数の要求を実行する](execute-multiple-requests.md)



