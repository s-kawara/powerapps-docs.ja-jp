---
title: 別のユーザーを偽装する (Common Data Service) | Microsoft Docs
description: 偽装を使用して、別の Common Data Service ユーザーに代わってビジネス ロジックを実行し、偽装されるユーザーの適切なロール ベースとオブジェクトベースのセキュリティを使用して任意の機能やサービスを提供します。
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: JimDaly
ms.author: jdaly
manager: ryjones
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="impersonate-another-user"></a>もう一方のユーザーの偽装

偽装を使用して、別の Common Data Service ユーザーに代わってビジネス ロジックを実行し、偽装されるユーザーの適切なロール ベースとオブジェクトベースのセキュリティを使用して任意の機能やサービスを提供します。 

偽装が必要なのは、Common Data Service ユーザーに代わってさまざまなクライアントやサービスによって Common Data Service Web サービスを呼び出すことができるためです。

偽装には、2 つの異なるユーザー アカウントが関与します。 

|偽装者|偽装ユーザー|
|--|--|
|コードを実行する時に使用されるユーザー アカウント|実行されているタスクが代理をしているユーザー アカウント。|

## <a name="required-privileges"></a>必要な特権

*偽装者*は、**代理人**セキュリティ ロールに含まれているか、またはすべてのセキュリティ ロールに有効化される、**別のユーザーの代わりに操作します** (`prvActOnBehalfOfAnotherUser`) の権限を必要とします。

> [!NOTE]
> ユーザーが 1 つ以上のセキュリティ ロールに関連付けられていることが必要です。 ユーザーに**代理人**セキュリティ ロールを割り当てることにより、ユーザー アカウントに関連付けられている他のすべてのセキュリティ ロールによって提供される権限と同様に、`prvActOnBehalfOfAnotherUser` 権限が付与されます。

データ変更に使用される実際の特権のセットは、*偽装者*の役割のユーザーが所有する特権と、*偽装ユーザー*が所有する特権との共通部分です。 

つまり、*偽装者*と*偽装されたユーザー*が操作に必要な特権を持つ*場合にのみ*、*偽装者*は何かを実行できます。

## <a name="impersonation-with-server-to-server-authentication"></a>サーバー間認証を使用した偽装

登録ユーザーの代理ができるユーザー アカウントを必要とする Web クライアント アプリケーションを作成している場合、特別な*アプリケーション ユーザー*を使用することにより、Common Data Service の有料ユーザー ライセンスを使用する必要がなくなります。

詳細情報: [サーバー間 (S2S) 認証を使用して Web アプリケーションを作成する](build-web-applications-server-server-s2s-authentication.md)。

## <a name="impersonate-another-user-using-the-web-api"></a>Web API を使用して別のユーザーを偽装する

ユーザーを偽装するには、要求を Web サービスに送信する前に、偽装されるユーザーの `systemuserid` に等しい GUID 値を持つ、`MSCRMCallerID` という要求ヘッダーを追加します。 

詳細情報: [Web API を使用して別のユーザーを偽装する](webapi/impersonate-another-user-web-api.md)。


## <a name="impersonate-another-user-using-the-organization-service"></a>組織サービスを使用して別のユーザーを偽装する

他のユーザーを偽装するには、`CallerId` プロパティを偽装ユーザーの GUID 値に設定します。 <xref:Microsoft.Xrm.Sdk.IOrganizationService> を実装している次のクラスは、このプロパティを含んでいます。

- <xref:Microsoft.Xrm.Tooling.Connector.CrmServiceClient>.<xref:Microsoft.Xrm.Tooling.Connector.CrmServiceClient.CallerId>
- <xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceProxy>.<xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceProxy.CallerId>
- <xref:Microsoft.Xrm.Sdk.WebServiceClient.OrganizationWebProxyClient>.<xref:Microsoft.Xrm.Sdk.WebServiceClient.OrganizationWebProxyClient.CallerId>

## <a name="impersonate-another-user-using-plug-ins"></a>プラグインの使用により別のユーザーを偽装する

プラグインを登録し、操作が使用するユーザーを指定することができます。 プラグインのコード内で、この設定を上書きすることができます。
詳細情報: [ユーザーを偽装する](impersonate-a-user.md)


### <a name="see-also"></a>関連項目

[サーバー間 (S2S) の認証を使用して Web アプリケーションを作成する](build-web-applications-server-server-s2s-authentication.md)<br />
[Web API を使用して別のユーザーを偽装する](webapi/impersonate-another-user-web-api.md)<br />
[プラグインを記述する](write-plug-in.md)
