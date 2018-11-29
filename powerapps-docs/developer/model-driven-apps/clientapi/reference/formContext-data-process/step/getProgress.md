---
title: モデル駆動型アプリの getProgress (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 56502c8b-af23-40d1-ad97-e780bb757d6d
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getprogress-client-api-reference"></a>getProgress (クライアント API 参照)



[!INCLUDE[./includes/getProgress-description.md](./includes/getProgress-description.md)]

## <a name="syntax"></a>構文

`var stepProgress = stepObj.getProgress();`

## <a name="return-value"></a>戻り値

**種類**: 数値。 

**説明**: 次のいずれかの値を返します。

|Value |内容|
|--|--|
|0|なし​​|
|1|処理しています|
|2|完了しました|
|3|失敗|
|4|無効|

## <a name="remarks"></a>備考

このメソッドは、データ ステップに対してではなく、アクション ステップに対してのみサポートされます。 アクション ステップは、オンデマンド ワークフローまたはアクションをトリガーするためにユーザーがクリックできる、ビジネス プロセスのステージにあるボタンです。 アクション ステップは、v9.0 リリースで導入されたプレビュー機能です。 詳細: [ブログ: 業務プロセス フローの新しい自動化およびビジュアル化機能 (パブリック プレビュー)](https://blogs.msdn.microsoft.com/crm/2017/10/25/new-automation-and-visualization-features-for-business-process-flows-public-preview/) の**アクション ステップによる業務プロセス フローの自動化**セクションを参照してください。

### <a name="related-topics"></a>関連トピック

[setProgress](setprogress.md)

[formContext.data.process](../../formContext-data-process.md)
 


