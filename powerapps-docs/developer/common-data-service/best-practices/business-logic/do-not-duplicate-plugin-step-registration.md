---
title: プラグイン ステップ登録を重複させない | MicrosoftDocs
description: プラグイン ステップ登録を重複させると、同じメッセージまたはイベントに対してプラグインが複数回実行されます。
services: ''
suite: powerapps
documentationcenter: na
author: jowells
manager: austinj
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 1/15/2019
ms.author: jowells
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="do-not-duplicate-plug-in-step-registration"></a>プラグイン ステップ登録を重複させない

**カテゴリ**: パフォーマンス

**影響の可能性**: 高い

<a name='symptoms'></a>

## <a name="symptoms"></a>現象

プラグイン ステップ登録を重複させると、同じメッセージまたはイベントに対してプラグインが複数回実行されます。 これは次の現象を招きます:

- 非同期実行モードとして登録されると、非同期ジョブのプロセスが遅れる。
- 同期実行モードとして登録されると、ユーザー パフォーマンス エクスペリエンスが低下する。 エクスペリエンスには次のものが含まれます:
    - モデル駆動アプリが応答しない
    - クライアント対話が遅くなる
    - ブラウザーが応答を停止する

<a name='guidance'></a>

## <a name="guidance"></a>ガイダンス

削除して再作成するのではなく、現存するプラグイン登録ステップを更新してください。  また、サポートされている手法のプラグイン登録ステップのみを作成および更新してください。

<a name='problem'></a>

## <a name="problematic-patterns"></a>問題となるパターン

> [!WARNING]
> これらのパターンは、回避する必要があります。

ソース インスタンス (test、dev、preprod) のステップが削除および再作成されると、そのステップが以前に登録されていた場合は、ターゲット環境で登録されている重複ステップも作成します。

![プラグイン ステップ登録の重複](../media/duplicate-plugin-registration-step.png)

新しい GUID で `SDKMessageProcessingSteps` を手動で作成するか `customizations.xml` ファイル内で既存の GUID を更新すると、重複ステップが登録されることになります。 [カスタマイズ ファイルを編集するとき](/powerapps/developer/model-driven-apps/when-edit-customization-file) で説明されているように、これらのタスクの種類はサポートされていません。

<a name='additional'></a>

## <a name="additional-information"></a>追加情報

イベントが更新メッセージに登録されると、プラグイン ステップ登録の重複により SQL のデッドロックが発生する可能性があります。 レコードの更新が発行されると、SQL はそのレコードの行のロックを作成します。 別のトランザクションが同じレコードを更新しようとする場合、更新が可能になる前にロックがリリースされるまで待つ必要があります。 タイムアウトが発生すると、トランザクションがロールバックされて、更新は SQL データベースにコミットされません。

<a name='seealso'></a>

### <a name="see-also"></a>関連項目

[プラグインの登録](../../register-plug-in.md)
[デッドロック](https://technet.microsoft.com/library/ms177433.aspx)<br />
