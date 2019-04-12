---
title: API の制限 (Common Data Service) | Microsoft Docs
description: API 要求に対する制限について理解します。
ms.custom: ''
ms.date: 03/21/2019
ms.reviewer: kvivek
ms.service: powerapps
ms.topic: article
author: brandonsimons
ms.author: bsimons
manager: annbe
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="api-limits"></a>API の制限

組織インスタンスごとに各ユーザーが 5 分間のスライド枠で実行する API 要求の数を制限します。 また、一度に受信する同時リクエストの数を制限します。  これらの制限のひとつを超えると、例外がプラットフォームによってスローされます。

この制限はアプリケーションを実行しているユーザーが、リソースの制約に基づいて互いに干渉できないようにします。 これらの制限はプラットフォームの標準ユーザーに影響しません。 影響を受ける可能性があるのは多数の API 要求を実行するアプリケーションのみです。 この制限は Common Data Service プラットフォームの可用性とパフォーマンス特性に対する脅威となる、ランダムに発生する予期しない要求数の急増に備えて一定レベルの保護を提供します。

アプリケーションがその制限を超える可能性がある場合は、以下の [アプリケーションが制限を超える場合に実行する内容](#what-should-i-do-if-my-application-exceeds-the-limit) セクション内で指定されたガイダンスを考慮してください。

## <a name="what-happens-when-the-limit-is-exceeded"></a>制限を超えると何が発生しますか

制限を超えると、同じユーザーに対するすべての要求に対してエラー応答が返されます。

.NET SDK アセンブリを使用している場合、プラットフォームは `FaultException<OrganizationServiceFault>` WCF エラーで応答します。  

| エラー コード | メッセージ |
|------------|-------------------------------------|
|`-2147015902`|`Number of requests exceeded the limit of 4000, measured over time window of 300 seconds.`|
|`-2147015903`|`Combined execution time of incoming requests exceeded limit of 1,200,000 milliseconds over time window of 300 seconds. Decrease number of concurrent requests or reduce the duration of requests and try again later.`|
|`-2147015898`|`Number of concurrent requests exceeded the limit of X`|

HTTP 要求を使用する場合、応答には同じメッセージと下記が含まれます:<br />
`StatusCode` : `429`

API 要求の量が制限を下回るまで、すべての要求に対してこれらのエラー応答が返されます。 これらの応答を受ける場合、要求量が制限を下回るまで、アプリケーションは API 要求の送信を停止する必要があります。

## <a name="what-should-i-do-if-my-application-exceeds-the-limit"></a>アプリケーションが制限を超える場合何をする必要がありますか

アプリケーションが制限を超えるとき、サーバーからのエラー応答により、さらに要求を送信するまで待機する必要がある時間量が指定される可能性があります。 SDK アセンブリまたは HTTP 要求を使用する場合、応答オブジェクトは少し異なります。

ベスト プラクティスの詳細については、[Azure アーキテクチャ ベスト プラクティスでの一時的なエラー処理](/azure/architecture/best-practices/transient-faults)を参照してください

[Polly Project](http://www.thepollyproject.org/) は、実行ポリシーを使用して一時的なエラーを処理する機能を含むライブラリです。

### <a name="http-requests"></a>HTTP 要求

HTTP 要求を使用する場合、エラー応答に含まれる `Retry-After` HTTP ヘッダーを検索することができます。 これには、フォローアップ要求を実行するまで待機する必要がある時間を示す秒単位の値が含まれます。 詳細 [MDN Web ドキュメントの後に試行](https://developer.mozilla.org/docs/Web/HTTP/Headers/Retry-After)

### <a name="sdk-assemblies"></a>SDK アセンブリ

SDK アセンブリを使用する場合、`Retry-After` 遅延を <xref:Microsoft.Xrm.Sdk.OrganizationServiceFault>.<xref:Microsoft.Xrm.Sdk.BaseServiceFault.ErrorDetails> プロパティ内で検索するには、`"Retry-After"` キーを使用することができます。 返される値は [TimeSpan](/dotnet/api/system.timespan) オブジェクトです。

### <a name="net-sdk-assembly-example"></a>.NET SDK アセンブリの例

次の例は以下で説明される [Retry クラス](#retry-class)を使用して、<xref:Microsoft.Xrm.Sdk.IOrganizationService>.<xref:Microsoft.Xrm.Sdk.IOrganizationService.RetrieveMultiple*>  メソッドを使用するアカウントを取得します。 API 制限を超えたために要求が失敗する場合、`Retry` クラスはサーバーが指定する遅延に応じて待機してから再試行します。

```csharp
var qe = new QueryExpression("account") { TopCount = 1 };
EntityCollection result = Retry.Do(() => service.RetrieveMultiple(qe));
```

#### <a name="retry-class"></a>Retry クラス

`Retry` クラスは、既知の <xref:Microsoft.Xrm.Sdk.OrganizationServiceFault> エラー コードに基づき、一時的エラーのために失敗する要求を再試行する方法を示します。 `Retry` クラスは再試行まで待機します。 エラーが再試行遅延を指定する場合、サーバーが指定する遅延に基づき待機します。 それ以外の場合、急激なバックオフを使用して、実行された再試行の数に応じて遅延が計算されます。

```csharp
using System;
using System.ServiceModel;
using System.Threading;

public class Retry
{
    private const int RateLimitExceededErrorCode = -2147015902;
    private const int TimeLimitExceededErrorCode = -2147015903;
    private const int ConcurrencyLimitExceededErrorCode = -2147015898;

    public static TResult Do<TResult>(Func<TResult> func, int maxRetries = 3)
    {
        int retryCount = 0;

        while (true)
        {
            try
            {
                return func();
            }
            catch (FaultException<Microsoft.Xrm.Sdk.OrganizationServiceFault> ex) 
                when (IsTransientError(ex))
            {
                if (++retryCount >= maxRetries)
                {
                    throw;
                }

                if (ex.Detail.ErrorCode == RateLimitExceededErrorCode)
                {
                    // Use Retry-After delay when specified
                    delay = (TimeSpan)ex.Detail.ErrorDetails["Retry-After"];
                }
                else
                {
                    // else use exponential backoff delay
                    delay = TimeSpan.FromSeconds(Math.Pow(2, retryCount));
                }

                Thread.Sleep(delay);
            }
        }
    }

    private static bool IsTransientError(FaultException<Microsoft.Xrm.Sdk.OrganizationServiceFault> ex)
    {
        // You can add more transient fault codes to retry here
        if (ex.Detail.ErrorCode == RateLimitExceededErrorCode ||
            ex.Detail.ErrorCode == TimeLimitExceededErrorCode ||
            ex.Detail.ErrorCode == ConcurrencyLimitExceededErrorCode)
        {
            return true;
        }

        return false;
    }
}
```

### <a name="see-also"></a>関連項目

[Common Data Service Web API の使用](webapi/overview.md)<br />
[Common Data Service 組織サービスを使用する](org-service/overview.md)<br />
[Web API を使用してバッチ操作を実行する](webapi/execute-batch-operations-using-web-api.md)<br />
[大量データ負荷でパフォーマンスを向上させる ExecuteMultiple を使用する](org-service/execute-multiple-requests.md)
