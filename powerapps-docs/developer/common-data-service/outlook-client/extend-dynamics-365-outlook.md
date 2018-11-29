---
title: Dynamics 365 for Outlook を拡張する (アプリ用 Common Data Service) | Microsoft Docs
description: Outlook 用 Dynamics 365 では、ユーザーはオフラインでサーバーに接続していない状態でも、データとやり取りすることができます。 アプリ用 Common Data Service は、カスタム コードから Web サービス オフラインを呼び出すことによってソリューションをオフラインのシナリオに拡張する機能を備えています。 また、SDK アセンブリで、同期、オフラインとオンラインの切り替え、Outlook 用 Dynamics 365 の状態の検証など、Outlook の基本的なアクションのプログラム的なサポートが提供されています。 オフライン プログラミングでは、ASP.NET Development Server を使用します。
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: sriharibs
ms.author: jdaly
manager: ryjones
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
<!-- https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/extend-customer-engagement-outlook 

This topic should be in powerapps-docs/developer/common-data-service/outlook-client/
-->

# <a name="extend-dynamics-365-for-outlook"></a>Dynamics 365 for Outlook を拡張

> [!IMPORTANT]
> 2018 年 1 月 29 日の時点で、圧倒される顧客フィードバックおよび顧客へのサポートを継続したいという願いに基づき、**Dynamics 365 for Outlook を廃止しないことを決定しました** (Outlook アドイン)。 詳細については、[このブログの投稿](https://blogs.msdn.microsoft.com/crm/2018/01/29/continued-support-for-outlook-add-in-dynamics-365-for-outlook/)をお読みください。

Microsoft Dynamics 365 for Outlook では、オフラインでサーバーに接続していない状態でも、データのやり取りすることができます。 アプリ用 CDSは、カスタム コードから Web サービス オフラインを呼び出すことによって、オフラインのシナリオでソリューションを拡張する機能を備えています。 さらに、<xref:Microsoft.Crm.Outlook.Sdk> アセンブリでは、同期、オフラインとオンラインの切り替え、Dynamics 365 for Outlook の状態の検証など、Outlook の基本的なアクションのプログラム的なサポートを提供しています。 オフライン プログラミングでは、ASP.NET Development Server を使用します。  
  
 Dynamics 365 では、管理者がユーザーのフィルターをカスタマイズして管理できるようにする機能を備えています。 フィルター テンプレートは、Dynamics 365 for Outlook のエンティティの同期の開始点を提供します。 フィルターは、オフライン対応の Dynamics 365 ソリューションのために Outlook および SQL Server 2008 Express Edition に同期するエンティティ コレクションを決定します。  
  
## <a name="in-this-section"></a>このセクションの内容

[オフラインと Outlook のフィルターおよびテンプレート](offline-outlook-filters-templates.md)<br />  
[サンプル: Outlook フィルターの取得](sample-create-retrieve-outlook-filters.md)<br />  
[サンプル: Outlook メソッドの使用](sample-outlook-methods.md)<br />
  
## <a name="related-sections"></a>関連セクション

<!-- TODO:
[Extend Dynamics 365](extend-dynamics-365-server.md)<br />
[Supported Extensions for Dynamics 365](supported-extensions.md)<br />
[The Metadata and Data Models in Dynamics 365](metadata-data-models.md)<br />
[Extend Dynamics 365 on the server](extend-dynamics-365-server.md)<br />
[Extend Dynamics 365 on the client](extend-client.md)<br />
[Customize Dynamics 365 applications](customize-dev/customize-applications.md)<br />
[Package and distribute extensions using solutions](package-distribute-extensions-use-solutions.md)<br />
[Integrate Dynamics 365 with SharePoint](integration-dev/integrate-sharepoint.md)<br />
 -->
<xref href="Microsoft.Dynamics.CRM.savedquery?text=savedquery EntityType" /><br />
[SavedQuery エンティティ](../reference/entities/savedquery.md)<br />
  

