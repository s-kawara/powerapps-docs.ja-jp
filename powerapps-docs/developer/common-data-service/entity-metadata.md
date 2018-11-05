---
title: エンティティ メタデータ | Microsoft Docs
description: Common Data Service for Apps でのエンティティ メタデータの使用について説明します。
services: ''
suite: powerapps
documentationcenter: na
author: JimDaly
manager: faisalmo
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/19/2018
ms.author: jdaly
search.audienceType:
- developer
search.app:
- PowerApps
- D365CE
ms.openlocfilehash: 60fafa90df656bb6d135a8cf7e2c2f3b4f8457da
ms.sourcegitcommit: 429b83aaa5a91d5868e1fbc169bed1bac0c709ea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/24/2018
ms.locfileid: "42840748"
---
# <a name="entity-metadata"></a>エンティティ メタデータ

各エンティティには、構造化されたデータを格納する機能があります。 開発者の場合、エンティティとは Common Data Service for Apps でデータを操作するときに使用するクラスに相当します。

## <a name="entity-names"></a>エンティティ名
各エンティティには、作成時に一意の名前が定義されます。 この名前は、いくつかの方法で表現されます。

|Name プロパティ |説明|
|---------|---------|
|`SchemaName`|通常、論理名をパスカル ケースで表します。 例: Account|
|`CollectionSchemaName`|スキーマ名の複数形です。 例: Accounts|
|`LogicalName`|スキーマ名をすべて小文字で表します。 例: account|
|`LogicalCollectionName`|コレクション スキーマ名をすべて小文字で表します。 例: accounts|
|`EntitySetName`|Web API でコレクションを識別するために使用します。 既定では、論理コレクション名と同じです。<br />プログラムによってメタデータを更新することにより、エンティティ セット名を変更することができます。 ただし、この変更は、エンティティの Web API コードを記述する前に完了しておく必要があります。 詳細情報: [Dynamics 365 Customer Engagement の開発者ガイド: Web API の種類および操作 > エンティティ セット名の変更](/dynamics365/customer-engagement/developer/webapi/web-api-types-operations#change-the-name-of-an-entity-set)|

> [!NOTE]
> カスタム エンティティを作成する場合、選択した名前の先頭には、エンティティが作成されたソリューションに関連付けられたソリューション発行者のカスタマイズ接頭辞が付加されます。 エンティティの作成後は、エンティティ セットの名前以外に、エンティティの名前を変更することはできません。 ソリューション内のメタデータ アイテムの名前に一貫性を持たせたい場合は、目的のカスタマイズ接頭辞を含むソリューション発行者に関連付けて作成したソリューションのコンテキストでそれらを作成する必要があります。 詳細情報: [ソリューション発行者とソリューションを作成する](introduction-solutions.md#create-a-solution-publisher-and-solution)

また、各エンティティには、ローカライズされた値を表示できる 3 つのプロパティがあります。


|名前  |説明  |
|---------|---------|
|`DisplayName`|通常、スキーマ名と同じですが、スペースを含めることができます。 例: Account|
|`DisplayCollectionName`|表示名の複数形です。 例: Accounts|
|`Description`|エンティティを説明する短い文です。例: *Business that represents a customer or potential customer. The company that is billed in business transactions. (顧客または潜在顧客を表す Business。ビジネス トランザクションにおける請求先の会社。)*|

アプリ内のエンティティを参照するために使用するローカライズ可能な値です。 これらの値は、いつでも変更できます。 ローカライズされた値を追加または編集するには、「[Dynamics 365 Customer Engagement のカスタマイズ ガイド: カスタマイズされたエンティティおよびフィールド テキストを他の言語に翻訳する](/dynamics365/customer-engagement/customize/export-customized-entity-field-text-translation)」を参照してください。


## <a name="primary-key"></a>主キー

`PrimaryIdAttribute` プロパティの値は、エンティティの主キーである属性の論理名となります。

既定では、すべてのエンティティが単一の GUID 一意識別子属性を持っています。 これは、通常、"*&lt;エンティティの論理名&gt;*+ `Id`" と呼ばれます。

## <a name="primary-name"></a>プライマリ名

`PrimaryNameAttribute` プロパティの値は、エンティティ レコードを識別する文字列値が格納される属性の論理名となります。 これは、UI でレコードを開くためのリンクに表示される値です。

**例**: Contact エンティティでは、`fullname` 属性がプライマリ名の属性として使用されます。

> [!NOTE]
> すべてのエンティティに、プライマリ名があるわけではありません。 一部のエンティティは、UI に表示することを目的としていません。

## <a name="entity-images"></a>エンティティのイメージ

`PrimaryImageAttribute` プロパティの値は、エンティティ レコードのイメージ データが格納される属性の論理名となります。 各エンティティはイメージ属性を 1 つだけ持つことができ、その属性の論理名は常に `entityimage` となります。

**例**: [Contact Entity](reference/entities/contact.md) [EntityImage](reference/entities/contact.md#BKMK_EntityImage) 属性には、連絡先の画像を格納できます。

パフォーマンス上の理由から、エンティティ イメージは、明示的に要求されない限り、取得操作に含められません。

エンティティ イメージをサポートする各エンティティでは、3 つの関連属性が使用されます。

|スキーマ名|種類|説明|
|--|--|--|
|`EntityImage_Timestamp` |`BigIntType`|値はイメージが最後に更新された日時を示します。イメージの最新バージョンがダウンロードされ、クライアント上にキャッシュされていることを確認するのに役立ちます。|
|`EntityImage_URL`|`StringType`|クライアントでエンティティ イメージを表示する絶対 URL です。|
|`EntityImageId`|`UniqueIdentifierType`|イメージの一意の識別子です。|

詳細情報: 
- [Dynamics 365 Customer Engagement の開発者ガイド: イメージの属性](/dynamics365/customer-engagement/developer/image-attributes)
- [Dynamics 365 Customer Engagement の開発者ガイド: サンプル: エンティティ イメージを設定および取得する](/dynamics365/customer-engagement/developer/sample-set-retrieve-entity-images)

> [!NOTE]
> これは、モデル駆動型アプリでエンティティとして表示されるアイコンとは異なります。 `IconVectorName` プロパティには、これを設定する SVG Web リソースの名前が含まれます。

## <a name="types-of-entities"></a>エンティティの種類

エンティティの機能と動作は、エンティティのいくつかのプロパティに依存します。 これらのプロパティのほとんどは比較的に簡単であり、わかりやすい名前が付けられています。 *所有権*、*活動エンティティ*、*Activityparty エンティティ*、および*子エンティティ*の 4 つについては、追加の説明が必要です。

### <a name="entity-ownership"></a>エンティティの所有権

エンティティは、エンティティに含まれるデータの所有形態によって分類できます。 これは、エンティティへのセキュリティの適用方法に関連する重要な概念です。 この情報は、`OwnershipType` プロパティに含まれています。 次の表では、さまざまな所有権の種類について説明します。

|所有権の種類  |説明  |
|---------|---------|
|Business|Business ユニットに属するデータです。 データへのアクセスは、Business ユニット レベルで制御できます。|
|なし|データは別のエンティティによって所有されていません。|
|組織|データは組織に属しています。 データへのアクセスは、組織レベルで制御されます。|
|ユーザーまたはチーム|データはユーザーまたはチームに属しています。 これらのレコードに対して実行できるアクションは、ユーザー レベルで制御できます。|

新しいエンティティを作成する場合に選択できる所有権は、**組織**か、**ユーザーまたはチーム**に限られます。 このオプションを選択すると、それ以降に変更することはできません。 レコードに対するアクションを表示または実行できるユーザーを最も細かく制御するには、**ユーザーまたはチーム**を選択します。 このレベルの制御が必要ない場合は、**組織**を選択します。 

### <a name="activity-entities"></a>活動エンティティ

活動は、ユーザーが実行する、または実行すべきタスクです。 活動は、カレンダーでエントリの作成対象とすることができる任意のアクションです。 

活動は、ビジネス データを格納する他の種類のエンティティとは異なる方法でモデル化されます。 活動に関するデータはたびたびリスト内に一緒に表示されますが、各種の活動にはそれぞれの固有のプロパティが必要です。 可能なプロパティをすべて持つ単一の活動エンティティ以外に、異なる種類の活動エンティティがあります。それらのエンティティはそれぞれ、基本となる [ActivityPointer エンティティ](reference/entities/activitypointer.md)からプロパティを継承します。 これらのエンティティでは、`IsActivity` プロパティが true に設定されます。


|組織 |説明  |
|---------|---------|
|[Appointment](reference/entities/appointment.md)|開始/終了時刻と期間で時間間隔を表す約束です。|
|[Email](reference/entities/email.md)|電子メール プロトコルを使用して配信される活動です。|
|[Fax](reference/entities/fax.md)|通話結果および FAX のページ数を追跡し、必要に応じてドキュメントの電子コピーを格納する活動です。|
|[Letter](reference/entities/letter.md)|レターの配送を追跡する活動です。 活動には、レターの電子コピーを含めることができます。|
|[PhoneCall](reference/entities/phonecall.md)|電話通話を追跡する活動です。|
|[RecurringAppointmentMaster](reference/entities/recurringappointmentmaster.md)|定期的な予定の系列のマスターの予定です。|
|[SocialActivity](reference/entities/socialactivity.md)|内部使用専用。|
|[Task](reference/entities/task.md)|処理する必要がある作業を表す全般的な活動です。|

このような種類の活動エンティティ レコードのいずれかを誰かが作成するたびに、対応する `ActivityPointer` エンティティ レコードが、同じ `ActivityId` 一意識別子属性の値を使用して作成されます。 `ActivityPointer` エンティティのインスタンスを作成、更新、または削除することはできませんが、取得することはできます。 この場合は、すべての種類の活動をリスト内に一緒に含めることができます。

同様に動作するカスタム活動エンティティを作成することができます。
<!-- TODO: Add link to topic about creating an activity entity -->

### <a name="activityparty-entity"></a>ActivityParty エンティティ

このエンティティは、他のエンティティへの参照が含まれている活動エンティティ `PartyListType` の属性に構造体を追加するために使用されます。 このエンティティは、`Email.to` や `PhoneCall.from` などの活動エンティティの属性の値を設定する場合に使用します。 [ActivityParty エンティティ](reference/entities/activityparty.md) 内では、[ParticipationTypeMask](reference/entities/activityparty.md#BKMK_ParticipationTypeMask) 属性を設定することで、参照によって実行されるロールを定義します。 ロールには、`Sender`、`ToRecipient`、`Organizer` などが含まれます。

`ActivityParty` エンティティに対してクエリを実行することはできますが、それが関連付けられた活動以外で活動関係者を作成、取得、更新、または削除することはできません。
詳細情報: 
- [Dynamics 365 Customer Engagement の開発者ガイド: ActivityParty エンティティ](/dynamics365/customer-engagement/developer/activityparty-entity)


### <a name="child-entities"></a>子エンティティ

`IsChildEntity` プロパティが true になっているエンティティの場合、いかなる権限も定義されず、所有形態はユーザーまたはチームになりません。 子エンティティで実行できる操作は、多対一のリレーションシップを介して関連付けられているエンティティにバインドされます。 ユーザーが子エンティティに対する操作を実行できるのは、関連するエンティティに対しても同じ操作を実行できる場合に限られます。 子エンティティは、依存しているエンティティ レコードが削除されると、自動的に削除されます。

たとえば、`PostComment`、`PostLike`、`PostRole` はそれぞれ `Post` エンティティの子となります。

## <a name="entity-keys"></a>エンティティのキー

各代替キーの定義では、エンティティのインスタンスを一意に識別する 1 つまたは複数の属性が組み合わせて記述されます。 代替キーは、通常、外部システムと統合する場合にのみ適用されます。 代替キーを定義することで、レコードを一意に識別できます。 これは、GUID 一意識別子キーがサポートされていないシステムとデータを統合する場合に役立ちます。 単一のフィールド値またはフィールド値の組み合わせを定義して、エンティティを一意に識別することができます。 代替キーを追加すると、これらの属性に一意性制約が適用されます。 別のエンティティ レコードを作成または更新し、同じ値を持たせることはできません。

詳細情報: 
 - [Dynamics 365 Customer Engagement のカスタマイズ ガイド: Dynamics 365 レコードを参照する代替キーの定義](/dynamics365/customer-engagement/customize/define-alternate-keys-reference-records)
 - [Dynamics 365 Customer Engagement の開発者ガイド: Dynamics 365 データを外部システムと同期する](/dynamics365/customer-engagement/developer/synchronize-dynamics-365-data-with-external-systems)

## <a name="entity-states"></a>エンティティの状態

ほとんどのエンティティには、レコードの状態を追跡するために 2 つのプロパティがあります。 `StateCode` (モデル駆動型アプリでは **Status** と呼ばれる) と、`StatusCode` (モデル駆動型アプリでは **Status Reason** と呼ばれる) の 2 つです。 

両方の属性に、有効な値を表示するオプション セットが含まれます。 `StateCode` 属性値と `StatusCode` 属性値は、指定された `StateCode` に対して特定の `StatusCode` オプションのみが有効になるようにリンクされます。

これはエンティティによって異なる場合がありますが、多くのエンティティが共通のパターンを持っています。カスタム エンティティの既定値は次のようになります。

|StateCode オプション  |StatusCode オプション  |
|---------|---------|
|0: アクティブ|1: アクティブ|
|1: 非アクティブ|2: 非アクティブ|

一部のエンティティには、異なるオプション セットがあります。 

**例**: `PhoneCall` エンティティの `StateCode` オプションと `StatusCode` オプション


|`StateCode`|`StatusCode`|
|---------|---------|
|0 : オープン|1: オープン|
|1 : 完了|2: 実行 <br />4: 受信|
|2: 取り消し|3: 取り消し|

エンティティの一連の有効な状態コードはカスタマイズすることができませんが、ステータス コードはカスタマイズ可能です。 別の `StatusCode` オプションを、対応する `StateCode` に追加することができます。

カスタム エンティティの場合、ステータス間の遷移を有効にするために追加の条件を定義できます。 詳細情報: 
- [Dynamics 365 Customer Engagement の開発者ガイド: エンティティ属性メタデータのカスタマイズ](/dynamics365/customer-engagement/developer/customize-entity-attribute-metadata)
- [Dynamics 365 Customer Engagement の開発者ガイド: カスタムの状態モデルの遷移の定義](/dynamics365/customer-engagement/developer/define-custom-state-model-transitions)

### <a name="see-also"></a>関連項目

[Common Data Service for Apps のエンティティ](entities.md)
