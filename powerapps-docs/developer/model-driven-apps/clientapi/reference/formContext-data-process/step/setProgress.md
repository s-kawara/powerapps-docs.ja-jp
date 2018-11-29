---
title: モデル駆動型アプリにおける setProgress (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 649fe7b0-016d-409f-ba3c-b14e0f1953e0
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="setprogress-client-api-reference"></a>setProgress (クライアント API 参照)



[!INCLUDE[./includes/setProgress-description.md](./includes/setProgress-description.md)]

## <a name="syntax"></a>構文

`stepObj.setProgress(stepProgress,message);`

## <a name="parameters"></a>パラメーター

<table style="width:100%">
<tr>
<th>Name</th>
<th>種類​​</th>
<th>必須出席者</th>
<th>内容</th>
</tr>
<tr>
<td>stepProgress</td>
<td>数値</td>
<td>あり</td>
<td>ステップの進行状況を指定するには、以下のいずれかの値を指定します。
<ul>
<li>0: なし</li>
<li>1: 処理中</li>
<li>2 : 完了</li>
<li>3: 失敗</li>
<li>4: 無効</li>
</ul>
</td>
</tr>
<tr>
<td>メッセージ</td>
<td>String</td>
<td>No</td>
<td><p>ステップのアイコンで alt テキストとして設定されるオプション メッセージ。</td>
</tr>
</table>


## <a name="return-value"></a>戻り値

**種類**: 文字列。 

**説明**: ステップの進行状況が更新されたかどうかに応じて、"無効" または "成功" を返します。

## <a name="remarks"></a>備考

このメソッドは、アクション ステップに対してのみサポートされます。 アクション ステップは、オンデマンド ワークフローまたはアクションをトリガーするためにユーザーがクリックできる、ビジネス プロセスのステージにあるボタンです。 アクション ステップは、v9.0 リリースで導入されたプレビュー機能です。 詳細: 「[ブログ: ビジネス プロセスのフローの新しい自動化およびビジュアル化機能 (パブリック プレビュー)](https://blogs.msdn.microsoft.com/crm/2017/10/25/new-automation-and-visualization-features-for-business-process-flows-public-preview/)」の**アクション ステップを使用したビジネス プロセス フローの自動化**セクションを参照してください。

### <a name="related-topics"></a>関連トピック

[getProgress](getprogress.md)
 
[formContext.data.process](../../formContext-data-process.md)

