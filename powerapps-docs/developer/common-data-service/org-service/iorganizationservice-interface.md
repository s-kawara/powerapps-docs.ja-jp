---
title: IOrganizationService インターフェイス (Common Data Service) | Microsoft Docs
description: Common Data Service を使ったデータ操作を実行するための、公開されている共通メソッドについて説明します。
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
# <a name="iorganizationservice-interface"></a>IOrganizationService インターフェイス

<xref:Microsoft.Xrm.Sdk.IOrganizationService> インターフェイスは、システム エンティティやユーザー定義エンティティと、組織のメタデータに対して、最も一般的な操作を実行する際に使用する一連のメソッドを提供します。

## <a name="client-applications"></a>クライアント アプリケーション

このインターフェイスは、クライアント アプリケーション作成時のコードで使用可能な幾つかのクラスに実装されています。

|クラス|説明|
|--|--|
|<xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceProxy>|これは WCF および SOAP エンドポイントで使用する元の下位クラスです |
|<xref:Microsoft.Xrm.Sdk.WebServiceClient.OrganizationWebProxyClient>|この下位クラスは SOAP エンドポイントの OAuth 認証を有効にするために作成されました|
|<xref:Microsoft.Xrm.Tooling.Connector.CrmServiceClient>|.NET クライアント アプリケーションを作成するときには、このクラスを使用する必要があります。 |

> [!NOTE]
> 下位レベルの <xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceProxy> または <xref:Microsoft.Xrm.Sdk.WebServiceClient.OrganizationWebProxyClient> クラスを使用している古いコードまたはサンプルを検索することができますが、新しい .NET クライアント アプリケーションのために <xref:Microsoft.Xrm.Tooling.Connector.CrmServiceClient> を使用することをお勧めします

## <a name="plug-ins"></a>プラグイン

プラグインを記述する場合は、<xref:Microsoft.Xrm.Sdk.IOrganizationServiceFactory>.<xref:Microsoft.Xrm.Sdk.IOrganizationServiceFactory.CreateOrganizationService(System.Nullable{System.Guid})> から返されたオブジェクトもあります <xref:Microsoft.Xrm.Sdk.IOrganizationService> インターフェイスは上述のクラスの幾つかの型では実装されない予定です。

## <a name="iorganizationservice-methods"></a>IOrganizationService メソッド

<xref:Microsoft.Xrm.Sdk.IOrganizationService> インターフェイスが実装された各クラスには、追加プロパティおよびメソッドが含まれますが、<xref:Microsoft.Xrm.Sdk.IOrganizationService> インターフェイスにあるのは 8 つのメソッドだけです。


|方法  |説明  |
|---------|---------|
|<xref:Microsoft.Xrm.Sdk.IOrganizationService.Associate*>|エンティティの関連付けを使用して 2 つのエンティティをリンクさせる|
|<xref:Microsoft.Xrm.Sdk.IOrganizationService.Create*>|エンティティ レコードを作成します。|
|<xref:Microsoft.Xrm.Sdk.IOrganizationService.Delete*>|エンティティ レコードの削除|
|<xref:Microsoft.Xrm.Sdk.IOrganizationService.Disassociate*>|エンティティの関連付けを使用して 2 つのエンティティ間のリンクを削除する|
|<xref:Microsoft.Xrm.Sdk.IOrganizationService.Execute*>|<xref:Microsoft.Xrm.Sdk.OrganizationRequest> のインスタンス、もしくはそこからの派生クラスを渡すことで、Message として定義する操作を呼び出します。|
|<xref:Microsoft.Xrm.Sdk.IOrganizationService.Retrieve*>|エンティティ レコードのインスタンスを取得します。|
|<xref:Microsoft.Xrm.Sdk.IOrganizationService.RetrieveMultiple*>|クエリ内の条件に一致するエンティティ レコードのコレクションを取得します。|
|<xref:Microsoft.Xrm.Sdk.IOrganizationService.Update*>|エンティティ レコードに対する属性値を変更します。|

> [!NOTE]
> 組織サービスは `Execute` メソッドのみを公開しています。 <xref:Microsoft.Xrm.Sdk.IOrganizationService> インターフェイスのその他のメソッドは、`Execute` メソッドのラッパーにすぎません。 これらのその他のメソッドが作業に便利なように、用意されています。 `Execute` メソッドのみを使用して全ての操作を実行できます。 詳細: [メッセージを組織サービスと共に使用する](use-messages.md)

## <a name="see-also"></a>関連項目

[メッセージを組織サービスと共に使用する](use-messages.md)<br />
[クライアント アプリケーションの作成](create-client-app.md)<br />
[プラグインを記述する](../write-plug-in.md)<br />
[組織サービスを使用したエンティティ操作](entity-operations.md)