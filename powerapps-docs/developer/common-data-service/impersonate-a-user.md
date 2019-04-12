---
title: ユーザーを偽装する (Common Data Service) | Microsoft Docs
description: 特定のユーザーに代わってプラグイン コードを記述する方法を説明します。
ms.custom: ''
ms.date: 1/24/2019
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: JimDaly
ms.author: pehecke
manager: kvivek
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="impersonate-a-user"></a>ユーザーを偽装する

別のユーザーのコンテキストで実行するためのプラグインのコードが必要になる場合があります。たとえば、そのユーザーに代わって操作を実行するときです。

プラグインの偽装を適用する 2 つの方法があります: 登録または実行。

## <a name="at-plug-in-registration"></a>プラグイン登録で

プラグイン ステップを登録する場合、**ユーザーのコンテキストで実行**オプションから選択して、コードの実行時に使用するユーザー アカウントを指定できます。 既定では、これは**呼び出し元ユーザー**を使用して設定され、これはアクションを開始したユーザー アカウントです。 このデフォルト オプションが適用される場合、[SdkMessageProcessingStep.ImpersonatingUserId](reference/entities/sdkmessageprocessingstep.md#BKMK_ImpersonatingUserId) は null または <xref:System.Guid.Empty> に設定されます。

詳細: [プラグイン ステップの登録](register-plug-in.md#register-plug-in-step)

## <a name="during-plug-in-execution"></a>プラグイン実行の間

<xref:Microsoft.Xrm.Sdk.IOrganizationServiceFactory>.<xref:Microsoft.Xrm.Sdk.IOrganizationServiceFactory.CreateOrganizationService(System.Nullable{System.Guid})> を設定することによって、実行時に、登録時に指定した設定を上書きできます `userId`パラメーター。

これはに通常、<xref:Microsoft.Xrm.Sdk.IExecutionContext>.<xref:Microsoft.Xrm.Sdk.IExecutionContext.UserId> に設定されます プラグイン ステップ登録によって定義されたユーザー アカウントを適用する値。

```csharp
(IOrganizationServiceFactory)serviceProvider.GetService(typeof(IOrganizationServiceFactory));
    IOrganizationService service = serviceFactory.CreateOrganizationService(context.UserId);
```

ステップ登録を上書きする場合は、<xref:Microsoft.Xrm.Sdk.IExecutionContext>.<xref:Microsoft.Xrm.Sdk.IExecutionContext.InitiatingUserId> の値を渡すことができます プラグインが実行されたアクションを開始したユーザー アカウントを使用するサービスを所持すること。

さらに、任意の有効なユーザー アカウントから [SystemUser.SystemUserId](reference/entities/systemuser.md#BKMK_SystemUserId) を提供することもできます。 これは、そのユーザーがプラグインで操作を実行するアクセス許可を持つそのユーザーである限り、機能します。

### <a name="see-also"></a>関連項目

[プラグイン](plug-ins.md)  
[プラグインを記述する](write-plug-in.md)