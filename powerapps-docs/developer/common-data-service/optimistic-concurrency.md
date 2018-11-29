---
title: オプティミスティック同時実行 (アプリ用 Common Data Service) | Microsoft Docs
description: オプティミスティック同時実行では、ユーザーのアプリケーションがエンティティ レコードを取得した時点からそのレコードの更新または削除を試みるときまでに、サーバー上でそのレコードに変更があったかどうかをアプリケーションで検出する機能が提供されます。
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
# <a name="optimistic-concurrency"></a>オプティミスティック同時実行

PowerApps のようなマルチスレッド、マルチユーザー システムでは、操作とデータの変更がよく並行して実行されます。 同じデータの部分に対して 2 つ以上の更新または削除の操作が同時に行われると、問題が発生します。 この状態は、データの損失を引き起こす可能性があります。 オプティミスティック同時実行機能では、ユーザーのアプリケーションがエンティティ レコードを取得した時点からそのレコードの更新または削除を試みるときまでに、サーバー上でそのレコードに変更があったかどうかをアプリケーションで検出するできます。  
  
 オプティミスティック同時実行は、オフライン同期とすべてのユーザー定義エンティティが有効なすべての標準エンティティでサポートされています。 ードを使用してエンティティのメタデータを取得することによって、または[メタデータ ブラウザー](browse-your-metadata.md)を使用してメタデータを表示することによってエンティティがオプティミスティック同時実行をサポートするかどうかを決定し、属性 **IsOptimisticConcurrencyEnabled** が  `true` に設定されているかを確認できます。 ユーザー定義エンティティでは、このプロパティは `true` に既定で設定されます。  
  
<a name="bkmk_enable"></a>   
## <a name="enable-optimistic-concurrency"></a>オプティミスティック同時実行を有効化  
 要求の <xref:Microsoft.Xrm.Sdk.Messages.UpdateRequest.ConcurrencyBehavior> プロパティを <xref:Microsoft.Xrm.Sdk.ConcurrencyBehavior.IfRowVersionMatches> に設定して  <xref:Microsoft.Xrm.Sdk.Messages.UpdateRequest> を実行するとき、オプティミスティック同時実行の確認動作を有効にできます。 同様に、<xref:Microsoft.Xrm.Sdk.Messages.DeleteRequest> に対して、<xref:Microsoft.Xrm.Sdk.Messages.DeleteRequest.ConcurrencyBehavior> プロパティを設定します。  
  
 組織サービス コンテキストを使用してデータに変更を加える場合、<xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext> オブジェクトに対して <xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext.ConcurrencyBehavior> を設定します。 この値は、<xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext.SaveChanges> が呼び出されたときに、**OrganizationServiceContext** によって使用されるすべての **UpdateRequest** および **DeleteRequest** メッセージに渡されます。  
  
 オプティミスティック同時実行の動作は、SDK 呼び出しによってのみ設定できます。 現在、Web アプリケーションのフォームでは、OC の動作に対して何も設定されていません。  
  
## <a name="apply-optimistic-concurrency-using-web-api"></a>Web API を使用してのオプティミスティック同時実行の適用

Web API を使用したオプティミスティック同時実行の適用の詳細については、「[オプティミスティック同時実行の適用](webapi/perform-conditional-operations-using-web-api.md##apply-optimistic-concurrency)」を参照してください。


## <a name="apply-optimistic-concurrency-using-organization-service"></a>組織サービスを使用してのオプティミスティック同時実行の適用

組織サービスを使用したオプティミスティック同時実行の適用の詳細については、「[オプティミスティック同時実行の動作](org-service/entity-operations-update-delete.md##optimistic-concurrency-behavior)」を参照してください。
  
<a name="bkmk_handle"></a>   
## <a name="handle-exceptions"></a>例外処理  
 オプティミスティック同時実行を使用するときに Web サービス呼び出しから [FaultException](https://msdn.microsoft.com/library/ms576199\(v=vs.110\).aspx)\<<xref:Microsoft.Xrm.Sdk.OrganizationServiceFault>> で返すことができるいくつかのエラー状態があります。  
  
- **ConcurrencyVersionMismatch** (code=-2147088254)  
  
     行バージョンが提供されて、**IfVersionMatches** 動作が指示されているとき、既存のレコードのバージョンが要求で提供された行バージョンと一致しない場合、フォールトが返されます。  
  
- **ConcurrencyVersionNotProvided** (code= -2147088253)  
  
     **IfVersionMatches** 動作が指示されていて、行バージョンの値が提供されていないとき、フォールトが返されます。  
  
- **OptimisticConcurrencyNotEnabled** (code=-2147088243)  
  
     **IfVersionMatches** 動作がエンティティの更新時に指示されていて、オプティミスティック同時実行が有効になっていない場合、フォールトが返されます。  
  
  返されたフォルトの [コード](https://msdn.microsoft.com/library/system.servicemodel.faultexception.code\(v=vs.110\).aspx) プロパティをチェックして、フォルトがオプティミスティック同時実行に関連しているかどうか確認できます。 先に表示されたエラー状態を示すコードが、ErrorCodes.cs ヘルパー コードから取得されました。  
  
