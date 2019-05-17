---
title: ソリューション チェッカーの一般的な問題と解決策 | Microsoft Docs
description: ' ソリューション チェッカーにおける一般的な問題と解決策の一覧'
keywords: ''
ms.date: 02/11/2019
ms.service:
  - powerapps
ms.custom:
  - ''
ms.topic: article
ms.assetid: caa4e3f2-9700-49b8-87ed-8a68e8878b02
author: jowells1
ms.author: jowells
manager: austinj
ms.reviewer: null
robots: 'noindex,nofollow'
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="common-issues-and-resolutions-for-solution-checker"></a>ソリューション チェッカーの一般的な問題と解決策

この記事ではソリューション チェッカーの使用中に発生する可能性がある一般的な問題について説明します。 適用対象には回避策を示します。

## <a name="solution-checker-runs-fail-due-to-powerapps-checker-version-installed"></a>PowerApps チェッカーのバージョンがインストールされているため、ソリューション チェッカーの実行に失敗する
ソリューション チェッカーは PowerApps チェッカーのソリューションに含まれている機能です。  PowerApps チェッカーのバージョンが 1.0.0.47 より前の場合、ソリューションのチェッカーの実行が正常に完了しません。 PowerApps チェッカーのバージョンを [!INCLUDE [pn-dyn-365-admin-center](../../includes/pn-dyn-365-admin-center.md)] からアップグレードする必要があります。 

ただし、バージョンが 1.0.0.45 より前の PowerApps チェッカーがインストールされている場合は、ソリューションを削除して再インストールすることをお勧めします。 最近のスキーマの変更により、PowerApps チェッカーの 1.0.0.45 より前のバージョンからのアップグレードは失敗する可能性があります。

ソリューション チェッカーの過去の結果を保持したい場合は、前回の実行からの結果をエクスポートするか、または [データをExcel にエクスポート](../../user/export-data-excel.md) を使用してすべてのソリューション チェッカーのデータを以下のエンティティからエクスポートします:

- 分析コンポーネント
- 分析ジョブ
- 分析結果
- 分析結果の詳細

### <a name="delete-powerapps-checker"></a>PowerApps チェッカーの削除

PowerApps チェッカーのソリューションの削除:

1. システム管理者またはシステム カスタマイザーとして https://web.powerapps.com/environments に移動して PowerApps ポータルを開きます。
2. **ソリューション**を選択します。
3. **PowerApps チェッカー** を選択して、ソリューション ツールバーで **削除** を選択します。

### <a name="add-powerapps-checker"></a>PowerApps チェッカーの追加

PowerApps チェッカーを Common Data Service 環境に再追加:

1. システム管理者またはシステム カスタマイザーとして https://web.powerapps.com/environments に移動して PowerApps ポータルを開きます。
2. **ソリューション**を選択します。
3. ソリューション ツールバーで **ソリューション チェッカー** を選択し、次に **Install** を選択します。

## <a name="runs-on-large-solutions-fail"></a>大規模ソリューションでの実行で失敗

ソリューションが大きすぎる場合に起こりうるシナリオがいくつかあります。 これらのシナリオについて以下でさらに説明します。 各シナリオに対するソリューションは、分析対象のコンポーネントが少ない小規模のソリューションを作成することです。 ソリューションのファイル サイズが大きい原因がプラグイン アセンブリ コンポーネントである場合は、[ユーザー定義のアセンブリ開発を最適化する](../../developer/common-data-service/best-practices/business-logic/optimize-assembly-development.md) のガイダンスを参照してください。

ソリューション チェッカーはこれらのシナリオに基づいたソリューションのチェックに失敗する可能性があります:
- ソリューションのファイル サイズは 30MB に厳しく制限されます。  
- Common Data Service 環境からソリューションをエクスポートする場合の 10 分のタイムアウト。 既定のソリューションのような大規模なソリューションはこの時間内ではエクスポートされない可能性があり、その場合チェックが正常に完了しません。 ソリューション チェッカーは、ジョブの処理に失敗する前に 3 回試行するため、失敗通知を受け取るまでに 30 分以上かかる可能性があります。

これらの問題に対処するには、分析対象として小規模なソリューションを作成または確認します。 誤検知を最小限に抑えるために、確実に依存するカスタマイズを追加してください。 ソリューションを作成してこれらのコンポーネントを追加する場合は、以下を含めます:

- プラグインを追加するときは、プラグインの SDK メッセージ処理手順を含めます。
- エンティティ フォームを追加するときは、フォーム イベントに添付された JavaScript Web リソースを含めます。  
- JavaScript Webリソースを追加するときは、すべての依存する JavaScript Web リソースを含めます。
- HTML Webリソースを追加するときは、HTML Webリソース内に定義されている依存スクリプトをすべて含めます。
- カスタム ワークフローを追加するときは、ワークフロー内で使用されているアセンブリを含めます。

## <a name="solution-checker-run-or-download-results-dont-complete"></a>ソリューション チェッカーの実行またはダウンロードの結果が不完全 
ソリューション チェッカーを実行した直後に操作が完了せず、以下のメッセージが表示されます:<br />
"*ソリューション名* ソリューションでチェックを実行できませんでした。 再実行してください。" <br />
![実行できませんでした](media/solution-checker-werent-able-to-run.png)

この問題は組織が **管理モード** の状態にあり、ソリューション チェッカーが要求を実行しているユーザーの権限を検証できないために発生します。 この問題を解決するには管理モードを無効にします。 

### <a name="disable-administration-mode-for-an-instance"></a>インスタンスの管理モードを無効化
1. Dynamics 365 for Customer Engagement のインスタンス ピッカーにアクセスします: https://port.crm.dynamics.com/G/Instances/InstancePicker.aspx
2. ソリューション チェッカーの実行に問題があるインスタンスを選択してください。
3. **管理** を選択します。<br />
![インスタンスの管理](media/solution-checker-instance-admin.png)

4. **管理モードを有効にする** をクリアする。 <br />
![管理モードの無効化](media/solution-checker-instance-disable-admin-mode.png)

5. ソリューション チェッカーを再実行

## <a name="solution-checker-will-not-process-patched-solutions"></a>ソリューション チェッカーは修正プログラム適用済みのソリューションを処理しません

ソリューションに [修正プログラム](https://docs.microsoft.com/powerapps/developer/common-data-service/create-patches-simplify-solution-updates) が適用済の場合、ソリューション チェッカーは分析のためのソリューションをエクスポートできません。 ソリューションに修正プログラムが適用されていると、元のソリューションがロックされそのソリューションを親ソリューションとして識別する依存修正プログラムが組織内に存在する限り、変更またはエクスポートができません。

この問題に対処するには、ソリューションに関連するすべての修正プログラムが新しく作成されたソリューションに含まれるようにソリューションを複製します。 これによりソリューションのロックが解除され、ソリューションをシステムからエクスポートできます。 詳細: [ソリューションの複製](use-segmented-solutions-patches-simplify-updates.md#clone-a-solution)

## <a name="line-number-references-for-issues-in-html-resources-with-embedded-javascript-are-not-correct"></a>JavaScript が埋め込まれた HTML リソースで問題の行番号参照が不正 

HTML Web リソースがソリューション チェッカーで処理されるときに、HTML Web リソースは HTML Web リソース内の JavaScript とは別に処理されます。 このため、HTML Web リソースの `<script>` の中に見つかった不正な行番号は正しくありません。

## <a name="web-unsupported-syntax-issue-for-web-resources"></a>Web リソースにおける Web-unsupported-syntax 問題

ECMAScript 6 (2015) またはそれ以降のバージョンは、ソリューション チェッカーで現在サポートされていません。 ソリューション チェッカーが ECMAScript 6 または以降のバージョンを使用した JavaScript を分析すると、Web リソースの web-supported-syntax 問題が報告されます。  

## <a name="multiple-violations-reported-for-plug-ins-and-workflow-activities-based-on-call-scope"></a>呼び出しスコープに基づいてプラグインとワークフロー活動について報告された複数の違反

問題が呼び出し側コンテキストのみに関連するプラグインとワークフロー活動ルールの場合、ソリューション チェッカー ツールが IPlugin インターフェースの実装で分析を開始して、実装の範囲で問題を検出するために呼び出しグラフを切り替えます。  場合によっては、問題が検出されたのと同じ場所に多数の呼び出しパスが到達することがあります。  この問題は呼び出しスコープに関連しているため、ツールはそのスコープに基づいてレポートして、個別の場所ではなくより良い影響を把握できます。 そのため、複数の問題が解決すべき単一の場所を参照することがあります。

## <a name="see-also"></a>関連項目
[Common Data Service のベスト プラクティスとガイダンス](../../developer/common-data-service/best-practices/index.md)<br />
[モデル駆動型アプリのベスト プラクティスとガイダンス](../../developer/model-driven-apps/best-practices/index.md)<br />
