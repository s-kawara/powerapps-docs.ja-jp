---
title: 複数選択候補リストの属性 (Common Data Service) | Microsoft Docs
description: 複数のオプション選択を単一属性に格納できる複数選択候補リスト属性について説明します。
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: MicroSri
ms.author: jdaly
manager: ryjones
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="multi-select-picklist-attributes"></a>複数選択候補リスト属性

カスタマイザーは、複数オプションを選択できる属性を定義できます。 <xref:Microsoft.Xrm.Sdk.Metadata.MultiSelectPicklistAttributeMetadata> クラスは、<xref:Microsoft.Xrm.Sdk.Metadata.EnumAttributeMetadata> クラスから継承される属性の種類を定義します。 <xref:Microsoft.Xrm.Sdk.Metadata.PicklistAttributeMetadata> クラスと同様、この属性には、その属性の有効なオプションを含む <xref:Microsoft.Xrm.Sdk.Metadata.OptionSetMetadata><xref:Microsoft.Xrm.Sdk.Metadata.OptionSetMetadata.Options> プロパティが含まれます。 違いは、取得または設定する値は、選択したオプションを表す整数の配列を含む <xref:Microsoft.Xrm.Sdk.OptionSetValueCollection> 型であることです。 この属性の書式設定された値は、選択したオプションのラベルを含むセミコロンで区切られた文字列です。

Web API では、この属性は <xref href="Microsoft.Dynamics.CRM.MultiSelectPicklistAttributeMetadata?text=MultiSelectPicklistAttributeMetadata EntityType" /> を使用して定義されます。

候補リスト属性と同様、定義できるオプションの数に技術的な上限はありません。 使いやすさに関する考慮事項を限定要因として適用する必要があります。 ただし、単一の属性に対して 150 のオプションしか選択できません。 また、既定値は設定できません。

## <a name="setting-multi-select-picklist-values"></a>複数選択候補リスト値の設定

Web API では、次の例に示すように、コンマで区切られた数値を含む文字列を渡すことで値を設定します。
### <a name="request"></a>要求
```http
POST [organization uri]/api/data/v9.0/contacts HTTP/1.1
Accept: application/json
Content-Type: application/json; charset=utf-8
OData-MaxVersion: 4.0
OData-Version: 4.0

{
    "@odata.type": "Microsoft.Dynamics.CRM.contact",
    "firstname": "Wayne",
    "lastname": "Yarborough",
    "sample_outdooractivities": "1, 9"
}
```
### <a name="response"></a>応答
```http
HTTP/1.1 204 No Content
OData-Version: 4.0
OData-EntityId: [organization uri]/api/data/v9.0/contacts(0c67748a-b78d-e711-811c-000d3a75bdf1)
```

アセンブリを使用する組織サービスでは、次の C# の例に示すように、<xref:Microsoft.Xrm.Sdk.OptionSetValueCollection> を使用して、この属性の値を設定します。
```csharp
OptionSetValueCollection activities = new OptionSetValueCollection();
activities.Add(new OptionSetValue(1)); //Swimming
activities.Add(new OptionSetValue(9)); //Camping

Contact contact = new Contact();
contact["firstname"] = "Wayne";
contact["lastname"] = "Yarborough";
contact["sample_outdooractivities"] = activities;

_serviceProxy.Create(contact);
```

## <a name="query-data-from-multi-select-picklists"></a>複数選択候補リストからのクエリ データ

複数選択オプション セットでクエリ値をサポートするために、2 つの新しい条件演算子が追加されました。`ContainValues` と `DoesNotContainValues` または FetchXml の `contain-values` と `not-contain-values` 演算子です。 Web API では、同等の `ContainValues` および `DoesNotContainValues` クエリ関数があります。

この属性の型で使用できるその他の既存の条件演算子には、次が含まれます。`Equal`、`NotEqual`、`NotNull`、`Null`、`In`、`NotIn` 

> [!NOTE]
> `ContainValues` と `DoesNotContainValues` 演算子は、複数値を格納するデータベース テーブルに適用されるフルテキスト インデックスによって異なります。 新しいレコードが作成され、フルテキスト インデックスが有効になった後、いくらかの遅延があります。 新しいレコードが作成されてから、これらの演算子を使用するフィルターが値を評価するまでに、数秒を待つ必要がある場合があります。

次の例は、`contact` エンティティの `sample_outdooractivities` という名前の複数選択複数の候補リスト属性に設定された次のデータに対して `FetchXML` を使用した `ContainValues` と`not-contain-values` の使用を示しています。

### <a name="multi-select-picklist-sampleoutdooractivities-options"></a>複数選択候補リスト `sample_outdooractivities` オプション:

|Value|ラベル|
|-----|-----|
|1|水泳|
|2|ハイキング|
|3|登山|
|4|魚釣り|
|5|狩猟|
|6|実行中|
|7|船遊び|
|8|スキー|
|9|キャンプ|

### <a name="contact-entity-values"></a>取引先担当者エンティティ値

|`fullname`| `sample_outdooractivities` |
|--------|-------------------|
|Wayne Yarborough|1,9|
|Monte Orton|2|
|Randal Maple|4|
|Hiram Mundy|2,3,8,9|
|Barbara Weber|1,4,7|
|Georgette Sullivan|4,5,9|
|Verna Kennedy|2,4,9|
|Marvin Bracken|1,2,8,9|

### <a name="example-code-using-web-api"></a>Web API を使用したコード例
次の例は、ハイキングが好きなすべての取引先担当者を返す `ContainsValues` クエリ関数の使用を示しています。 適用された `odata.include-annotations="OData.Community.Display.V1.FormattedValue"` 基本設定によって、オプションのテキストがどのようにコメントとして返されるかに注意してください。

#### <a name="request"></a>要求
```http
GET [organization uri]/api/data/v9.0/contacts?$select=fullname,sample_outdooractivities&$filter=Microsoft.Dynamics.CRM.ContainValues(PropertyName='sample_outdooractivities',PropertyValues=%5B'2'%5D) HTTP/1.1
Accept: application/json
Content-Type: application/json; charset=utf-8
OData-MaxVersion: 4.0
OData-Version: 4.0
Prefer: odata.include-annotations="OData.Community.Display.V1.FormattedValue"
```
#### <a name="response"></a>応答
```http
HTTP/1.1 200 OK
Content-Type: application/json; odata.metadata=minimal
OData-Version: 4.0
Preference-Applied: odata.include-annotations="OData.Community.Display.V1.FormattedValue"
Content-Length: 1092

{
    "@odata.context": "[organization uri]/api/data/v9.0/$metadata#contacts(fullname,sample_outdooractivities)",
    "value": [{
        "@odata.etag": "W/\"529811\"",
        "fullname": "Monte Orton",
        "sample_outdooractivities@OData.Community.Display.V1.FormattedValue": "Hiking",
        "sample_outdooractivities": "2",
        "contactid": "cdbcc48e-0b8d-e711-811c-000d3a75bdf1"
    }, {
        "@odata.etag": "W/\"529823\"",
        "fullname": "Hiram Mundy",
        "sample_outdooractivities@OData.Community.Display.V1.FormattedValue": "Hiking; Mountain Climbing; Skiing; Camping",
        "sample_outdooractivities": "2,3,8,9",
        "contactid": "d7bcc48e-0b8d-e711-811c-000d3a75bdf1"
    }, {
        "@odata.etag": "W/\"529838\"",
        "fullname": "Verna Kennedy",
        "sample_outdooractivities@OData.Community.Display.V1.FormattedValue": "Hiking; Fishing; Camping",
        "sample_outdooractivities": "2,4,9",
        "contactid": "e6bcc48e-0b8d-e711-811c-000d3a75bdf1"
    }, {
        "@odata.etag": "W/\"529843\"",
        "fullname": "Marvin Bracken",
        "sample_outdooractivities@OData.Community.Display.V1.FormattedValue": "Swimming; Hiking; Skiing; Camping",
        "sample_outdooractivities": "1,2,8,9",
        "contactid": "ebbcc48e-0b8d-e711-811c-000d3a75bdf1"
    }]
}
```
次の例は、Web API を使用して、次の`FetchXml` クエリで `not-contain-values` 演算子を使用する方法を示しています。

```xml
<fetch distinct='false' no-lock='false' mapping='logical'>
    <entity name='contact'>
        <attribute name='fullname' />
        <attribute name='sample_outdooractivities' />
            <filter type='and'>
                <condition attribute='sample_outdooractivities' operator='not-contain-values'>
                    <value>2</value>
                </condition>
            </filter>
    </entity>
</fetch>
```

#### <a name="request"></a>要求
```http
GET [organization uri]/api/data/v9.0/contacts?fetchXml=%253Cfetch%2520distinct%253D'false'%2520no-lock%253D'false'%2520mapping%253D'logical'%253E%253Centity%2520name%253D'contact'%253E%253Cattribute%2520name%253D'fullname'%2520%252F%253E%253Cattribute%2520name%253D'sample_outdooractivities'%2520%252F%253E%253Cfilter%2520type%253D'and'%253E%253Ccondition%2520attribute%253D'sample_outdooractivities'%2520operator%253D'not-contain-values'%253E%253Cvalue%253E2%253C%252Fvalue%253E%253C%252Fcondition%253E%253C%252Ffilter%253E%253C%252Fentity%253E%253C%252Ffetch%253E HTTP/1.1
Accept: application/json
Content-Type: application/json; charset=utf-8
OData-MaxVersion: 4.0
OData-Version: 4.0
Prefer: odata.include-annotations="OData.Community.Display.V1.FormattedValue"
```
#### <a name="response"></a>応答
```http
HTTP/1.1 200 OK
Content-Type: application/json; odata.metadata=minimal
OData-Version: 4.0
Preference-Applied: odata.include-annotations="OData.Community.Display.V1.FormattedValue"

{
    "@odata.context": "[organization uri]/api/data/v9.0/$metadata#contacts(fullname,sample_outdooractivities,contactid)",
    "value": [{
        "@odata.etag": "W/\"529806\"",
        "fullname": "Wayne Yarborough",
        "sample_outdooractivities@OData.Community.Display.V1.FormattedValue": "Swimming; Camping",
        "sample_outdooractivities": "1,9",
        "contactid": "c8bcc48e-0b8d-e711-811c-000d3a75bdf1"
    }, {
        "@odata.etag": "W/\"529816\"",
        "fullname": "Randal Maple",
        "sample_outdooractivities@OData.Community.Display.V1.FormattedValue": "Fishing",
        "sample_outdooractivities": "4",
        "contactid": "d2bcc48e-0b8d-e711-811c-000d3a75bdf1"
    }, {
        "@odata.etag": "W/\"529828\"",
        "fullname": "Barbara Weber",
        "sample_outdooractivities@OData.Community.Display.V1.FormattedValue": "Swimming; Fishing; Boating",
        "sample_outdooractivities": "1,4,7",
        "contactid": "dcbcc48e-0b8d-e711-811c-000d3a75bdf1"
    }, {
        "@odata.etag": "W/\"529833\"",
        "fullname": "Georgette Sullivan",
        "sample_outdooractivities@OData.Community.Display.V1.FormattedValue": "Fishing; Hunting; Camping",
        "sample_outdooractivities": "4,5,9",
        "contactid": "e1bcc48e-0b8d-e711-811c-000d3a75bdf1"
    }]
}
```

### <a name="example-code-using-queryexpression-and-fetchexpression"></a>QueryExpression と FetchExpression を使用したコード例

次の C# サンプルは、`RetrieveMultiple` および組織サービスを使用して、`QueryExpression` を使用した `ContainsValues` 演算子の使用と、`FetchExpression` を使用した `not-contain-values` 演算子の使用を示しています。

```csharp
//Retrieve contacts who like hiking
//Using Query Expression
int[] hikingValue = new int[] { 2 };
ConditionExpression condition = new ConditionExpression("sample_outdooractivities", ConditionOperator.ContainValues, hikingValue);

FilterExpression filter = new FilterExpression();
filter.AddCondition(condition);

QueryExpression likesHikingQuery = new QueryExpression(Contact.EntityLogicalName);
likesHikingQuery.ColumnSet.AddColumns("fullname", "sample_outdooractivities");
likesHikingQuery.Criteria.AddFilter(filter);

EntityCollection hikers = _serviceProxy.RetrieveMultiple(likesHikingQuery);

Console.WriteLine("\nContacts who like Hiking");
Console.WriteLine("=========================");
foreach (Contact contact in hikers.Entities)
{
    string values = (contact["sample_outdooractivities"] == null) ? "null" : contact.FormattedValues["sample_outdooractivities"];
    Console.WriteLine("{0} {1}", contact.FullName, values);
}

    /*OUTPUT:
    Contacts who like Hiking
    =========================
    Monte Orton Hiking
    Hiram Mundy Hiking; Mountain Climbing; Skiing; Camping
    Verna Kennedy Hiking; Fishing; Camping
    Marvin Bracken Swimming; Hiking; Skiing; Camping
    */

//Retrieving contacts who do not like hiking:
//Using Fetch Expression
string fetchXml = @"<fetch distinct='false' no-lock='false' mapping='logical'>
                     <entity name='contact'>
                      <attribute name='fullname' />
                      <attribute name='sample_outdooractivities' />
                       <filter type='and'>
                        <condition attribute='sample_outdooractivities' operator='not-contain-values'>
                         <value>2</value>
                        </condition>
                       </filter>
                      </entity>
                     </fetch>";
FetchExpression doesNotLikeHiking = new FetchExpression(fetchXml);

EntityCollection nonHikers = _serviceProxy.RetrieveMultiple(doesNotLikeHiking);

Console.WriteLine("\nContacts who do not like Hiking");
Console.WriteLine("===============================");
foreach (Contact contact in nonHikers.Entities)
{
    string values = (contact["sample_outdooractivities"] == null) ? "null" : contact.FormattedValues["sample_outdooractivities"];
    Console.WriteLine("{0} {1}", contact.FullName, values);
}

    /* OUTPUT
    Contacts who do not like Hiking
    ===============================
    Wayne Yarborough Swimming; Camping
    Randal Maple Fishing
    Barbara Weber Swimming; Fishing; Boating
    Georgette Sullivan Fishing; Hunting; Camping 
    */
```


## <a name="create-a-multi-select-picklist-with-code"></a>複数選択候補リストをコードで作成する

複数選択候補リストを作成する最も簡単な方法は、カスタマイズ ツールの属性エディターを使用することです。 詳細: [フィールドの作成と編集](/dynamics365/customer-engagement/customize/create-edit-fields)

ただし、この種類の属性の作成を自動化する必要がある場合は、複数選択候補リストを作成する組織サービスで、次のように C# コードを使用して、 `contact` エンティティに対する屋外活動の選択を可能にすることができます。 詳細: [属性を作成する](/dynamics365/customer-engagement/developer/org-service/work-attribute-metadata.md#create-attributes)

```csharp
    private const int _languageCode = 1033; //English

    MultiSelectPicklistAttributeMetadata outDoorActivitiesAttribute = new MultiSelectPicklistAttributeMetadata()
    {
    SchemaName = "sample_OutdoorActivities",
    LogicalName = "sample_outdooractivities",
    DisplayName = new Label("Outdoor activities", _languageCode),
    RequiredLevel = new AttributeRequiredLevelManagedProperty(AttributeRequiredLevel.None),
    Description = new Label("Outdoor activities that the contact likes.", _languageCode),
    OptionSet = new OptionSetMetadata()
        {
            IsGlobal = false,
            OptionSetType = OptionSetType.Picklist,
            Options = {
                new OptionMetadata(new Label("Swimming",_languageCode),1),
                new OptionMetadata(new Label("Hiking",_languageCode),2),
                new OptionMetadata(new Label("Mountain Climbing",_languageCode),3),
                new OptionMetadata(new Label("Fishing",_languageCode),4),
                new OptionMetadata(new Label("Hunting",_languageCode),5),
                new OptionMetadata(new Label("Running",_languageCode),6),
                new OptionMetadata(new Label("Boating",_languageCode),7),
                new OptionMetadata(new Label("Skiing",_languageCode),8),
                new OptionMetadata(new Label("Camping",_languageCode),9)}
        }
    };

    CreateAttributeRequest createAttributeRequest = new CreateAttributeRequest
    {
        EntityName = Contact.EntityLogicalName,
        Attribute = outDoorActivitiesAttribute
    };
```

### <a name="see-also"></a>関連項目
[エンティティ属性の概要](/dynamics365/customer-engagement/developer/introduction-entity-attributes)<br />
[Web API を使用してエンティティを作成する](webapi/create-entity-web-api.md)<br />
[Web API を使用したクエリ データ](webapi/query-data-web-api.md)<br />
[属性メタデータに関する作業](/dynamics365/customer-engagement/developer/org-service/work-attribute-metadata)<br />
[サンプル: 属性メタデータに関する作業](/dynamics365/customer-engagement/developer/org-service/sample-work-attribute-metadata)<br />
[組織サービスを使用して遅延バインドと事前バインドのプログラミング クラス](org-service/early-bound-programming.md)
