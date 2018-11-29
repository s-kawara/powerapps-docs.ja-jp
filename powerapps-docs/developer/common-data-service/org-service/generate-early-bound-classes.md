---
title: 組織サービスの事前バインド クラスを生成する (アプリ用 Common Data Service) | Microsoft Docs
description: CrmSvcUtil.exe は、アプリ用 Common Data Serviceで使用するコマンド ライン コード生成ツールです。 このツールは、アプリ用 CDS で使用されるエンティティ データ モデルを表す、事前バインドされた .NET Framework クラスを生成します。
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
# <a name="generate-early-bound-classes-for-the-organization-service"></a>組織サービスの事前バインド クラスを生成する

**CrmSvcUtil.exe** は、アプリ用 Common Data Service で使用するコマンド ライン コード生成ツールです。 このツールは、アプリ用 CDS で使用されるエンティティ データ モデルを表す、事前バインドされた .NET Framework クラスを生成します。 コード生成ツール (CrmSvcUtil.exe) が [Microsoft.CrmSdk.CoreTools](https://www.nuget.org/packages/Microsoft.CrmSdk.CoreTools) NuGetパッケージの一部として配布されます。 

> [!NOTE]
> コード生成ツール(CrmSvcUtil.exe)のダウンロードについては、「 [NuGet からツールをダウンロード](../download-tools-NuGet.md)」を参照してください。

## <a name="generate-entity-classes"></a>エンティティ クラスの生成

**CrmSvcUtil.exe** ツールは、組織内のエンティティ用の厳密に型指定されたクラスが含まれる Microsoft Visual C# または Visual Basic .NET 出力ファイルを作成します。 これには、ユーザー定義のエンティティと属性が含まれます。 事前バインドおよびコードの作成を容易にする Visual Studio 内の IntelliSense サポートを提供することにより、この出力ファイルにエンティティごとに 1 つのクラスが格納されます。 生成されるクラスは部分クラスであり、別のファイルにユーザー定義のビジネス ロジックを作成することで拡張できます。 このツールに対する拡張機能を作成することもできます。 詳細については、 [コード生成ツールの拡張機能の作成](extend-code-generation-tool.md)を参照してください。  

## <a name="generate-an-organizationservicecontext-class"></a>OrganizationServiceContext の生成

また、このツールを使用して、エンティティ データ モデルでのエンティティ コンテナーとして動作する <xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext> からの派生クラスを生成することもできます。 このサービス コンテキストを利用して、変更内容を追跡したり、ID、同時実行、および関連付けを管理したりすることができます。 また、このクラスは、アプリ用 CDS でレコードの挿入、更新、および削除を実行する <xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceContext.SaveChanges> メソッドも公開します。 詳細については、 [OrganizationServiceContext の使用](organizationservicecontext.md)を参照してください。  

## <a name="use-generated-classes"></a>生成されたクラスの使用

コード生成ツールによって作成されるクラスは、クラス ライブラリに組み込むことで、アプリ用 CDS を使用するプロジェクトにより参照できるように設計されています。 ツールを使用してクラス ファイルを生成した後で、そのファイルを Visual Studio プロジェクトに追加する必要があります。 また、生成したクラスが依存する複数のアセンブリへの参照を追加する必要があります。  

次は、生成したコード ファイルを使用するときにこのプロジェクトで参照する必要があるアセンブリの一覧です。  

- `Microsoft.Crm.Sdk.Proxy.dll`  
- `Microsoft.Xrm.Sdk.dll ` 

これらのアセンブリは、[Microsoft.CrmSdk.CoreAssemblies](https://www.nuget.org/packages/Microsoft.CrmSdk.CoreAssemblies/) NuGet パッケージに含まれます。 この NuGet パッケージを使用して、これらのアセンブリを Visual Studio プロジェクトへ追加します。

<a name="bkmk_RuntheCodeGenerationUtility"></a>

## <a name="run-the-code-generation-tool"></a>コード生成ツールの実行

コード生成ツールは複数のパラメーターを受け取ります。その値に基づいて、作成するファイルの内容が決定されます。 パラメーターは、ツールを実行するときにコマンドラインから入力するか、.NET に接続されたアプリケーションの構成ファイルに記述して渡すことができます。 

[NuGet からのツールのダウンロード](../download-tools-NuGet.md) で説明されているスクリプトを使用し、ツールをダウンロードしたときに作成された `Tools\CoreTools` フォルダから `CrmSvcUtil.exe` ツールを実行します。 このツールを別の場所のフォルダーから実行する場合は、`Microsoft.Xrm.Sdk.dll` アセンブリのコピーが同じフォルダーにあることを確認します。  

次のサンプルは、アプリ用 CDS でツールをコマンド ラインから実行するときの構文を示しています。 対話型ログインを使用するには、次のオプションを指定するだけで行えます。

```ms-dos
CrmSvcUtil.exe /interactivelogin ^
/out:<outputFilename>.cs ^
/namespace:<outputNamespace> ^
/serviceContextName:<serviceContextName> ^
/generateActions
```

`interactivelogin` (ショートカット `il`) オプションでツールを実行する時に、ダイアログを開いて、ログイン資格情報および接続したいサーバを指定することができます。

コマンド ラインで直接渡すパラメータまたは、新しいクラスを生成するために実行できるバッチ (.bat) ファイルを指定することもできます。

```ms-dos
CrmSvcUtil.exe ^
/url:https://<organizationUrlName>.api.crm.dynamics.com/XRMServices/2011/Organization.svc ^
/out:<outputFilename>.cs ^
/username:<username> ^
/password:<password> ^
/namespace:<outputNamespace> ^
/serviceContextName:<serviceContextName>
```
たとえば、次のようになります。

```ms-dos
CrmSvcUtil.exe ^
/url:https://myorganization.api.crm.dynamics.com/XRMServices/2011/Organization.svc ^
/out:MyOrganizationSdkTypes.cs ^
/username:you@yourOrg.onmicrosoft.com ^
/password:myp455w0rd ^
/namespace:MyOrg ^
/serviceContextName:MyContext
```


> [!NOTE]
> 上記の例では、読みやすさのためにパラメータのリストを分割するために carat (`^`) 文字を使用しています。 メモ帳を使用して引数でコマンド パラメータを構成し、コマンド ラインに貼り付けることができます。

- `username` および `password` パラメータには、アプリ用 CDS にサインインするために使用するユーザー名とパスワードを入力します。 
- `url` パラメータは、**設定**を選択し、**カスタマイズ**に移動して、**開発者リソース**を選択すると、Web アプリケーションで正しい URL を検索することができます。 URL は**組織のサービス**の下に表示されます。  

サポートされているコマンド ライン パラメーターを表示するには、次のコマンドを使用します。

```ms-dos
CrmSvcUtil.exe /?  
```

<a name="bkmk_parameters"></a>

## <a name="parameters"></a>パラメーター

次の表は、コード生成ツールのパラメーターと、それらの使い方の簡単な説明です。  
  
|パラメーター|ショートカット|説明|必須出席者|
|--|--|--|--|
|`deviceid`|`di`|不要になりました|いいえ|
|`devicepassword`|`dp`|不要になりました|いいえ|
|`domain`|`d`|設置型サーバーに接続するときに認証先となるドメイン。|いいえ|
|`url`||組織サービスの URL。|`interactivelogin` を使わない限り、はいです|
|`out`|`o`|生成するコードのファイル名。|はい|
|`language`|`l`|コードを生成する言語。 これは、「CS」または「VB」のいずれかにすることができます。 既定値は 「CS」 です。|いいえ|
|`namespace`|`n`|生成するコードの名前空間。 既定値はグローバル名前空間です。|いいえ|  
|`username`|`u`|認証用のサーバーに接続するときに使用するユーザー名。|いいえ|  
|`password`|`p`|認証用のサーバーに接続するときに使用するパスワード。|いいえ|  
|`servicecontextname`||生成する組織サービス コンテキスト クラスの名前。 値を指定しない場合は、サービス コンテキストが作成されません。|いいえ|
|`help`|`?`|コマンドの使用方法に関する情報を表示します。|いいえ|
|`nologo`||実行時にメッセージを表示しません。|いいえ|
|`generateActions`||定義アクションの要求クラスと応答クラスを生成します。|いいえ|
|`interactivelogin`|`il`|これを使用すると、アプリ用 CDS サービスにログインするためのダイアログが表示されます。 コマンド ラインで指定された他のすべての接続関連パラメーターは無視されます。|いいえ|  
|`connectionstring`|`connstr`|アプリ用 CDS の組織に接続するための、単一文字列として提供される情報を含みます。 コマンド ラインで指定された他のすべての接続関連パラメーターは無視されます。 詳細については、[XRM ツールの接続文字列を使用してアプリ用 Common Data Service に接続する](../xrm-tooling/use-connection-strings-xrm-tooling-connect.md)を参照してください。|いいえ|


<a name="bkmk_sampleconfig"></a>

## <a name="use-the-configuration-file"></a>構成ファイルの使用

CrmSvcUtil.exe.config 構成ファイルは、CrmSvcUtil.exe ツールと同じフォルダーに存在する必要があります。 構成ファイルでは、 `appSettings` セクションに標準のキー/値ペアを使用します。 ただし、コマンドラインから値を入力した場合は、その値が構成ファイル内の値の代わりに使用されます。 アプリケーションの構成ファイルにあるキー/値ペアのうち、想定されているパラメーターのいずれにも一致しないものは無視されます。  

`url` パラメーターと `namespace` パラメーターは、構成ファイルに記述しないでください。 これらは、CrmSvcUtil.exe ツールの実行中にコマンドラインから入力する必要があります。  

次のサンプルは、ショートカット キーを使用して、アプリケーション構成ファイルに出力ファイルとドメイン名のパラメーターを構成する方法を示しています。  

```xml
<appSettings>    
    <add key="o" value="CrmProxy.cs"/>    
    <add key="d" value="mydomain"/>
</appSettings>  
```

<a name="bkmk_enabletrace"></a>

## <a name="enable-tracing"></a>トレースの有効化
 ツール実行中のトレースを有効にするには、次の行を構成ファイルに追加します。  

```xml
<system.diagnostics>   
   <trace autoflush="false" indentsize="4">   
      <listeners>   
         <add name="configConsoleListener" type="System.Diagnostics.ConsoleTraceListener">   
            <filter type="System.Diagnostics.EventTypeFilter" initializeData="Error" />   
         </add>   
      </listeners>   
   </trace>   
</system.diagnostics>  
```

サポートされているトレース オプションの詳細については、 [XRMツールのトレースの構成](../xrm-tooling/configure-tracing-xrm-tooling.md)参照してください。  

## <a name="community-tools"></a>コミュニティ ツール

**事前バインド ジェネレーター**は、XrmToolbox コミュニティのツールです。 コミュニティ開発ツールの詳細については、[開発者のツールとリソース](../developer-tools.md)トピックを参照してください。

> [!NOTE]
> コミュニティ ツールは Microsoft の製品ではなく、コミュニティ ツールに対するサポートは提供されません。 このツールに関するご質問は、その発行元にお問い合わせください。 詳細: [XrmToolBox](https://www.xrmtoolbox.com)。 


### <a name="see-also"></a>関連項目

[開発者のツールとリソース](../developer-tools.md)<br />
[コード生成ツール用の拡張機能の作成](extend-code-generation-tool.md)<br />
[NuGet からツールをダウンロード](../download-tools-NuGet.md)