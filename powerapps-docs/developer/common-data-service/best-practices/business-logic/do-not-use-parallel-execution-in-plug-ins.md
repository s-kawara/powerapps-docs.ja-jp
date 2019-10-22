---
title: プラグインおよびワークフロー アクティビティ内でパラレル実行を使用しないでください | MicrosoftDocs
description: プラグインまたはカスタム ワークフロー アクティビティ内では、マルチスレッドまたは並列スレッドはサポートされていません。
services: ''
suite: powerapps
documentationcenter: na
author: JimDaly
manager: ryjones
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/14/2019
ms.author: pehecke
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="do-not-use-parallel-execution-within-plug-ins-and-workflow-activities"></a>プラグインおよびワークフロー アクティビティ内でパラレル実行を使用しないでください

**カテゴリ**: 設計、パフォーマンス、セキュリティ、サポート性

**影響の可能性**: 高い

<a name='symptoms'></a>

## <a name="symptoms"></a>現象

プラグイン内でののマルチスレッドまたは並列スレッドの呼び出し、またはカスタム ワークフロー アクティビティーを使用することで、これらの接続が損なわれる可能性があります。  たとえば、並列スレッドを実行すると、以下のような例外処理が引き起こされます:

`Generic SQL error.`
`The transaction active in this session has been committed or aborted by another session.`

また、 [System.Collections 名前空間](/dotnet/api/system.collections) 内の項目などの非スレッド セーフなオブジェクトは、パラレル スレッドによって損なわれる可能性があります。

<a name='guidance'></a>

## <a name="guidance"></a>ガイダンス

サンドボックス サービスは、トランザクションの一部として特定の順序で呼び出し処理を実行するように設計されています。  並列スレッド、またはマルチスレッドの呼び出し処理をするためのプラグイン、またはカスタム ワークフロー アクティビティの開発には対応していません。  プラグインとカスタム ワークフロー アクティビティーを開発するには、呼び出し処理が順番通りに実行され、ロールバックが必要になる場合もあることを理解することが前提となります。

> [!NOTE]
> クライアント プログラムから並列処理を実行することで、必要に応じてパフォーマンスを最適化することができます。 この参考例は、プラグインまたはカスタム ワークフロー アクティビティ内で実行するように記述されたコードに特化した方法です。

<a name='problem'></a>

## <a name="problematic-patterns"></a>問題となるパターン

プラグインおよびカスタム ワークフロー アクティビティは単一のトランザクション内で実行され、パラレル実行によって複数のスレッドが発生すると、トランザクションが破損してしまう可能性があります。 プラグインおよびカスタム ワークフロー アクティビティ内で使用するべきではないパターンと実用例を以下に示します:

- [タスクベースの非同期パターン (TAP)](/dotnet/standard/asynchronous-programming-patterns/task-based-asynchronous-pattern-tap)の使用
- [タスク並列ライブラリ(TPL)](/dotnet/standard/parallel-programming/task-parallel-library-tpl)の使用
- [管理スレッド](/dotnet/standard/threading/index)の使用


<a name='additional'></a>

## <a name="additional-information"></a>追加情報

共有パイプライン コンテキスト オブジェクトの使用および更新を行うと、これらのオブジェクトが予期しない結果となったり、破損したりする可能性があります。 これにより、プラグインまたはカスタム ワークフロー アクティビティでエラーが発生します。 

<a name='seealso'></a>

### <a name="see-also"></a>関連項目

[.NETにおける並列処理、並行性、非同期プログラミング](/dotnet/standard/parallel-processing-and-concurrency)<br />