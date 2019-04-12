---
title: ユーザー定義のアセンブリ開発を最適化する | MicrosoftDocs
description: 個々のプラグイン/ユーザー定義ワークフロー活動を単一のカスタム アセンブリに統合してパフォーマンスおよび保守性を改善し、アセンブリ サイズがサンドボックス アセンブリ サイズの上限に近い場合は、プラグイン / ユーザー定義ワークフロー活動をユーザー定義アセンブリに移動することを検討してください。
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
# <a name="optimize-assembly-development"></a>アセンブリ開発を最適化する

**カテゴリ**: パフォーマンス、保守性、設計

**影響の可能性**: 低い

<a name='symptoms'></a>

## <a name="symptoms"></a>現象

カスタム アセンブリの開発時には、考慮すべき事項がいくつかあります:

1. 異なる複数のカスタム アセンブリ
    - 保守性の複雑さの増大
    - プラグイン実行期間の増大の可能性

2. サンドボックスのアセンブリ サイズ制約は、Common Data Service では 16 MBです。

<a name='guidance'></a>

## <a name="guidance"></a>ガイダンス

> [!NOTE]
> より詳細なガイダンス説明は、アセンブリ開発の最適化の詳細に関する開発 (個別のプラグインを単一のカスタム アセンブリに統合する方法、アセンブリ サイズを最小限に抑える推奨など) を参照してください。

### <a name="consolidate-plug-ins-or-custom-workflow-activities-into-a-single-assembly"></a>プラグインまたはユーザー定義ワークフロー活動を単一のアセンブリに統合します。

Common Data Service ソリューション用に開発されたプラグインおよびユーザー定義ワークフロー活動は、単一の Visual Studio プロジェクト内にまとめて存在させる必要があります。 プラグインが次の例外に当てはまらない限り、個別のプラグインおよびユーザー定義ワークフロー活動を単一の Visual Studio プロジェクトまたはアセンブリに統合することを考量してください。

1. プラグイン / ユーザー定義のワークフロー活動は、選択的に 1 つの環境に展開する必要があります。

2. Common Data Service インスタンスの場合、物理アセンブリ サイズは 16 MB に近いサイズまたはそれ以上です。


### <a name="move-plug-inscustom-workflow-activities-into-multiple-assemblies"></a>プラグイン / ユーザー定義ワークフロー活動を複数のアセンブリに移動する

PowerApps および Dynamics 365 (online) には 16 MB のアセンブリ サイズ制限があり、これは変更できません。 アセンブリ サイズが 16 MB に近づいたら、プラグイン/ユーザー定義ワークフロー活動を複数のアセンブリに移動することを検討します。

<a name='problem'></a>

## <a name="problematic-patterns"></a>問題となるパターン

### <a name="multiple-assemblies"></a>複数のアセンブリ
複数の領域に影響を与える可能性のあるアセンブリが複数ある:

1. パフォーマンス - 各アセンブリには、Common Data Service によって統合されるライフサイクルがあります。  これにはアセンブリの読み込み、キャッシュ、アンロードが含まれます。  複数のアセンブリが原因でサーバー上で多くの作業 (アセンブリの読み込みやキャッシュ) が実行されており、プラグイン/ユーザー定義ワークフロー活動の全体の実行時間に影響を与える可能性がある。

2. 保守性 - 複数のプラグイン/ユーザー定義ワークフロー活動があると、Visual Studio プロジェクトのアプリケーション ライフサイクル管理 (ALM) が複雑化する原因となります。 これにより、特定のプラグイン/ユーザー定義ワークフロー活動のプロジェクトを更新またはパッチする場合、プラグイン/ユーザー定義ワークフロー活動をソリューション内にパッケージする場合、プラグイン/ユーザー定義ワークフロー活動を展開内で管理する場合のリスクと作業時間が増大します。

### <a name="assembly-larger-than-16-mb"></a>16 MB より大きいアセンブリ
16 MB より大きいユーザー定義アセンブリは、Common Data Service 内に登録できません。

<a name='additional'></a>

## <a name="additional-information"></a>追加情報

多くの場合、開発者はプラグイン/ユーザー定義ワークフロー活動ごとに新しい Visual Studio プロジェクトを作成します。  つまり、プラグイン/ユーザー定義ワークフロー活動ごとに個別のアセンブリが生成されることになります。

<a name='seealso'></a>

### <a name="see-also"></a>関連項目

[イベント フレームワーク](../../event-framework.md)<br />
[ビジネス プロセスを拡張するためのプラグインの使用](../../plug-ins.md)<br />
