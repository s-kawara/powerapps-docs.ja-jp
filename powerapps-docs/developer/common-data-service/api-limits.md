---
title: API の制限 (アプリ用 Common Data Service) | Microsoft Docs
description: API 要求に対する制限について理解します。
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: MicroSri
ms.author: jdaly
manager: ryjones
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="api-limits"></a>API の制限

2018 年 3 月 19 日から、組織インスタンスごとに、ユーザーが 5 分間隔内に実行する API 要求の数を制限します。 この制限を超えると、例外がプラットフォームによってスローされます。

この制限は、サーバーに対して非常に高い負荷がかかるアプリケーションを実行しているユーザーによって他のユーザーが影響を受けないようにするために役立ちます。 この制限がプラットフォームの標準的なユーザーに影響することはありません。 影響を受けるのは、非常に多数の API 要求を実行するアプリケーションのみです。 この制限はテレメトリ データの分析に基づいており、API 要求を多数実行するほとんどのアプリケーションはこの範囲内に十分収まります。 この制限は、アプリ用 Common Data Service プラットフォームの可用性とパフォーマンス特性に対する脅威となる、ランダムに発生する予期しない要求数の急増に備えて一定レベルの保護を提供します。

アプリケーションがその制限を超える可能性がある場合は、以下の [アプリケーションが制限を超える場合に実行する内容](#what-should-i-do-if-my-application-exceeds-the-limit) セクション内で指定されたガイダンスを考慮してください。

## <a name="what-is-the-limit"></a>制限とは何ですか

各ユーザーは、組織インスタンスごとに、5 分のスライド間隔内で、最大 60,000 の API 要求を許可されます。

## <a name="what-happens-when-the-limit-is-exceeded"></a>制限を超えると何が発生しますか

制限を超えると、すべての要求に対してエラー応答が返されます。

.NET SDK アセンブリを使用する場合、プラットフォームは `FaultException<OrganizationServiceFault>` WCF エラー、エラーコード `-2147015902` およびメッセージ `Number of requests exceeded the limit of 60000, measured over time window of 300 seconds.` を応答します

HTTP 要求を使用する場合、応答には以下のプロパティが含まれます。<br />
`StatusCode` : `429`<br />
`Message` : `Number of requests exceeded the limit of 60000, measured over time window of 300 seconds.`

API 要求の量が制限を下回るまで、すべての要求に対してこれらのエラー応答が返されます。 これらの応答を受ける場合、要求量が制限を下回るまで、アプリケーションは API 要求の送信を停止する必要があります。

## <a name="how-is-this-limit-calculated"></a>この制限はどのように計算されますか

組織インスタンス内では、(自動化の実行に使用されるライセンス ID を含む) ライセンスを受けた個々のユーザーが実行した API 要求はこの制限に対して測定されます。 プラットフォームは 5 分内 (一定期間でスライド) に実行された API 要求量を測定します。 各測定間隔内の、5 分の最後に、ユーザーによる API 要求量が数えられます。 次の図では、3 人のユーザーが 6 分の期間にわたり API コール要求を実行します。  

![api 制限の実装](media/api-limit-implementation-1.png)

|間隔|内容|
|--|--|
|A|5 分の最後に、ユーザー 1 の API 要求の総数は 6K で、ユーザー 2 は 3K で、ユーザー 3 は 10K です。|
|B|5+X 分で、プラットフォームはこれらアクティブな状態にあるユーザーのための合計を測定します。X はスライドする間隔定数である時間の一定スライスです (たとえば、数秒)。 上の図によれば、ユーザー 1 は 7k、ユーザー 2 は 6k、およびユーザー 3 は 25k になります。 すべての累積数は 60,000 の制限を下回っているため、これらのユーザーに対する動作の変更は生じません。|
|C|時間が経過して 5+2X に達すると、ユーザー 3 は 40k API 要求を実行し、ユーザー 1 およびユーザー 2 はそれぞれ 8K および 9K のコールを実行します。 この結果、ユーザー 3 は 5 分以内に 65K API 要求に達し、これにより 5K (65K-60K=5K) の要求が拒否されます。|

> [!NOTE]
> .NET SDK アセンブリを使用する <xref:Microsoft.Xrm.Sdk.Messages.ExecuteMultipleRequest> または <xref:Microsoft.Xrm.Sdk.Messages.ExecuteTransactionRequest>、または Web API を使用する `$batch` のような複数の API 要求を実行する要求は、この制限の計算では単一の要求として数えられます。 ただし、これらの種類のオペレーションの場合、これらの API 要求は[ランタイムの制限](org-service/execute-multiple-requests.md#limitations)に従う必要があります。

## <a name="what-should-i-do-if-my-application-exceeds-the-limit"></a>アプリケーションが制限を超える場合何をする必要がありますか

アプリケーションが制限を超えるとき、サーバーからのエラー応答により、さらに要求を送信するまで待機する必要がある時間量が指定されます。 SDK アセンブリまたは HTTP 要求を使用する場合、応答オブジェクトは少し異なります。

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
        if (ex.Detail.ErrorCode == RateLimitExceededErrorCode)
        {
            return true;
        }

        return false;
    }
}

```



### <a name="see-also"></a>関連項目

[アプリ用 CDS Web API を使用](webapi/overview.md)<br />
[アプリ用 CDS 組織サービスを使用](org-service/overview.md)<br />
[Web API を使用してバッチ操作を実行する](webapi/execute-batch-operations-using-web-api.md)<br />
[大量データ負荷でパフォーマンスを向上させる ExecuteMultiple を使用する](org-service/execute-multiple-requests.md)