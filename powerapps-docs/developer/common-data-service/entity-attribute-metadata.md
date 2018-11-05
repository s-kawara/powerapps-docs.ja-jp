---
title: 属性メタデータ | Microsoft Docs
description: Common Data Service for Apps での属性メタデータの使用について説明します。
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
ms.date: 03/12/2018
ms.author: jdaly
search.audienceType:
- developer
search.app:
- PowerApps
- D365CE
ms.openlocfilehash: f6fcf3ba1e8e9773df65ac566a9d5c798f4d13a9
ms.sourcegitcommit: 429b83aaa5a91d5868e1fbc169bed1bac0c709ea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/24/2018
ms.locfileid: "42859163"
---
# <a name="attribute-metadata"></a>属性メタデータ

エンティティには、各レコードに含めることができるデータを表す属性のコレクションが含まれます。 開発者は、さまざまな種類の属性について、また、それらの操作方法について理解する必要があります。 

詳細情報: [Dynamics 365 Customer Engagement の開発者ガイド: エンティティ属性の概要](/dynamics365/customer-engagement/developer/introduction-entity-attributes)

## <a name="attribute-names"></a>属性名

エンティティと同様、各属性は作成時に定義された一意の名前を持っています。 この名前は、いくつかの方法で表現されます。


|名前 |説明  |
|---------|---------|
|`SchemaName`|通常、論理名をパスカル ケースで表します。 例: `AccountNumber`|
|`LogicalName`|すべて小文字の名前です。 例: `accountnumber`|

カスタム属性を作成する場合、選択した名前の先頭には、属性が作成されたソリューションに関連付けられたソリューション発行者のカスタマイズ接頭辞が付加されます。

属性を作成した後、その名前を変更することはできません。

また、各属性には、ローカライズされた値を表示できる 2 つのプロパティがあります。 それらは、アプリ内で属性を参照するために使用される値です。

|名前 |説明  |
|---------|---------|
|`DisplayName`|通常、スキーマ名と同じですが、スペースを含めることができます。 例: **Account Number**|
|`Description`|属性を説明、またはユーザーにガイダンスを提示する短い文です。 例: *Type an ID number or code for the account to quickly search and identify the account in system views (システム ビュー内でアカウントを迅速に検索および特定するにはアカウントの ID 番号またはコードを入力してください).*<br />モデル駆動型アプリでは、ユーザーがフォーム内で、この属性のフィールド上にカーソルを移動すると、この情報が表示されます。|


これらは、アプリ内で属性を参照するために使用されるローカライズ可能な値です。 これらの値は、いつでも変更できます。 ローカライズされた値を追加または編集するには、「[Dynamics 365 Customer Engagement のカスタマイズ ガイド: カスタマイズされたエンティティおよびフィールド テキストを他の言語に翻訳する](/dynamics365/customer-engagement/customize/export-customized-entity-field-text-translation)」を参照してください。

## <a name="attribute-types"></a>属性の型

`AttributeTypeName` プロパティでは属性の型を示します。 このプロパティには、存在するさまざまな属性の各々にラベルを指定する型 `AttributeTypeDisplayName` の値が含まれます。 

> [!NOTE]
> `AttributeType` プロパティと混同しないでください。 この古いプロパティの値は、多くの場合 `AttributeTypeName` と一致します。ただし、後者の場合、`ImageType` 属性は `Virtual` として表示されます。 `AttributeType` プロパティではなく、`AttributeTypeName` プロパティを参照してください。

表の説明:

- これらの型は、比較のためにカテゴリ別にグループ化されています。
- `AttributeTypeDisplayName` の各値に対して、可能な場合は対応する .NET アセンブリ [AttributeMetadata](/dotnet/api/microsoft.xrm.sdk.metadata.attributemetadata) 派生クラスが含められます。 これらの型と `AttributeTypeDisplayName` ラベルとの間に 1:1 のリレーションシップはありません。
- カスタム属性として作成できるそのような属性の型には、UI に表示される対応するラベルが含まれます。


|Category|AttributeTypeDisplayName/<br />AttributeMetadata 型|作成可能かどうか/<br />ラベル|説明  |
|---------|---------|---------|---------|
|分類|`BooleanType`<br />[BooleanAttributeMetadata](/dotnet/api/microsoft.xrm.sdk.metadata.booleanattributemetadata)|はい<br />**2 つのオプション**|通常、true 値または false 値を示す 2 つのオプションのうち、選択したオプション値が含まれます。<br />詳細情報: [オプション セット](#option-sets)|
|分類|`EntityNameType`<br />[EntityNameAttributeMetadata](/dotnet/api/microsoft.xrm.sdk.metadata.entitynameattributemetadata)|いいえ|システム内のエンティティに対応するオプション値が含まれます。 内部使用専用。|
|分類|`MultiSelectPicklistType`<br />[MultiSelectPicklistAttributeMetadata](/dotnet/api/microsoft.xrm.sdk.metadata.multiselectpicklistattributemetadata)|はい<br />**MultiSelect オプション セット**|複数のオプションを選択できる場合に、選択した複数のオプション値が含まれます。<br />詳細情報: <br />[オプション セット](#option-sets)<br />[Dynamics 365 Customer Engagement の開発者ガイド: 複数選択候補リスト属性](/dynamics365/customer-engagement/developer/multi-select-picklist)|
|分類|`PicklistType`<br />[PicklistAttributeMetadata](/dotnet/api/microsoft.xrm.sdk.metadata.picklistattributemetadata)|はい<br />**オプション セット**|いずれか 1 つのオプションを選択できる場合に、選択したオプションの値が含まれます。<br />詳細情報: [オプション セット](#option-sets)|
|分類|`StateType`<br />[StateAttributeMetadata](/dotnet/api/microsoft.xrm.sdk.metadata.stateattributemetadata)|いいえ|エンティティ レコードのステータスを示すオプション値が含まれます。<br />詳細情報: [オプション セット](#option-sets)|
|分類|`StatusType`<br />[StatusAttributeMetadata](/dotnet/api/microsoft.xrm.sdk.metadata.statusattributemetadata)|いいえ|エンティティ レコードのステータスの理由を示すオプション値が含まれます。<br />詳細情報: [オプション セット](#option-sets)|
|コレクション|`CalendarRulesType`|いいえ|`CalendarRules` エンティティ レコードのコレクションが含まれます。<br />この型を使用する属性はありません。 プロキシを生成する場合は、コード生成ツールによって、メタデータに存在しない 2 つのシミュレーション属性が作成されます。 これらの属性は、一対多のリレーションシップでエンティティ レコードに関連付けられたカレンダー ルール レコードのビューを表します。|
|コレクション|`PartyListType`|いいえ|`ActivityParty` エンティティ レコードのコレクションが含まれます。<br />詳細情報: [ActivityParty エンティティ](#activityparty-entity)|
|日付と時刻|`DateTimeType`<br />[DateTimeAttributeMetadata](/dotnet/api/microsoft.xrm.sdk.metadata.datetimeattributemetadata)|はい<br />**日付と時刻**|日付と時刻の値が含まれます。<br />日付と時刻の属性はすべて、1753 年 1 月 1 日、午前 12 時 00 分からの値をサポートします。|
|イメージ|`ImageType`<br />[ImageAttributeMetadata]()|はい<br />**イメージ**|エンティティ レコードのイメージ データの取得をサポートするデータが含まれます。<br />詳細情報: [エンティティ イメージ](entity-metadata.md#entity-images)|
|マネージド プロパティ|`ManagedPropertyType`<br />[ManagedPropertyAttributeMetadata](/dotnet/api/microsoft.xrm.sdk.metadata.imageattributemetadata)|いいえ|エンティティ レコードに格納されているソリューション コンポーネントを、マネージド ソリューションに取り込む場合に、カスタマイズできるかどうかを示すデータが含まれます。<br />詳細情報: [マネージド プロパティ](introduction-solutions.md#managed-properties)|
|数量|`BigIntType`<br />[BigIntAttributeMetadata](/dotnet/api/microsoft.xrm.sdk.metadata.bigintattributemetadata)|いいえ|`BigInt` の値が含まれます。 内部使用専用。|
|数量|`DecimalType`<br />[DecimalAttributeMetadata](/dotnet/api/microsoft.xrm.sdk.metadata.decimalattributemetadata)|はい<br />**10 進数**|`Decimal` の値が含まれます。 `Precision` プロパティでは、有効桁数のレベルを設定します。|
|数量|`DoubleType`<br />[DoubleAttributeMetadata](/dotnet/api/microsoft.xrm.sdk.metadata.doubleattributemetadata)|はい<br />**浮動小数点数**|`Double` の値が含まれます。 `Precision` プロパティでは、有効桁数のレベルを設定します。|
|数量|`IntegerType`<br />[IntegerAttributeMetadata](/dotnet/api/microsoft.xrm.sdk.metadata.integerattributemetadata)|はい<br />**整数**|`Int` の値が含まれます。|
|数量|`MoneyType`<br />[MoneyAttributeMetadata](/dotnet/api/microsoft.xrm.sdk.metadata.moneyattributemetadata)|はい<br />**通貨**|`Decimal` の値が含まれます。 `PrecisionSource` プロパティでは、有効桁数のレベルが設定されている場所を特定します。<br />0 : `Precision` プロパティ<br />1 : `Organization.PricingDecimalPrecision` 属性<br />2: エンティティ レコード内の `TransactionCurrency.CurrencyPrecision` 属性|
|リファレンス|`CustomerType`<br />[LookupAttributeMetadata](/dotnet/api/microsoft.xrm.sdk.metadata.lookupattributemetadata)|はい<br />**顧客**|アカウントまたは連絡先エンティティ レコードへの参照が含まれます。|
|リファレンス|`LookupType`<br />[LookupAttributeMetadata](/dotnet/api/microsoft.xrm.sdk.metadata.lookupattributemetadata)|はい<br />**検索**|エンティティ レコードへの参照が含まれます。 有効なレコードの論理名は、通常、属性の `Targets` プロパティに格納されます。|
|リファレンス|`OwnerType`<br />[LookupAttributeMetadata](/dotnet/api/microsoft.xrm.sdk.metadata.lookupattributemetadata)|いいえ|ユーザーまたはチーム エンティティ レコードへの参照が含まれます。|
|String|`MemoType`<br />[MemoAttributeMetadata](/dotnet/api/microsoft.xrm.sdk.metadata.memoattributemetadata)|はい<br />**複数行テキスト**|複数行テキスト ボックスに表示するための文字列値が含まれます。|
|String|`StringType`<br />[StringAttributeMetadata](/dotnet/api/microsoft.xrm.sdk.metadata.stringattributemetadata)|はい<br />**1 行テキスト**|単一行のテキスト ボックスに表示するための文字列値が含まれます。|
|一意識別子|`UniqueidentifierType`<br />[UniqueIdentifierAttributeMetadata](/dotnet/api/microsoft.xrm.sdk.metadata.uniqueidentifierattributemetadata)|いいえ|GUID 一意識別子値が含まれます。|
|仮想|`VirtualType`|いいえ|これらの属性はコード内では使用できず、通常は無視することができます。|


## <a name="supported-operations-and-form-usage-for-attributes"></a>属性についてサポートされる操作とフォームの使用

各属性には、それぞれが参加することができる操作の種類と、それぞれをフォームに含める方法を記述したブール型プロパティが含まれます。

|プロパティ|説明|
|--|--|
|`IsRequiredForForm`|属性を、フォーム内にフィールドとして含める必要があるかどうか。|
|`IsValidForCreate`|作成操作に属性値を設定できるかどうか。|
|`IsValidForForm`|属性を、フォーム内にフィールドとして含めることができるかどうか。|
|`IsValidForRead`|属性値を取得できるかどうか。|
|`IsValidForUpdate`|更新操作に属性値を設定できるかどうか。|

作成操作または更新操作において、これらの操作に使用できない属性に値を設定しようとした場合、値は無視されます。
読み取りができない属性の取得を試みた場合は、null 値が返されます。


## <a name="attribute-requirement-level"></a>属性要求レベル

`RequiredLevel` プロパティは、属性値が必要かどうかを示すブール型のマネージド プロパティです。

このプロパティには、次の値を設定できます。

|名前|値|UI ラベル|説明|
|--|--|--|--|
|`None`|0|**省略可能**|要件は指定されません。|
|`SystemRequired`|1|**システム要件**|属性には値を設定する必要があります。|
|`ApplicationRequired`|2|**必須項目**|属性に値を設定することがビジネスで必要です。|
|`Recommended`|3|**推奨項目**|属性に値を設定することをお勧めします。|

Common Data Service for Apps では、システムによって作成された属性に対して `SystemRequired` オプションが適用されるだけです。 `SystemRequired` オプションを使用するように、カスタム属性を設定することはできません。 

モデル駆動型アプリでは、`ApplicationRequired` オプションが適用され、`Recommended` オプションについては別の表現が使用されます。 カスタム クライアントの作成者は、この情報を使用して、同様の検証または表示オプションを要求する場合があります。

これはマネージド プロパティであるため、マネージド ソリューションの発行者として、ソリューションの顧客がソリューション内で属性に対する前述の設定を変更できるかどうかを決めることができます。

詳細情報: [マネージド プロパティ](introduction-solutions.md#managed-properties)


## <a name="rollup-and-calculated-attributes"></a>ロールアップ属性と計算属性

計算属性およびロールアップ属性を使用することで、ユーザーは計算を手動で実行しなくても済むようになり、本来の作業に集中することができます。 システム管理者は、開発者と共同作業を行わなくても、一般的な多くの計算の値を格納するフィールドを定義できます。 開発者は独自のコード内の機能ではなく、プラットフォームの機能を活用して、そのような計算を実行することもできます。

詳細情報: 
- [Dynamics 365 Customer Engagement のカスタマイズ ガイド: 値を集約するロールアップ フィールドを定義](/dynamics365/customer-engagement/customize/define-rollup-fields)
- [Dynamics 365 Customer Engagement のカスタマイズ ガイド: 計算フィールドを定義して手動計算を自動化する](/dynamics365/customer-engagement/customize/define-calculated-fields)
- [Dynamics 365 Customer Engagement の開発者ガイド: 計算およびロールアップ属性](/dynamics365/customer-engagement/developer/calculated-rollup-attributes)

## <a name="attribute-format"></a>属性の形式

属性の形式値では、モデル駆動型アプリにおける表示方法を制御します。 カスタム アプリの開発者は、この情報を使用して、同様のエクスペリエンスを作成することができます。

### <a name="integer-formats"></a>整数の形式

`Format` プロパティを整数型の属性で使用して、この型のための代替ユーザー エクスペリエンスを表示します。

|オプション|説明|
|--|--|
|`None`|数値を編集するテキスト ボックスを表示します。|
|`Duration`|時間間隔が含まれたドロップダウン リストを表示します。 ユーザーは一覧から値を選択することも、分数を表す整数値を入力することもできます。|
|`TimeZone`|タイム ゾーンの一覧が含まれたドロップダウン リストを表示します。|
|`Language`|組織に対して有効にされている言語の一覧が含まれたドロップダウン リストを表示します。 他に有効になっている言語がない場合は、基本言語が唯一のオプションとなります。 保存される値は、言語の LCID 値です。|

### <a name="string-formats"></a>文字列の形式

文字列型の属性で `FormatName` プロパティを使用して、[StringFormatName クラス](/dotnet/api/microsoft.xrm.sdk.metadata.stringformatname)から値を設定し、文字列型の属性を書式設定する方法を制御します。

|名前|説明|
|--|--|
|`Email`|フォーム フィールドでは、電子メール アドレスとしてのテキスト値を検証し、フィールドに mailto リンクを作成します。|
|`PhoneNumber`|フォーム フィールドには、Skype を使用して電話を開始するリンクが含まれます。|
|`PhoneticGuide`|内部使用専用。|
|`Text`|フォームに、テキスト ボックスが表示されます。|
|`TextArea`|フォームに、テキスト領域のフィールドが表示されます。|
|`TickerSymbol`|フォームに、株式銘柄の相場を表示するためのリンクが表示されます。|
|`URL`|フォームに、URL を開くためのリンクが表示されます。|
|`VersionNumber`|内部使用専用。|

### <a name="date-and-time-formats"></a>日付と時刻の形式

日付および時刻の属性の動作を制御するための `DateTimeBehavior` プロパティ。
オプションは 3 つあります。

|オプション|簡単な説明|
|--|--|
|`UserLocal`|日付と時刻の値を UTC 値としてシステムに格納します。|
|`DateOnly`|実際の日付値と、午前 12:00 (00:00:00) のような時刻値をシステムに格納します。|
|`TimeZoneIndependent`|ユーザーのタイム ゾーンに関係なく、実際の日付と時刻の値をシステムに格納します。|

`DateTimeBehavior` に関係なくモデル駆動型アプリでの値の表示方法を制御するには、`Format` プロパティを使用します。

|オプション|説明|
|--|--|
|DateAndTime|日付と時刻を完全に表示します。|
|DateOnly|日付のみを表示します。|

詳細情報: [Dynamics 365 Customer Engagement の開発者ガイド: 日時属性の動作と形式](/dynamics365/customer-engagement/developer/behavior-format-date-time-attribute)

## <a name="auto-number-attributes"></a>自動付番の属性

任意のエンティティに対して自動付番の属性を追加することができます。 現在、プログラムによって属性を追加することができます。 この型の属性に追加するユーザー インターフェイスはありません。
詳細情報: [Dynamics 365 Customer Engagement の開発者ガイド: 自動付番の属性を作成](/dynamics365/customer-engagement/developer/create-auto-number-attributes)

## <a name="option-sets"></a>オプション セット

オプション セットを表示する前述属性は、属性で定義されているオプション セットを参照できます。あるいは、1 つまたは複数の属性によって共有できる個別のオプション セットを参照することもできます。 このことは、1 つの属性の値を他の属性にも適用する場合に特に便利です。 共通のオプション セットを参照すれば、オプションを 1 か所で保守できます。 それらの共有できるオプション セットは、"*グローバル*" オプションです。 属性内で定義されているオプション セットは、"*ローカル*" オプション セットです。

### <a name="retrieve-options-data"></a>オプション データを取得する
組織のサービスでは、属性によって使用されるオプションを取得する際に使用できる要求クラスを提供します。

#### <a name="use-the-organization-service-to-retrieve-options"></a>組織のサービスを使用してオプションを取得する

オプションを持つ各属性は、[EnumAttributeMetadata](/dotnet/api/microsoft.xrm.sdk.metadata.enumattributemetadata) から継承され、[OptionSet プロパティ](/dotnet/api/microsoft.xrm.sdk.metadata.enumattributemetadata.optionset)を含みます。 このプロパティには、[Options プロパティ](/dotnet/api/microsoft.xrm.sdk.metadata.optionsetmetadata.options)にオプションを取り込む [OptionSetMetadata](/dotnet/api/microsoft.xrm.sdk.metadata.optionsetmetadata) が含まれます。 

組織のサービスを使用すると、次のメッセージを使用して、オプションセットに関する情報を取得することができます。

|要求クラス|説明|
|--|--|
|[RetrieveAllOptionSetsRequest](/dotnet/api/microsoft.xrm.sdk.messages.retrievealloptionsetsrequest) |すべての "*グローバル*" オプションセットに関するデータを取得します。|
|[RetrieveAttributeRequest](/dotnet/api/microsoft.xrm.sdk.messages.retrieveattributerequest) |任意の "*ローカル*" オプションセットが含まれる属性についてデータを取得します。|
|[RetrieveMetadataChangesRequest](/dotnet/api/microsoft.xrm.sdk.messages.retrievemetadatachangesrequest) |"*ローカル*" オプションセットを含めることができるクエリに基づいて、メタデータを取得します。<br />詳細情報: [メタデータへの変更の取得および検出](/dynamics365/customer-engagement/developer/retrieve-detect-changes-metadata)|
|[RetrieveOptionSetRequest](/dotnet/api/microsoft.xrm.sdk.messages.retrieveoptionsetrequest) |"*グローバル*" オプション セットに関するデータを取得します。|

詳細情報: 
- [サンプル: 属性候補リストのメタデータをファイルにダンプする](/dynamics365/customer-engagement/developer/org-service/sample-dump-attribute-picklist-metadata-file)
- [Dynamics 365 Customer Engagement の開発者ガイド: グローバル オプション セットのカスタマイズ](/dynamics365/customer-engagement/developer/org-service/customize-global-option-sets)

#### <a name="use-the-web-api-to-retrieve-options"></a>Web API を使用してオプションを取得する

Web API は、オプション値に対してクエリを実行するための RESTful スタイルを提供します。 エンティティ内の属性を取得することによって、ローカル オプションまたはグローバル オプションを取得できます。 次の例では、[Account](reference/entities/account.md).[AccountCategoryCode プロパティ](reference/entities/account.md#BKMK_AccountCategoryCode)に取り込まれたオプションの [OptionSetMetadata](/dynamics365/customer-engagement/web-api/optionsetmetadata) を返します。

`GET <organization url>/api/data/v9.0/EntityDefinitions(LogicalName='account')/Attributes(LogicalName='accountcategorycode')/Microsoft.Dynamics.CRM.PicklistAttributeMetadata?$select=LogicalName&$expand=OptionSet`

Web API の場合は、[RetrieveMetadataChanges 関数](/dynamics365/customer-engagement/web-api/retrievemetadatachanges)を使用することもできます。

詳細情報: [Dynamics 365 Customer Engagement の開発者ガイド: Web API を使用したクエリ メタデータ > EntityMetadata 属性をクエリ](/dynamics365/customer-engagement/developer/webapi/query-metadata-web-api#querying-entitymetadata-attributes)



## <a name="attribute-mapping"></a>属性マッピング

既存のエンティティ レコードのコンテキストで新しいエンティティ レコードを作成する場合は、既存のエンティティ レコードから特定の値を既定の値として新しいエンティティ レコードに自動的に転送することができます。 これにより、モデル駆動型アプリを使用するユーザーのデータ入力が効率的になります。 アプリケーション ユーザーはエンティティを保存する前に、マップされた値を確認し、編集することができます。

カスタム クライアントを作成する開発者が同じ動作を実現するには、`InitializeFrom`メッセージ (組織のサービスの [InitializeFromRequest](/dotnet/api/microsoft.crm.sdk.messages.initializefromrequest) クラスまたは Web API の [InitializeFrom](/dynamics365/customer-engagement/web-api/initializefrom) 関数) を使用して、構成済みの既定値が設定されたエンティティ データを取得します。

詳細 
- [Dynamics 365 Customer Engagement のカスタマイズ ガイド: エンティティ フィールドのマップ](/dynamics365/customer-engagement/customize/map-entity-fields#BKMK_mappingEntityFields)
- [Dynamics 365 Customer Engagement の開発者ガイド: エンティティ マッピングおよび属性マッピングのカスタマイズ](/dynamics365/customer-engagement/developer/customize-entity-attribute-mappings)

### <a name="see-also"></a>関連項目

[Common Data Service for Apps のエンティティ](entities.md)
