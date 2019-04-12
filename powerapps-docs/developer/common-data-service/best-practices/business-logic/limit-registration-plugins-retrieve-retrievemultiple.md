---
title: retrieve および RetrieveMultiple メッセージ用のプラグインの登録を制限する | MicrosoftDocs
description: 同期プラグイン ロジックを Retrieve および RetrieveMultiple メッセージ イベントに追加すると速度低下が発生する可能性があります。
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
# <a name="limit-the-registration-of-plug-ins-for-retrieve-and-retrievemultiple-messages"></a>retrieve および RetrieveMultiple メッセージ用のプラグインの登録を制限する

**カテゴリ**: パフォーマンス

**影響の可能性**: 中程度

<a name='symptoms'></a>

## <a name="symptoms"></a>現象

同期プラグイン ロジックを Retrieve および RetrieveMultiple メッセージ イベントに追加すると以下の現象が発生する可能性があります。

- モデル駆動アプリが応答しない
- クライアント対話が遅くなる
- ブラウザーが応答を停止する

<a name='guidance'></a>

## <a name="guidance"></a>ガイダンス

Retrieve メッセージおよび RetrieveMultiple メッセージに登録されているプラグインを含むソリューションの設計を評価します。  一般に、これらのメッセージにプラグインを登録することはお勧めできません。その理由は、さまざまなエントリ ポイントからエンティティ レコードを返す要求の速度低下に関連するリスクがあるためです。  ただし、アプリケーションの設計には適している場合があります。 一般的なアプリケーションの例として、特定の既存クエリへの追加のフィルター条件の挿入が挙げられます。 これにより、ビューのユーザー インターフェイスでできないことをソリューションで補正できます。  ビュー デザイナーでサポートできるのは複雑性レベルの特定の階層のみで、結果やクエリを設定するにはそのほかのオプションを採用する必要があります。

適切なソリューションの場合は、次のヒントに従って環境への影響を最小限に抑えてください:

- プラグイン コードに条件を追加して、対象ロジックを実行する必要があるかどうかをすばやく確認します。 不要な場合はすぐに戻り、呼び出し側にデータを返すことを遅らせる不要な手順は実行しません。

- 時間のかかるタスクは避けます。特に、外部サービスの呼び出しや Dynamics 365 への複雑なクエリといった、非確定的なタスクです。

- Common Data Service の追加データのクエリは制限または回避します。

### <a name="virtual-entities"></a>仮想エンティティ

外部ソースからデータを取得するための最も一般的な Retrieve および RetrieveMultiple はプラグイン内で呼び出されます。 外部ソースのデータは PowerApps 内で表示されるか、既存のデータを処理 / 操作するために使用されます。 バージョン 9.0 の Dynamics 365 (online) には、[仮想エンティティ](/dynamics365/customer-engagement/developer/virtual-entities/get-started-ve) と呼ばれる機能が導入されました。この機能により、外部システムに常駐しているデータをシームレスに統合し、そのデータを PowerApps 内のエンティティとして表示することができ、データのレプリケーションやカスタム コーディングは不要です。 機能、制限、構成の詳細については、[仮想エンティティ](/dynamics365/customer-engagement/developer/virtual-entities/get-started-ve) のドキュメントを参照してください。

### <a name="retrieve-caution"></a>取得に関する注意

Common Data Service は、エンティティ フォームを読み込むごとに少なくとも 2 つの Retrieve メッセージをトリガーします。  1 つの取得に含まれる属性は限られています。これらの属性はエンティティによって変わり、後続の呼び出しにより多くの属性が含まれます。  フォームの読み込み時に 1 つのアクションが発生することを期待している場合は、Retrieve メッセージのトリガーに厳密に依存しません。

<a name='additional'></a>

## <a name="additional-information"></a>追加情報

`Retrieve` メッセージと `RetrieveMultiple` メッセージは、最も頻繁に処理される 2 つのメッセージです。 `Retrieve` メッセージは、エンティティ フォームが開くとき、または 1 つのサービス エンドポイントで `Retrieve` 操作を使用してエンティティがアクセスされるときにトリガーされます。 `RetrieveMultiple` は、アプリケーションやサービス ポイントでのさまざまなアクションによりトリガーされます。たとえば、ユーザー インターフェイスのグリッドに値が入力される場合などです。  同期プラグイン ロジックをこれらのメッセージ イベントに追加すると速度低下が発生する可能性があります。

<a name='seealso'></a>

### <a name="see-also"></a>関連項目

[パフォーマンス最適化、Microsoft Dynamics CRM Online](https://mbs.microsoft.com/customersource/northamerica/CRM/learning/documentation/user-guides/PerformanceOptimizationsCRMOnlineSuccess)<br />
[外部データ ソースからのデータを格納する仮想エンティティの作成および編集](/powerapps/maker/common-data-service/create-edit-virtual-entities)<br />
