---
title: 属性メタデータ | Microsoft Docs
description: Common Data Service で使用する属性メタデータについて説明します。
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

<!-- This topic was not migrated it was written for PowerApps 
Was Mike Carter
Overlap with https://docs.microsoft.com/dynamics365/customer-engagement/developer/introduction-entity-attributes

-->
# <a name="attribute-metadata"></a>属性メタデータ

エンティティには、各レコードに含めることのできるデータを表す、一連の属性のコレクションが保存されます。 開発者は、属性のさまざまな種類、およびその使用方法について理解する必要があります。 

詳細: [エンティティ属性の概要](/dynamics365/customer-engagement/developer/introduction-entity-attributes)

## <a name="attribute-names"></a>属性名

エンティティと同様に、各属性は、作成時に定義された一意の名前を持ちます。 この名前は、次のいくつかの方法で表示されます。


|Name |説明  |
|---------|---------|
|`SchemaName`|通常は、論理名の Pascal 形式バージョンです 例 `AccountNumber`|
|`LogicalName`|すべて小文字の名前。 例 `accountnumber`|

カスタム属性を作成すると、選択した名前の前に、属性が作成されたソリューションに関連付けられているソリューション発行者のカスタマイズの接頭辞値が付加されます。

属性の作成後は名前を変更できません。

各属性には、ローカライズされた値を表示できる 2 つのプロパティがあります。 これらは、アプリ内の属性を参照するために使用される値です。

|Name |説明  |
|---------|---------|
|`DisplayName`|通常、スキーマ名と同じですが、スペースを含めることができます。 例 **取引先企業番号**|
|`Description`|属性の説明、またはユーザーにガイダンスを提供する短い文章。 例 *システム ビューで取引先企業をすばやく検索して識別できるようにするための取引先企業の ID 番号またはコードを入力します。*<br />モデル駆動型アプリでは、この情報は、ユーザーがこの属性のフィールドをフォーム上に置いたときに表示されます。|


これらは、アプリ内の属性を参照するために使用されるローカライズ可能な値です。 これらの値は、いつでも変更できます。 ローカライズされた値を追加または編集するには、[Common Data Service カスタマイズ ガイド: カスタマイズされたエンティティおよびフィールド テキストを他の言語に翻訳する](/dynamics365/customer-engagement/customize/export-customized-entity-field-text-translation) を参照してください。

## <a name="attribute-types"></a>属性の種類

`AttributeTypeName` プロパティは、属性のタイプを記述します このプロパティには、存在するさまざまな種類の属性ごとにラベルを提供する `AttributeTypeDisplayName` 型の値が含まれます。 

> [!NOTE]
> `AttributeType` プロパティと混同しないでください。 この古いプロパティの値は、ほとんどが `AttributeTypeName` と対応しており、`ImageType` 属性は `Virtual` として表示されます。 `AttributeType` プロパティではなく、`AttributeTypeName` プロパティを参照してください。

次の表を参照してください。

- これらのタイプは、比較のためにカテゴリ別にグループ化されています。
- 各 `AttributeTypeDisplayName` 値に対して、対応する .NET アセンブリの [AttributeMetadata](/dotnet/api/microsoft.xrm.sdk.metadata.attributemetadata) 派生クラスが使用可能な場所に含まれます。 これらのタイプと `AttributeTypeDisplayName` ラベルの間には 1 対 1 の関係はありません。
- カスタム属性として作成できる属性タイプには、UI に表示される、対応するラベルが含まれます。


|カテゴリ|AttributeTypeDisplayName/<br />AttributeMetadata タイプ|作成可能/<br />ラベル|説明  |
|---------|---------|---------|---------|
|分類|`BooleanType`<br />[BooleanAttributeMetadata](/dotnet/api/microsoft.xrm.sdk.metadata.booleanattributemetadata)|あり<br />**2 つのオプション**|通常は true または false の値を示す 2 つのオプションから選択されたオプション値を含みます。<br />詳細: [オプション セット](#option-sets)|
|分類|`EntityNameType`<br />[EntityNameAttributeMetadata](/dotnet/api/microsoft.xrm.sdk.metadata.entitynameattributemetadata)|なし|システム内のエンティティに対応するオプション値が含まれます。 内部のみで使用|
|分類|`MultiSelectPicklistType`<br />[MultiSelectPicklistAttributeMetadata](/dotnet/api/microsoft.xrm.sdk.metadata.multiselectpicklistattributemetadata)|あり<br />**MultiSelect オプション セット**|複数のオプションを選択できる複数のオプション値が含まれます。<br />詳細: <br />[Option Sets](#option-sets)<br />[複数選択候補リスト属性](/dynamics365/customer-engagement/developer/multi-select-picklist)|
|分類|`PicklistType`<br />[PicklistAttributeMetadata](/dotnet/api/microsoft.xrm.sdk.metadata.picklistattributemetadata)|あり<br />**オプション セット**|1 つのオプションを選択できる、選択されたオプション値を含みます。<br />詳細: [オプション セット](#option-sets)|
|分類|`StateType`<br />[StateAttributeMetadata](/dotnet/api/microsoft.xrm.sdk.metadata.stateattributemetadata)|なし|エンティティ レコードのステータスを記述するオプション値が含まれます。<br />詳細: [オプション セット](#option-sets)|
|分類|`StatusType`<br />[StatusAttributeMetadata](/dotnet/api/microsoft.xrm.sdk.metadata.statusattributemetadata)|なし|エンティティ レコードの状態の理由を説明するオプション値が含まれます。<br />詳細: [オプション セット](#option-sets)|
|集荷|`CalendarRulesType`|なし|`CalendarRules` エンティティ レコードのコレクションを含みます。<br />このタイプを使用する属性はありません。 プロキシを生成する際、コード生成ツールは、メタデータに存在しない 2 つのシミュレーション属性を作成します。 これらの属性は、一対多でエンティティ レコードに関連付けられているカレンダー ルール レコードのビューを表します。|
|集荷|`PartyListType`|なし|`ActivityParty` エンティティ レコードのコレクションを含みます。<br />詳細: [ActivityParty エンティティ](#activityparty-entity)|
|日付と時間|`DateTimeType`<br />[DateTimeAttributeMetadata](/dotnet/api/microsoft.xrm.sdk.metadata.datetimeattributemetadata)|あり<br />**日付と時間**|日付と時刻の値を含みます。<br />すべての日付と時刻の属性は、1753 年 1 月 1 日午前 12:00 以降の日付をサポートします。|
|イメージ|`ImageType`<br />[ImageAttributeMetadata]()|あり<br />**画像**|エンティティ レコードのイメージ データの取得をサポートするためのデータが含まれています。<br />詳細: [エンティティ イメージ](entity-metadata.md#entity-images)|
|管理プロパティ|`ManagedPropertyType`<br />[ManagedPropertyAttributeMetadata](/dotnet/api/microsoft.xrm.sdk.metadata.imageattributemetadata)|なし|エンティティ レコードに格納されているソリューション コンポーネントを、管理ソリューションに含めるときにカスタマイズできるかどうかを示すデータが含まれています。<br />詳細: [管理プロパティ](introduction-solutions.md#managed-properties)|
|数量|`BigIntType`<br />[BigIntAttributeMetadata](/dotnet/api/microsoft.xrm.sdk.metadata.bigintattributemetadata)|なし|`BigInt` 値を含みます。 内部のみで使用|
|数量|`DecimalType`<br />[DecimalAttributeMetadata](/dotnet/api/microsoft.xrm.sdk.metadata.decimalattributemetadata)|あり<br />**10 進数**|`Decimal` 値を含みます。 `Precision` プロパティで精度を設定します。|
|数量|`DoubleType`<br />[DoubleAttributeMetadata](/dotnet/api/microsoft.xrm.sdk.metadata.doubleattributemetadata)|あり<br />**浮動小数点数**|`Double` 値を含みます。 `Precision` プロパティで精度を設定します。|
|数量|`IntegerType`<br />[IntegerAttributeMetadata](/dotnet/api/microsoft.xrm.sdk.metadata.integerattributemetadata)|あり<br />**整数**|`Int` 値を含みます|
|<a name='money_type'></a>数量|`MoneyType`<br />[MoneyAttributeMetadata](/dotnet/api/microsoft.xrm.sdk.metadata.moneyattributemetadata)|あり<br />**通貨**|`Decimal` 値を含みます。 `PrecisionSource` プロパティは、精度のレベルを決定します。<br />0 : `Precision` プロパティ<br />1 : `Organization.PricingDecimalPrecision` 属性<br />2 : `TransactionCurrency.CurrencyPrecision` エンティティ レコードの属性|
|参照|`CustomerType`<br />[LookupAttributeMetadata](/dotnet/api/microsoft.xrm.sdk.metadata.lookupattributemetadata)|あり<br />**顧客**|取引先企業または取引先担当者エンティティ レコードへの参照が含まれます。|
|参照|`LookupType`<br />[LookupAttributeMetadata](/dotnet/api/microsoft.xrm.sdk.metadata.lookupattributemetadata)|あり<br />**検索**|エンティティ レコードへの参照を含みます。 有効なレコードの論理名は通常、属性の `Targets` プロパティに格納されます。|
|参照|`OwnerType`<br />[LookupAttributeMetadata](/dotnet/api/microsoft.xrm.sdk.metadata.lookupattributemetadata)|なし|ユーザー エンティティ レコードまたはチーム エンティティ レコードへの参照が含まれます。|
|String|`MemoType`<br />[MemoAttributeMetadata](/dotnet/api/microsoft.xrm.sdk.metadata.memoattributemetadata)|あり<br />**複数行テキスト**|複数行テキストボックスに表示するための文字列値が含まれています。|
|String|`StringType`<br />[StringAttributeMetadata](/dotnet/api/microsoft.xrm.sdk.metadata.stringattributemetadata)|あり<br />**1 行テキスト**|単一行テキストボックスに表示するための文字列値が含まれています。|
|一意識別子|`UniqueidentifierType`<br />[UniqueIdentifierAttributeMetadata](/dotnet/api/microsoft.xrm.sdk.metadata.uniqueidentifierattributemetadata)|なし|GUID 固有の識別子値が含まれます。|
|仮想|`VirtualType`|なし|これらの属性はコードで使用することはできず、一般的に無視することができます。|


## <a name="supported-operations-and-form-usage-for-attributes"></a>属性でサポートされている操作とフォームの使用法

各属性には、参加可能な操作の種類と、その操作がどのようにフォームに含まれるかを記述するブール値のプロパティが含まれています。

|プロパティ|説明|
|--|--|
|`IsRequiredForForm`|属性をフォーム内のフィールドとして含める必要があるかどうか。|
|`IsValidForCreate`|属性値を作成操作で設定できるかどうか。|
|`IsValidForForm`|属性をフォーム内のフィールドとして含めることができるかどうか。|
|`IsValidForRead`|属性値を取得できるかどうか。|
|`IsValidForUpdate`|更新操作で属性値を設定できるかどうか。|

その操作に無効な属性の作成操作または更新操作で値を設定しようとすると、その値は無視されます。
読み取りに有効でない属性を取得しようとすると、null 値が返されます。


## <a name="attribute-requirement-level"></a>属性の入力要求レベル

`RequiredLevel` プロパティは、属性値が必要かどうかを記述するブール管理プロパティです。

このプロパティには次の値を設定できます。

|Name|Value|UI ラベル|説明|
|--|--|--|--|
|`None`|0|**任意出席者**|要件は指定されていません。|
|`SystemRequired`|1|**システム要件**|属性には値が必要です。|
|`ApplicationRequired`|2|**必須項目**|この属性は、部署が値を持つために必要です。|
|`Recommended`|3|**推奨項目**|属性は値があることが推奨されます。|

Common Data Service では、システムによって作成された属性に対してのみ `SystemRequired` オプションが適用されます。 カスタム属性は、`SystemRequired` オプションを使用するように設定することはできません。 

モデル駆動型アプリケーションでは、`ApplicationRequired` オプションが強制され、`Recommended` オプションには別のプレゼンテーションが使用されます。 ユーザー定義のクライアントの作成者は、この情報を使用して、同様の検証または表示オプションを要求する場合があります。

これは管理プロパティであるため、管理ソリューションの発行元として、ソリューションのコンシューマーがソリューション内の属性のこれらの設定を変更できるかどうかを判断できます。

詳細: [管理プロパティ](introduction-solutions.md#managed-properties)


## <a name="rollup-and-calculated-attributes"></a>ロールアップおよび計算属性

計算およびロールアップ属性を使用すると、手動で計算を実行する必要がなくなるので、作業に集中できます。 システム管理者は、開発者と作業をすることなく、多くの共通計算の値を含むフィールドを定義できます。 開発者も、自分のコード内ではなく、プラットフォーム機能を活用してこれらの計算を実行できます。

詳細: 
- [Common Data Service カスタマイズ ガイド: 値を集約するロールアップ フィールドを定義](/dynamics365/customer-engagement/customize/define-rollup-fields)
- [Common Data Service カスタマイズ ガイド: 計算およびロールアップ属性](/dynamics365/customer-engagement/customize/define-calculated-fields)
- [計算およびロールアップ属性](/dynamics365/customer-engagement/developer/calculated-rollup-attributes)

## <a name="attribute-format"></a>属性フォーマット

属性の書式値は、モデル駆動型アプリでの表示方法を制御します。 カスタム アプリの開発者は、この情報を使用して同様のエクスペリエンスを作成できます。

### <a name="integer-formats"></a>整数形式

この種類の代替ユーザー エクスペリエンスを表示するには、整数属性で `Format` プロパティを使用します。

|オプション|説明|
|--|--|
|`None`|数値を編集するためのテキスト ボックスを表示します。|
|`Duration`|時間間隔を含むドロップダウン リストが表示されます。 このリストから値を選択するか、分を表す整数値を入力できます。|
|`TimeZone`|タイム ゾーンのリストを含むドロップダウン リストが表示されます。|
|`Language`|組織で有効になっている言語のリストを含むドロップダウン リストが表示されます。 他の言語が有効になっていない場合は、基本言語が唯一のオプションになります。 保存される値は、言語の LCID 値です。|

### <a name="string-formats"></a>文字列形式

文字列属性で `FormatName` プロパティを使用して、[StringFormatName クラス](/dotnet/api/microsoft.xrm.sdk.metadata.stringformatname) の値を設定して、文字列属性のフォーマット方法を制御します。

|Name|説明|
|--|--|
|`Email`|フォーム フィールドはテキスト値を電子メール アドレスとして検証し、フィールドに mailto リンクを作成します。|
|`PhoneNumber`|フォーム フィールドには Skype を使用して、電話の発信ためのリンクも含まれています。|
|`PhoneticGuide`|内部のみで使用。|
|`Text`|フォームにテキスト ボックスが表示されます。|
|`TextArea`|フォームにテキスト領域フィールドが表示されます。|
|`TickerSymbol`|株式銘柄コードの見積もりを表示するためのリンクがフォームに表示されます。|
|`URL`|URL をオープンするためのリンクがフォームに表示されます。|
|`VersionNumber`|内部のみで使用|

### <a name="date-and-time-formats"></a>日付と時刻の形式

`DateTimeBehavior` プロパティは、日時属性の動作を制御します。
3 種類のオプションがあります。

|オプション|短い説明:|
|--|--|
|`UserLocal`|日時値を UTC 値としてシステムに格納します。|
|`DateOnly`|実際値の日付の値を、時刻値 12:00 AM (00:00:00) で、システムに格納します。|
|`TimeZoneIndependent`|ユーザーのタイムゾーンに関係なく、実際の日時値をシステムに格納します。|

`Format` プロパティ コントロールを使用して、`DateTimeBehavior` に関係なく、モデル駆動型アプリで値を表示する方法を指定します。

|オプション|説明|
|--|--|
|DateAndTime|完全な日時を表示します。|
|DateOnly|日付のみを表示します。|

詳細: [日時属性の動作と形式](/dynamics365/customer-engagement/developer/behavior-format-date-time-attribute)。

## <a name="auto-number-attributes"></a>自動付番の属性

任意のエンティティの自動付番の属性を追加できます。 現在は、プログラムで属性を追加することができます。 この種類の属性を追加するユーザー インターフェイスはありません。
詳細: [自動付番の属性を作成](/dynamics365/customer-engagement/developer/create-auto-number-attributes)

## <a name="option-sets"></a>オプション セット

オプションのセットを表示するこれらの属性は、属性によって定義されたオプションのセットを参照することができます。または、複数の属性で共有できるオプションのセットを参照することもできます。 これは、ある属性の値が他の属性にも当てはまる場合に特に便利です。 共通のオプション セットを参照することで、オプションを 1 か所で管理することができます。 共有できるオプション セットは*グローバル* オプション セットです。 属性内で定義されたものは、*ローカル* オプション セットです。

### <a name="retrieve-options-data"></a>オプション データの取得
組織サービスは、属性によって使用されるオプションを取得するために使用できる要求クラスを提供します。

#### <a name="use-the-organization-service-to-retrieve-options"></a>組織サービスを使用してオプションを取得する

オプションを持つ各属性は、[EnumAttributeMetadata](/dotnet/api/microsoft.xrm.sdk.metadata.enumattributemetadata) を継承し、[OptionSet プロパティ](/dotnet/api/microsoft.xrm.sdk.metadata.enumattributemetadata.optionset) プロパティを含みます。 このプロパティには、[Options プロパティ](/dotnet/api/microsoft.xrm.sdk.metadata.optionsetmetadata.options) 内のオプションを含む [OptionSetMetadata](/dotnet/api/microsoft.xrm.sdk.metadata.optionsetmetadata) が含まれています。 

組織サービスでは、次のメッセージを使用してオプションに関する情報を取得できます。

|Request Class|説明|
|--|--|
|[RetrieveAllOptionSetsRequest](/dotnet/api/microsoft.xrm.sdk.messages.retrievealloptionsetsrequest) |すべての*グローバル* オプション セットに関するデータを取得する|
|[RetrieveAttributeRequest](/dotnet/api/microsoft.xrm.sdk.messages.retrieveattributerequest) |すべての*ローカル* オプション セットを含む属性に関するデータを取得する|
|[RetrieveMetadataChangesRequest](/dotnet/api/microsoft.xrm.sdk.messages.retrievemetadatachangesrequest) |*ローカル* オプション セットを含むことができるクエリに基づいてメタデータを取得する<br />詳細: [メタデータへの変更の取得および検出](/dynamics365/customer-engagement/developer/retrieve-detect-changes-metadata)|
|[RetrieveOptionSetRequest](/dotnet/api/microsoft.xrm.sdk.messages.retrieveoptionsetrequest) |*グローバル* オプション セットに関するデータを取得します。|

詳細: 
- [サンプル: 属性候補リストのメタデータをファイルにダンプする](/dynamics365/customer-engagement/developer/org-service/sample-dump-attribute-picklist-metadata-file)
- [Common Data Service の開発者ガイド: グローバル オプション セットのカスタマイズ](/dynamics365/customer-engagement/developer/org-service/customize-global-option-sets)

#### <a name="use-the-web-api-to-retrieve-options"></a>Web API を使用してオプションを取得する

Web API は、オプション値を照会するための RESTful スタイルを提供します。 エンティティ内の属性を取得することによって、ローカル オプションまたはグローバル オプションを取得できます。 次の例では、[Account](reference/entities/account.md).[AccountCategoryCode property](reference/entities/account.md#BKMK_AccountCategoryCode)に含まれるオプションの [OptionSetMetadata](/dynamics365/customer-engagement/web-api/optionsetmetadata) を返します。

`GET <organization url>/api/data/v9.0/EntityDefinitions(LogicalName='account')/Attributes(LogicalName='accountcategorycode')/Microsoft.Dynamics.CRM.PicklistAttributeMetadata?$select=LogicalName&$expand=OptionSet`

Web API を使用すると、[RetrieveMetadataChanges 関数](/dynamics365/customer-engagement/web-api/retrievemetadatachanges)を使用することもできます。

詳細: [Web API を使用したクエリ メタデータ > EntityMetadata 属性のクエリ](/dynamics365/customer-engagement/developer/webapi/query-metadata-web-api#querying-entitymetadata-attributes)



## <a name="attribute-mapping"></a>属性マッピング

既存のエンティティ レコードのコンテキストで新しいエンティティ レコードを作成すると、既存のエンティティ レコードの特定の値を新しいエンティティ レコードの既定値として自動的に転送できます。 これにより、モデル駆動型アプリを使用するユーザーのデータ入力が合理化されます。 アプリ ユーザーはマップされた値を参照し、エンティティを保存する前にそれらの値を編集できます。

カスタム クライアントを作成する開発者は、`InitializeFrom` メッセージ (組織サービス  [InitializeFromRequest Class](/dotnet/api/microsoft.crm.sdk.messages.initializefromrequest) または Web API [InitializeFrom 関数](/dynamics365/customer-engagement/web-api/initializefrom)) を使用して、構成された既定値が設定されたエンティティ データを取得することで同じ動作を実現できます。

詳細 
- [Common Data Service カスタマイズ ガイド: エンティティ フィールドのマップ](/dynamics365/customer-engagement/customize/map-entity-fields#BKMK_mappingEntityFields)
- [Common Data Service の開発者ガイド エンティティおよび属性マッピングのカスタマイズ](/dynamics365/customer-engagement/developer/customize-entity-attribute-mappings)

### <a name="see-also"></a>関連項目

[Common Data Service エンティティ](entities.md)
