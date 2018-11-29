---
title: エンティティ メタデータ | Microsoft Docs
description: アプリ用 Common Data Service で使用するエンティティ メタデータについて。
services: ''
suite: powerapps
documentationcenter: na
author: mayadumesh
manager: kvivek
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/31/2018
ms.author: jdaly
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
<!-- 
Was Mike Carter
This topic was not migrated it was written for PowerApps 

Overlap with content in https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/introduction-entities

-->
# <a name="entity-metadata"></a>エンティティ メタデータ

各エンティティは、構造化データを保存する機能を提供します。 エンティティは、開発者向けに、アプリ用の Common Data Service を操作する際に使用するクラスに対応しています。

## <a name="entity-names"></a>エンティティ名
各エンティティには、作成時に一意の名前が定義されています。 この名前は、次のいくつかの方法で表示されます。

|名前プロパティ |説明|
|---------|---------|
|`SchemaName`|通常は、論理名の Pascal 形式バージョンです 例 Account|
|`CollectionSchemaName`|スキーマ名の複数形。 例 Accounts|
|`LogicalName`|小文字のスキーマ名のすべてのバージョン。 例 account|
|`LogicalCollectionName`|小文字のコレクション スキーマ名のすべてのバージョン。 例 accounts|
|`EntitySetName`|Web API を使用してコレクションを識別するために使用されます。 既定では、論理コレクション名と同じです。<br />メタデータをプログラムによって更新することによって、エンティティ セット名を変更することが可能です。 しかし、エンティティ用の Web API コードが作成される前に行う必要があります。 詳細: [Web API のタイプおよび操作 > エンティティ セットの名前の変更](/dynamics365/customer-engagement/developer/webapi/web-api-types-operations#change-the-name-of-an-entity-set)。|

> [!NOTE]
> ユーザー定義エンティティを作成すると、選択した名前の前に、エンティティが作成されたソリューションに関連付けられているソリューション発行者のカスタマイズ プレフィックス値が付加されます。 エンティティ セット名以外は、エンティティが作成された後で名前を変更することはできません。 ソリューション内でメタデータ アイテムの一貫した名前を使用する場合は、使用するカスタマイズの接頭辞を含むソリューション発行者に関連付けて作成する、ソリューションのコンテキストで作成する必要があります。 詳細: [ソリューション発行者およびソリューションを作成する](introduction-solutions.md#create-a-solution-publisher-and-solution)

各エンティティには、ローカライズされた値を表示できる 3 つのプロパティがあります。


|Name  |説明  |
|---------|---------|
|`DisplayName`|通常、スキーマ名と同じですが、スペースを含めることができます。 例 Account|
|`DisplayCollectionName`|表示名の複数形。 例 Accounts|
|`Description`|エンティティを表す短い文、つまり、*顧客または見込み顧客を表す部署です。この会社には、業務取引で請求が行われます。*|

これらは、アプリ内のエンティティを参照するために使用されるローカライズ可能な値です。 これらの値は、いつでも変更できます。 ローカライズされた値を追加または編集するには、[アプリ用 CDS カスタマイズ ガイド: カスタマイズされたエンティティおよびフィールド テキストを他の言語に翻訳する](/dynamics365/customer-engagement/customize/export-customized-entity-field-text-translation)を参照してください。


## <a name="primary-key"></a>主キー

`PrimaryIdAttribute` プロパティ値は、エンティティの主キーである属性の論理名です。

既定では、すべてのエンティティに GUID 一意識別子属性が 1 つあります。 これは通常、*&lt; エンティティ論理名 &gt;*+ `Id` という名前です。

## <a name="primary-name"></a>プライマリ名

`PrimaryNameAttribute` プロパティ値は、エンティティ レコードを識別する文字列値を保存する属性の論理名です。 これは、UI でレコードを開くためのリンクに表示される値です。

**例**: 取引先担当者エンティティは、`fullname` 属性をプライマリ名属性として使用します。

> [!NOTE]
> すべてのエンティティがプライマリ名を持つわけではありません。 一部のエンティティは UI に表示されることを意図していません。

## <a name="entity-images"></a>エンティティ イメージ

`PrimaryImageAttribute` プロパティ値は、エンティティ レコードのイメージ データを保存する属性の論理名です。 各エンティティは 1 つのイメージ属性のみを持つことができ、その属性の論理名は常に `entityimage` です。

**例**: [取引先担当者エンティティ](reference/entities/contact.md) [EntityImage](reference/entities/contact.md#BKMK_EntityImage) 属性には取引先担当者の画像を保存できます。

パフォーマンス上の理由から、明示的に要求されない限り、エンティティ イメージは検索操作に含まれません。

エンティティ イメージをサポートする各エンティティには、3 つのサポート属性があります。

|SchemaName|型|説明|
|--|--|--|
|`EntityImage_Timestamp` |`BigIntType`|値は、イメージが最後に更新されときに表され、イメージの最新版がクライアントでダウンロードされ、キャッシュされることが確実にできるように使用されます。|
|`EntityImage_URL`|`StringType`|クライアントでエンティティ イメージを表示する絶対 URL。|
|`EntityImageId`|`UniqueIdentifierType`|イメージの一意の識別子|

詳細: 
- [アプリ用 Common Data Service 開発者ガイドイメージ属性](/dynamics365/customer-engagement/developer/image-attributes)
- [アプリ用 Common Data Service のデベロッパーガイド サンプル: エンティティ イメージの設定と取得](/dynamics365/customer-engagement/developer/sample-set-retrieve-entity-images)

> [!NOTE]
> これは、モデル駆動型アプリのエンティティ用に表示されるアイコンとは異なります。 `IconVectorName` プロパティには、これを設定する SVG Web リソースの名前が含まれます。

## <a name="types-of-entities"></a>エンティティの種類

エンティティの機能と動作は、いくつかのエンティティのプロパティに依存します。 これらのプロパティのほとんどは比較的単純で、わかりやすい名前が付いています。 以下の 4 つは追加の説明が必要です。*企業形態*、*活動エンティティ*、*Activityparty エンティティ*および*子エンティティ*。

### <a name="entity-ownership"></a>エンティティの所有権

エンティティは、それらのデータがどのように所有されているかによって分類できます。 これは、セキュリティがエンティティにどのように適用されるかに関する重要な概念です。 この情報は `OwnershipType` プロパティにあります。 次の表で、さまざまな企業形態タイプを示しています。

|所有権の種類  |説明  |
|---------|---------|
|業務|データは部署に属します。 データへのアクセスは、部署レベルで管理できます。|
|なし|データは別のエンティティによって所有されません。|
|組織|データは、組織に属します。 データへのアクセスは組織レベルで管理されます。|
|[ユーザーまたはチーム]|データは、ユーザーまたはチームに属します。 これらのレコードで実行できる操作は、ユーザー レベルで管理できます。|

新しいエンティティを作成する場合、唯一の所有権オプションは**組織**または**ユーザーまたはチーム**です。 このオプションを選択すると、そのオプションを変更することはできません。 レコードの操作を表示または実行できるユーザーを最も詳細に制御するには、**ユーザーまたはチーム**を選択します 。 このレベルの制御が不要な場合は、**組織**を選択します。 

### <a name="activity-entities"></a>活動エンティティ

活動は、ユーザによって実行される、または実行されるタスクです。 活動は、カレンダーにエントリを作成できる任意のアクションです。 

活動は、ビジネス データを保存する他の種類のエンティティとは異なるモデル化をされています。 活動に関するデータは頻繁に一覧にまとめて表示されますが、活動の種類ごとに固有のプロパティが必要です。 すべての可能なプロパティの単一活動エンティティを持つのではなく、別々の種類の活動 エンティティがあり、それぞれが基本の [ActivityPointer エンティティ](reference/entities/activitypointer.md)からプロパティを継承します。 これらのエンティティは `IsActivity` プロパティを true に設定します。


|エンティティ |説明  |
|---------|---------|
|[予定](reference/entities/appointment.md)|開始時刻、終了時刻、および期間により時間間隔を定めた約束です。|
|[電子メール](reference/entities/email.md)|電子メール プロトコルを使用して配信される活動です。|
|[FAX](reference/entities/fax.md)|FAX の通信結果やページ数を追跡する活動です。ドキュメントの電子コピーを保存することもできます。|
|[レター](reference/entities/letter.md)|レターの配送を追跡する活動です。 この活動にはレターの電子コピーを使用できます。|
|[PhoneCall](reference/entities/phonecall.md)|通話を追跡する活動です。|
|[RecurringAppointmentMaster](reference/entities/recurringappointmentmaster.md)|定期的な予定の系列のマスター予定です。|
|[ソーシャル活動](reference/entities/socialactivity.md)|内部のみで使用|
|[タスク](reference/entities/task.md)|処理する必要がある作業を表す全般的な活動です。|

これらの種類の活動エンティティ レコードの 1 つを作成するときはいつも、対応する `ActivityPointer` エンティティ レコードが同じ `ActivityId` 一意識別子属性値で作成されます。 `ActivityPointer` エンティティのインスタンスを作成、更新、または削除することはできませんが、取得することはできます。 これは、すべてのタイプのアクティビティをリストにまとめて表示できるようにするものです。

同じように動作するユーザー定義活動エンティティを作成できます。
<!-- TODO: Add link to topic about creating an activity entity -->

### <a name="activityparty-entity"></a>ActivityParty エンティティ

このエンティティは、他のエンティティへの参照を含む活動エンティティの `PartyListType` 属性に構造を追加するために使用されます。 `Email.to` や `PhoneCall.from` などの活動エンティティ属性の値を設定するときは、このエンティティを使用します。 [ActivityParty エンティティ](reference/entities/activityparty.md)内では、参照が再生されている役割を定義するために [ParticipationTypeMask](reference/entities/activityparty.md#BKMK_ParticipationTypeMask) 属性を設定します。 ロールには、`Sender`、`ToRecipient`、`Organizer` などがあります。

`ActivityParty` エンティティを照会することはできますが、関連する活動外の活動関係者を作成、取得、更新、または削除することはできません。
詳細: 
- [ActivityParty エンティティ](/dynamics365/customer-engagement/developer/activityparty-entity).


### <a name="child-entities"></a>子エンティティ

`IsChildEntity` プロパティが true のエンティティには、特権が定義されることはなく、ユーザーまたはチームが所有することは決してありません。 子エンティティで実行できる操作は、多対 1 の関係から関連するエンティティにバインドされます。 ユーザーは、関連エンティティで同じ操作を実行できる場合にのみ、子エンティティに対する操作を実行できます。 子エンティティは、依存するエンティティ レコードが削除されると自動的に削除されます。

たとえば、`Post` エンティティの各子エンティティには、`PostComment`、`PostLike`、および `PostRole` があります。

## <a name="entity-keys"></a>エンティティ キー

各代替キー定義は、エンティティ インスタンスを一意に識別する 1 つ以上の属性を組み合わせて記述します。 代替キーは、通常、外部システムとの統合にのみ適用されます。 代替キーを定義して、レコードを一意に識別することができます。 これは、GUID 固有の識別子キーをサポートしていないシステムとデータを統合する場合に便利です。 エンティティを一意に識別するために、単一のフィールド値またはフィールド値の組み合わせを定義できます。 代替キーを追加すると、これらの属性に一意性制約が適用されます。 同じ値を持つ別のエンティティ レコードを作成または更新することはできません。

詳細: 
 - [アプリ用 Common Data Service カスタマイズ ガイド: アプリ用 CDS レコードで参照する代替キーを定義](/dynamics365/customer-engagement/customize/define-alternate-keys-reference-records)
 - [エンティティの代替キーの定義および開発者ガイド: アプリ用 CDS データを外部システムと同期する](/dynamics365/customer-engagement/developer/synchronize-dynamics-365-data-with-external-systems)

## <a name="entity-states"></a>エンティティの状態

大部分のエンティティには、レコードの状態を追跡するための 2 つのプロパティがあります。 モデル駆動型アプリの**ステータス**である `StateCode` と、モデル駆動型アプリの**ステータス**である `StatusCode` があります。 

両方の属性には、有効な値を表示する一連のオプションが含まれています。 `StateCode` および `StatusCode` 属性値は、特定の `StatusCode` オプションが特定の `StateCode` に対して有効になるようにリンクされています。

これはエンティティによって異なりますが、多くのエンティティの共通パターンです。ユーザー定義エンティティの既定は次のとおりです。

|StateCode オプション  |StatusCode オプション  |
|---------|---------|
|0 : アクティブ|1 : アクティブ|
|1 : 非アクティブ|2 : 非アクティブ|

いくつかのエンティティには異なるオプションのセットがあります。 

**例**: `PhoneCall` エンティティ `StateCode` および `StatusCode` オプション


|`StateCode`|`StatusCode`|
|---------|---------|
|0 : 開く|1 : 開く|
|1 : 完了|2 : 実行 <br />4 : 受信|
|2: キャンセル済み|3: キャンセル済み|

エンティティの有効な状態コードのセットはカスタマイズできませんが、状態コードはカスタマイズ可能です。 対応する `StateCode` に `StatusCode` オプションを追加できます。

ユーザー定義エンティティでは、ステータス間の有効な遷移に関する追加条件を定義できます。 詳細: 
- [エンティティ属性メタデータのカスタマイズ](/dynamics365/customer-engagement/developer/customize-entity-attribute-metadata)
- [カスタムの状態モデルの遷移の定義](/dynamics365/customer-engagement/developer/define-custom-state-model-transitions)。

### <a name="see-also"></a>関連項目

[アプリ用 Common Data Service のエンティティ](entities.md)
