---
title: .NET Framework アプリケーションでの認証 (Common Data Service) | Microsoft Docs
description: .NET Framework アプリケーションが Common Data Service で認証する方法
ms.custom: ''
ms.date: 01/25/2019
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: paulliew
ms.author: jdaly
manager: ryjones
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---

# <a name="authentication-with-net-framework-applications"></a>.NET Framework アプリケーションでの認証

.NET Framework を使用している場合、[Xrm.Tooling](/dotnet/api/?view=dynamics-xrmtooling-ce-9) 名前空間内でクラスを使用して認証し、組織サービスおよび Web API に接続できます。

`Xrm.Tooling` クラスで、<xref:Microsoft.Xrm.Sdk.IOrganizationService> インターフェイス メソッドを使用している SDK アセンブリを使用できます。 これはプラグインおよびワークフロー活動で使用されるプログラミングと同じスタイルで、.NET Framework アプリケーションのどこででも使用できる 1 つのスタイルになっています。

`Xrm.Tooling` クラスで、<xref:Microsoft.Xrm.Tooling.Connector> を使用します。<xref:Microsoft.Xrm.Tooling.Connector.CrmServiceClient> クラス。

> [!NOTE]
> 下位レベルの <xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceProxy> または <xref:Microsoft.Xrm.Sdk.WebServiceClient.OrganizationWebProxyClient> クラスを使用している古いコードまたはサンプルを検索する場合があります。 これらはサポートされており廃止されてはいませんが、新しい .NET Framework クライアント アプリケーションの <xref:Microsoft.Xrm.Tooling.Connector.CrmServiceClient> を使用することをお勧めします。

`Xrm.Tooling` クラスの提供する利点には次のものが含まれます。
- 接続文字列を使用して接続情報を定義できます。
- OAuth および Office 365 両方のクレームベース認証をサポートします。
- マルチスレッド環境で実行される操作のためのスレッド セーフ。 
- Windows クライアント アプリケーションから一貫性のあるサインイン エクスペリエンスに対する共通 Windows Presentation Foundation (WPF) ログイン コントロール。
- サインイン資格情報の安全な格納、および最初のサインイン後に自動的にサインインするための、保存された資格情報の再利用のサポート。
- 実行されたアクションの組み込み診断トレースおよびパフォーマンス レポートにより、組織の要求に基づいて構成できます。
- x509 証明書認証をサポートします。

`Xrm.Tooling` クラスは、<xref:Microsoft.Xrm.Sdk.IOrganizationService> インターフェイス メソッドを使用するよう最適化されます。 

Web API の使用を希望する場合は、<xref:Microsoft.Xrm.Tooling.Connector> を使用できます。<xref:Microsoft.Xrm.Tooling.Connector.CrmServiceClient>.<xref:Microsoft.Xrm.Tooling.Connector.CrmServiceClient.ExecuteCrmWebRequest*> OAuth を使用する限り、`Xrm.Tooling` クラスで提供される他のすべての利点を伴う、Web API を使用している要求を構成するメソッドです。

詳細情報: [XRM ツールを使用して Windows のクライアント アプリケーションを作成する](xrm-tooling/build-windows-client-applications-xrm-tools.md)


## <a name="net-framework-versions"></a>.NET Framework バージョン

クライアント アプリケーションを作成するときには、.NET Framework バージョン 4.6.2 以降を使用します。 Transport Level Security (TLS) 1.2 またはそれより優れたセキュリティを使用するアプリケーションのみが接続できます。 TLS 1.2 は .NET Framework 4.5.2 で使用される既定のプロトコルではありませんが、.NET Framework 4.6.2 内にあります。

> [!NOTE]
> **Visual Studio 2015 に関する既知の問題**
> 
> VS 2015 のデバッグモードでプロジェクト/ソリューションを実行していると、接続できなくなることがあります。 これは、4.6.2 以降のターゲットフレームワークを使用しているかどうかにかかわらず発生します。 これは、Visual Studio ホスティングプロセスが .NET 4.5 に対してコンパイルされているために発生します。これは既定で TLS 1.2 がサポートされていないことを意味します。 回避策として、Visual Studio ホスティング プロセスを無効にできます。 
>
> Visual Studio でプロジェクトの名前を右クリックしてから、**プロパティ**をクリックします。 **デバッグ**タブで、**Visual Studio ホスティング プロセスの無効化**オプションをオフにできます。 
>
> これは、VS 2015 のデバッグ エクスペリエンスにのみ影響を与えます。 これは構築されるバイナリまたは実行可能ファイルには影響しません。 同じ問題は、Visual Studio 2017 では発生しません。

## <a name="net-framework-applications-without-sdk-assemblies"></a>SDK アセンブリを使用しない .NET Framework アプリケーション

任意の SDK アセンブリに依存しないことを望む場合、任意の SDK アセンブリに依存せずに [Common Data Service で OAuth を使用する](authenticate-oauth.md) で説明されたパターンを使用することもできます。 SDK アセンブリなしで、OData Restful Web サービス (Web API および OData グローバル検索サービス) のみを使用できます。 [Web API データ操作サンプル (C#)](webapi/web-api-samples-csharp.md) ではこのアプローチを示します。

### <a name="see-also"></a>関連項目

[Common Data Service Web サービスでの認証](authentication.md)<br />
[Common Data Service での OAuth の使用](authenticate-oauth.md)

