---
title: PowerApps のチェッカー Web API を使用します | Microsoft Docs
description: PowerApps チェッカー Web API は、各種のプログラミング言語、プラットフォーム、およびデバイスで使用できる開発作業を提供します。
ms.custom: ''
ms.date: 06/3/2019
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
ms.assetid: 0d5f7579-304a-4d28-ba73-df30722205eb
caps.latest.revision: 1
author: mhuguet
ms.author: mhuguet
ms.reviewer: pehecke
manager: maustinjones
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="use-the-powerapps-checker-web-api"></a>PowerApps チェッカー Web API を使用します

[!INCLUDE [cc-beta-prerelease-disclaimer](../../../../includes/cc-beta-prerelease-disclaimer.md)]

PowerApps の Web チェッカー API はカスタマイズに対して実行されたスタティック分析のチェックやプラットフォームを拡張する Common Data Service 機能を提供します。 作成者や開発者は一連のベスト プラクティス ルールに対してソリューションで機能豊富なスタティック分析チェックを実行し、これらの問題となるパターンを識別できます。 サービスは PowerApps メーカー [ポータル](https://make.powerapps.com) の [ソリューション チェッカー機能](../../../../maker/common-data-service/use-powerapps-checker.md) のロジックを提供し、 [AppSource に提出されたアプリケーション](../../publish-app-appsource.md) の自動化の一部として含まれています。 この方式でサービスと直接やり取りすることで、設置型 (すべてのサポートされているバージョン) とOnline環境の一部として含まれているソリューションの分析をおこなうことができます。

 > [!IMPORTANT]
 >
 > - PowerApps のチェッカーの Web API はプレビュー機能です。
 > - [!INCLUDE[cc_preview_features_definition](../../../../includes/cc-preview-features-definition.md)]

<a name="bkmk_altApproaches"></a>

## <a name="alternative-approaches"></a>代替アプローチ

Web API で下位レベルで対話する方法の詳細に関して読見勧める前に、PowerShell モジュール、Microsoft.PowerApps.Checker.PowerShell を代わりに活用することを検討してください。 これは [PowerShell Gallery](https://www.powershellgallery.com) で完全にサポートされているツールです。 現在の制限では、 Windows PowerShell を必要とします。 この要件に合わない場合は、API と直接やり取りすることがおそらく最善の方法です。

<a name="bkmk_getStarted"></a>

## <a name="getting-started"></a>はじめに

ソリューション分析のプロセスに長時間かかってしまうこともあり得ますので注意することが重要です。 カスタマイズとコードの数値、サイズ、複雑性など、さまざまな要因によって、通常60秒から5分強がかかる場合があります。 分析フローはジョブを完了するために使用されるステータス API でジョブ分析の起動を開始する複数かつ非同期のマルチステップです。 分析のためのフロー例は次のとおりです: 

1. OAuth トークンの取得
2. アップロードの呼び出し (各ファイル同時に) 
3. 分析の呼び出し (分析ジョブの起動) 
4. 完了するまでの呼び出し状況 (完了が通知される、またはしきい値が満たされるまで、呼び出し間に一時停止を繰り返す) 
5. 提供された SAS URL から結果をダウンロードします。

いくつかの種類は次のとおりです:

- 前手順とししてのルールセットまたはルールの参照を含みます。 しかし、構成された、またはコーディングされたルールセット ID では、渡すのが若干速くなります。 ニーズに合ったルールセットを使用することをお勧めします。
- アップロードメカニズムを使用しないことを選択できます (制限についてはアップロードを参照してください)。

次を決定する必要があります。

- [どの地域ですか](#determine-a-geography)
- [どのバージョンですか ](#versioning)
- [どのルールセットとルールですか ](#rulesets-and-rules)
- [テナント ID は何ですか。](#find-your-tenant-id)

個々 API 文書用の以下のトピックを参照してください:

[ルールセットの一覧の取得](retrieve-rulesets.md)<br />
[ルールの一覧の取得](retrieve-rules.md)<br />
[ファイルのアップロード](upload-file.md)<br />
[分析を呼び出す](analyze.md)<br />
[分析状態の確認](check-status.md)<br />

<a name="bkmk_geo"></a>

## <a name="determine-a-geography"></a>地域条件の決定

PowerApps のチェッカー サービスと対話するとき、ファイルには、生成されるレポートとともに Azure に一時的に保存されます。 地域固有の API を使用して、データをのどこに保存する方法を制御できます。 分析のライフサイクルに、API 呼び出しで同じ地理条件を使用することをお勧めします。 各地域は、マルチステージの安全な展開のアプローチにより、ある時点でのあらゆる特定ポイントで異なるバージョンを持つ場合があり、これをおこなうことでフルバージョンの互換性を保証します。 また、データの場合は全距離のとして移行する必要がないため、実行時間の短縮かもしあります。 使用可能な地域は次のとおりです:

|Azure Datacenter|Name|地域|基本 URI|
|---|---|---|---|
|パブリック|プレビュー​​|米国|unitedstatesfirstrelease.api.advisor.powerapps.com|
|パブリック|実稼働|米国|unitedstates.api.advisor.powerapps.com|
|パブリック|実稼働|ヨーロッパ|europe.api.advisor.powerapps.com|
|パブリック|実稼働|アジア|asia.api.advisor.powerapps.com|
|パブリック|実稼働|オーストラリア|australia.api.advisor.powerapps.com|
|パブリック|実稼働|日本|japan.api.advisor.powerapps.com|
|パブリック|実稼働|インド|india.api.advisor.powerapps.com|
|パブリック|実稼働|カナダ|canada.api.advisor.powerapps.com|
|パブリック|実稼働|南米|southamerica.api.advisor.powerapps.com|
|パブリック|実稼働|英国|unitedkingdom.api.advisor.powerapps.com|

> [!NOTE]
>  最新機能と変更を組み込む先にプレビュー、地域条件を使用することを選択できます。 ただし、プレビューの米国 Azure 領域のみを使用して、入力します。

<a name="bkmk_versioning"></a>

## <a name="versioning"></a>バージョン管理

必要なされなくても、目的の API バージョンの api バージョンクエリ文字列パラメーターを含めることをお勧めします。 現在の API バージョンは 1.0 です。 たとえば、バージョン1.0 の API を使用を指定するルールセットのHTTP要求には、次があります:

`https://unitedstatesfirstrelease.api.advisor.powerapps.com/api/ruleset?api-version=1.0`

提供されていない場合は、最新バージョンの API が既定で使用されます。 大きな変更あればバージョン番号が増えることから、明示バージョン番号を使用することをお勧めします。 バージョン番号が要求に指定されている場合は、最新 (数字が大きい方) のバージョンで下位互換性サポートが維持されます。

<a name="bkmk_rules"></a>

## <a name="rulesets-and-rules"></a>ルールセットとルール

PowerApps チェッカーには、実行時にルールの一覧が必要です。 このルールでは、個々のルールまたは *[ルールセット]* と呼ばれるグループ化形式で設定できます。 ルールセットは各ルールをここに指定する代わりに、グループ化されたルールを指定する便利な方法です。 たとえば、ソリューションのチェッカー機能は、いう *[ソリューションのチェッカー]* のrulesetを使用します。 新しいルールが追加、または削除されるにつれ、サービスはこれらの変更をアプリケーションの消費による変化を求めることなく自動的に含めます。 ルールの一覧を上記のように自動的に変更しないことが必要な場合は、ルールは個別に指定できます。
ルールセットは制限なしで1つ以上のルールを持つことができます。 ルールには、ルールセットなしや複数のルールセットにすることができます。 API を呼び出すことですべてのルールセットの一覧を次のように取得できます: `[Geographical URL]/api/ruleset`。 このエンドポイントはオープンで、認証は必要ありません。

### <a name="solution-checker-ruleset"></a>ソリューション チェッカー ルールセット

ソリューション チェッカー ルールセットには偽陽性の制限された可能性を持つ一連のインパクトが強いルールが含まれています。 既存のソリューションに対して分析を実行している場合、このルールセットから開始することをお勧めします。 これは [ソリューション チェッカー機能](../../../../maker/common-data-service/use-powerapps-checker.md) によって使用されるルールセットです。

### <a name="appsource-certification-ruleset"></a>AppSource 認証のルールセット

AppSource 上でアプリケーションを公開する場合は、アプリケーションは認証を取得する必要があります。 [AppSource で公開されたアプリケーション](../../publish-app-appsource.md) は高い品質基準を満たす必要があります。 AppSource 認証ルールセットには、ソリューション チェッカー ルールセットの一部であるルール、それに加えてストアで公開されている高品質のアプリケーションのみを確実にするつ以下のルールセットを含みます。 AppSource 認証ルールの一部は偽陽性を起こしやすく、解決するために追加の注意が必要な場合があります。

<a name="bkmk_tenant"></a>

## <a name="find-your-tenant-id"></a>テナント ID を検索します

テナントの ID が、トークンを必要とする API と対話するために必要です。 テナントIDを取得する方法の詳細については、[この記事](https://docs.microsoft.com/en-us/onedrive/find-your-office-365-tenant-id) を参照してください。 テナント ID を取得するために PowerShell コマンドを使用することもできます。 次の例は、[AzureADモジュール](https://docs.microsoft.com/en-us/powershell/module/azuread/?view=azureadps-2.0) のコマンドレットを活用します。

```powershell
# Login to AAD as your user
Connect-AzureAD

# Establish your tenant ID
$tenantId = (Get-AzureADTenantDetail).ObjectId
```

テナント ID は、`Get-AzureADTenantDetail` から返される `ObjectId` プロパティの値です。 コマンドレット出力の Connect-AzureAD コマンドレットを使用してログインした後、表示されるばあいもあります。 この場合は `TenantId` と名づけられます。

<a name="bkmk_auth"></a>

## <a name="authentication-and-authorization"></a>認証および承認

 ルールおよびルールセットの紹介は、OAuth トークンを必要としませんが、他のすべての API は、トークンが必要です。 API はトークンが必要ないかなる API の呼び出しによる認証検出をサポートします。 回答は、WWW 認証ヘッダー、認証 URL、およびリソース ID を持つ 401 の非認証 HTTP ステータス コードになります。 また、 `x-ms-tenant-id` ヘッダーでのテナント ID も提供しなければなりません。 詳細については、 [PowerAppsのチェッカーで認証および承認](/powershell/powerapps/overview#powerapps-checker-authentication-and-authorization) を参照してください。 以下は、API 要求から返される回答ヘッダーの例です:

```http
WWW-Authenticate →Bearer authorization_uri="https://login.microsoftonline.com/0082fff7-33c5-44c9-920c-c2009943fd1e", resource_id="https://api.advisor.powerapps.com/"
```

この情報を一度手に入れれば、 Azure Active Directory 認証ライブラリ (ADAL) またはトークンを取得するための一部のその他メカニズムを使用することを選択できます。 以下は、C# と [ADALライブラリ、バージョン4.5.1](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/4.5.1) を使用してこれをおこなえる方法の例です:

```c#
// Call the status URI as it is the most appropriate to use with a GET.
// The GUID here is just random, but needs to be there.
Uri queryUri = new Uri($"{targetServiceUrl}/api/status/4799049A-E623-4B2A-818A-3A674E106DE5");
AuthenticationParameters authParams = null;

using (var client = new HttpClient())
{
    var request = new HttpRequestMessage(HttpMethod.Get, queryUri);
    request.Headers.Add("x-ms-tenant-id", tenantId.ToString());

    // NOTE - It is highly recommended to use async/await
    using (var response = client.SendAsync(request).GetAwaiter().GetResult())
    {
        if (response.StatusCode == System.Net.HttpStatusCode.Unauthorized)
        {
            // NOTE - It is highly recommended to use async/await
            authParams = AuthenticationParameters.CreateFromUnauthorizedResponseAsync(response).GetAwaiter().GetResult();
        }
        else
        {
            throw new Exception($"Unable to connect to the service for authorization information. {response.ReasonPhrase}");
        }
    }
}
```

一度トークンを取得すれば、要求ライフサイクルで以降の呼び出しをするために同じトークンを提供することが推奨されています。 ただし、追加の要求は、セキュリティ上の理由のために新しいトークンの獲得を保証する可能性があります。

<a name="bkmk_transport"></a>

## <a name="transport-security"></a>トランスポート セキュリティ
クラス最高レベルの暗号化では、チェッカー サービスは Transport Layer Security (TLS) 1.2 以上のみをサポートします。 TLS に関する .NET ベスト プラクティスのガイダンスについては、 [.NET Framework で Transport Layer Security Windows (TLS) のベスト プラクティス](https://docs.microsoft.com/dotnet/framework/network-programming/tls) を参照してください。

<a name="bkmk_report"></a>

## <a name="report-format"></a>レポートの形式

ソリューション分析の結果は、標準化された JSON 形式で 1 つ以上のレポートを含む zip ファイルです。 レポート形式は、スタティック分析結果相互交換形式 (SARIF) として参照されるスタティック分析結果に基づいています。 SARIF 文書の表示とやり取りに使用可能なツールがあります。 詳細はこの [Webサイト](https://sarifweb.azurewebsites.net/) を参照します。 サービスは [OASISの標準](http://docs.oasis-open.org/sarif/sarif/v2.0/sarif-v2.0.html) のバージョン1を活用します。


### <a name="see-also"></a>関連項目

[ルールセットの一覧の取得](retrieve-rulesets.md)<br />
[ルールの一覧の取得](retrieve-rules.md)<br />
[ファイルのアップロード](upload-file.md)<br />
[分析を呼び出す](analyze.md)<br />
[分析状態の確認](check-status.md)<br />