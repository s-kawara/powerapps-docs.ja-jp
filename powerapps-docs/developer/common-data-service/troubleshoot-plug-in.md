---
title: プラグインのトラブルシューティング (アプリ用 Common Data Service) | Microsoft Docs
description: プラグインが原因で発生する可能性があるエラーと、その修正方法に関する情報が含まれます。
ms.custom: ''
ms.date: 04/21/2019
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: JimDaly
ms.author: jdaly
manager: ryjones
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="troubleshoot-plug-ins"></a>プラグインのトラブルシューティング 

このトピックには、プラグインが原因で発生する可能性があるエラーと、その修正方法に関する情報が含まれます。

## <a name="error-there-is-no-active-transaction"></a>エラー: アクティブなトランザクションがありません。 

エラー コード: `-2147220911`<br />
エラー メッセージ: `There is no active transaction. This error is usually caused by custom plug-ins that ignore errors from service calls and continue processing.`

他人のコードが原因の場合があり、これは対処が難しいエラーになる可能性があります。 このメッセージを理解するには、同期プラグイン内でデータ操作に関連したエラーが発生した場合に、操作全体のトランザクションが終了することを認識する必要があります。
[Common Data Service のスケーラブル カスタマイズ設計](scalable-customization-design/overview.md) 最も一般的な原因は、単に開発者が成功する *かもしれない* 操作を実行できると信じることで、その操作を try / catch ブロックでラップして、失敗したらエラーを吸収しようとします。

これはクライアント アプリケーションでは有効ですが、プラグイン実行中にはデータ操作の失敗によってトランザクション全体がロール バックされます。 エラーを吸収できないので、必ず <xref:Microsoft.Xrm.Sdk.InvalidPluginExecutionException> を返す必要があります。

## <a name="error-sql-error-execution-timeout-expired"></a>エラー: SQL エラー: 実行タイムアウト期限切れ

エラー コード: `-2147204783`<br />
エラー メッセージ: `Sql error: 'Execution Timeout Expired.  The timeout period elapsed prior to completion of the operation or the server is not responding.'`

SQL タイムアウト エラーの発生には様々な理由があります。

### <a name="blocking"></a>ブロック

ブロックは SQL タイムアウト エラーの最も一般的な原因であり、これは操作が別の SQL トランザクションがロックしたリソースを待っています。 このエラーは、システムがデータの整合性とユーザーのパフォーマンスに影響を与える長時間の要求から保護しているためです。

ブロックは並行した他の操作が原因の可能性があります。 あなたのコードはテスト環境では独立して問題なく動作するにも関わらず、複数のユーザーがプラグインのロジックを起動した場合にのみ発生する状況の影響を受ける場合があります。

プラグインを書くときは、スケーラブルなカスタマイズの設計方法を理解することが重要です。 詳細: [Common Data Service のスケーラブル カスタマイズ設計](scalable-customization-design/overview.md)

### <a name="cascade-operations"></a>カスケード操作

レコードの割り当てや削除などプラグインで行う特定の操作が、関連レコードのカスケード操作を開始することがあります。 これらのアクションが関連レコードにロックを適用し、その後のデータ操作をブロックして SQL タイムアウトを発生させる可能性があります。 

プラグインのデータ操作でこれらのカスケード操作の影響を考慮する必要があります。 詳細: [エンティティ関係の動作](../../maker/common-data-service/entity-relationship-behavior.md)

これらの動作は環境によって異なる方法で構成できるため、環境が同じように設定されていない限り動作を再現するのは困難です。

### <a name="indexes-on-new-entities"></a>新しいエンティティのインデックス

プラグインが最近作成されたエンティティや属性を使用して操作を実行している場合、インデックスを管理する Azure SQL の機能のいくつかは数日後に効果が出る場合があります。

## <a name="errors-due-to-user-privileges"></a>ユーザー特権によるエラー

クライアント アプリケーションではユーザーが実行を許可されていないコマンドを無効にできます。 プラグインにはこれがありません。 あなたのコードは、呼び出し元のユーザーが実行する特権を持っていない自動化を含んでいる可能性があります。

ユーザーに **ユーザーのコンテキストで実行** 値を設定することで、正しい特権を確かに持っているユーザーのコンテキストで実行するようプラグインを登録できます。 または他のユーザーに偽装して操作を実行できます。 詳細:
 - [プラグインの登録](register-plug-in.md)
 - [ユーザーを偽装する](impersonate-a-user.md)

<!-- But if you prefer that the logic in your plug-in adapt to the privileges that the calling user has, you really need to verify the user's privileges in your code.

TODO: Add content that shows how to do this -->