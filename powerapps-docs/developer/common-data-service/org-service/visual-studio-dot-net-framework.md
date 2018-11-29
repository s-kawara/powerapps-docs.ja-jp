---
title: Visual Studio および .NET Framework (アプリ用 Common Data Service) | Microsoft Docs
description: マネージド コードの開発ツールと要件について説明します。
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
# <a name="visual-studio-and-the-net-framework"></a>Visual Studio および .NET Framework

アプリ用 Common Data Service の .NET SDK アセンブリは、.NET Framework 4.5.2 で構築されます。 

.NET Framework 4.5.2 またはそれ以降を使用してマネージ コード コンソール アプリケーションを構築するには、Visual Studio を使用できます。 

> [!IMPORTANT]
> ユーザー定義のクライアント アプリケーションを作成するには、Microsoft .NET Framework 4.6.2 またはそれ以降を使用する必要があります。
> Transport Level Security (TLS) 1.2 またはそれより優れたセキュリティを使用するアプリケーションのみがアプリ用 CDS との接続を許可されます。 TLS 1.2 は .NET Framework 4.5.2 で使用される既定のプロトコルではありませんが、.NET Framework 4.6.2 内にあります。
> 
> 詳細情報: [ブログ投稿: Dynamics 365 Customer Engagement 接続のセキュリティに予定されている更新](https://blogs.msdn.microsoft.com/crm/2017/09/28/updates-coming-to-dynamics-365-customer-engagement-connection-security/)
> 
> [!TIP]
> 開発用コンピューターに .NET Framework 4.6.2 をインストールする場合、ランタイムだけでなく開発者パックのインストールを実行してください。 これにより、4.6.2 フレームワークを、Visual Studio の**新しいプロジェクト**ダイアログ ボックスおよびプロジェクトのプロパティのターゲット フレームワーク ドロップダウン メニューで選択できるようになります。  

開発に Visual Studio Community エディションを使用できます。 

[comment]: <> (However, use of extensions isn’t supported in the Express edition so you won’t be able to install useful extensions in that version of Visual Studio)

詳細: [サポートされる .NET Framework のバージョン](/dynamics365/customer-engagement/developer/supported-extensions#SupportNET)

サポートされる開発およびサポートされていない開発に関する声明の全文については、「[Dynamics 365 でサポートされる拡張](/dynamics365/customer-engagement/developer/supported-extensions#SupportNET)」を参照してください。

## <a name="see-also"></a>関連項目

 [開発者ツール](/dynamics365/customer-engagement/developer/developer-tools)