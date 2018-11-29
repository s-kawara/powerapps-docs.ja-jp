---
title: PowerApps でエンティティ マッピングおよび属性マッピングのカスタマイズ (アプリ用 Common Data Service) | Microsoft Docs
description: PowerApps で、エンティティの関連付けを持つエンティティ間の属性のマッピングについて学習します。 これにより、他のレコードのコンテキストで作成したレコードの既定値を設定できます。
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: mayadumesh
ms.author: jdaly
manager: kvivek
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="customize-entity-and-attribute-mappings"></a>エンティティ マッピングおよび属性マッピングのカスタマイズ

エンティティの関連付けを持つエンティティ間で属性をマップできます。 これにより、他のレコードのコンテキストで作成したレコードの既定値を設定できます。 属性をマップするには、アプリケーションのカスタマイズ ツールを使用します。[エンティティ フィールドのマップ](../../maker/common-data-service/map-entity-fields.md)を参照してください。

<a name="bkmk_BehaviorintheApplication"></a>

## <a name="behavior-in-the-application"></a>アプリケーションの動作

 アプリ用 Common Data Service (CDS) でのマッピングにより、別のレコードに関連付けられた新しいレコードを作成するときのデータ入力の効率が上がります。 エンティティに他のエンティティとのエンティティ関連付けがある場合、リボンの**関連項目の作成**タブを使用して新しい関連エンティティ レコードを作成できます。 この方法で新しいレコードを作成すると、主エンティティ レコードからマップされたデータが、新しい関連エンティティ レコードのフォームにコピーされます。 エンティティ属性をマップすることにより、コピーされるデータの種類は、2 つのエンティティ間の関連付けに新しいマッピングを追加して制御します。 主エンティティの関連ビューから作成する以外の方法でレコードを作成した場合、データはマップされません。  

 たとえば、取引先企業の住所フィールドと取引先担当者の住所フィールドの間にマッピングを設定して、 ユーザーが特定の取引先企業と関連付けられた取引先担当者を追加すると、取引先担当者の住所フィールドに自動的に入力されるようにすることができます。  

 1 つの属性を複数のターゲット属性にマップできます。 たとえば、取引先の住所情報を、受注の請求先住所と送付先住所の両方にマップできます。  

 マッピングは、新しい関連レコードが作成される前に適用されます。 ユーザーはレコードを保存する前にデータを変更することができます。 保存後に主レコードのデータに加えられた変更は、関連レコードに適用されません。  

<a name="bkmk_UsingEntityandAttributeMappingData"></a>

## <a name="using-entity-and-attribute-mapping-data"></a>エンティティおよび属性のマッピング データの使用

### <a name="using-web-api"></a>Web API の使用

Web API での作業時は、<xref href="Microsoft.Dynamics.CRM.InitializeFrom?text=InitializeFrom Function" /> を使用して、エンティティ間にマッピングが存在する既存のレコードのコンテキスト内にレコードを新規作成することができます。 

InitializeFrom 要求から受け取った反応は、ソース エンティティとターゲット エンティティ間でマッピングされた属性値と親レコードの GUID で構成されます。 エンティティの関連付けを持つエンティティ間の属性マッピングは、違うエンティティ セットでは異なりカスタマイズ可能であるため、InitializeFrom 関数要求からの応答は違うエンティティおよび組織では異なる可能性があります。 この応答が新しいレコードの作成要求のボディに渡されるとき、これらの属性値は新しいレコードで複製されます。 カスタム マッピングした属性の値も、プロセス中に新しいレコード内のセットを取得します。

> [!NOTE] 
> 2 つのエンティティがマッピング可能か判断するには、次の Web API 要求を使用します。<br/>`GET [Organization URI]/api/data/v9.0/entitymaps?$select=sourceentityname,targetentityname&$orderby=sourceentityname`

詳細については、[別のエンティティから新しいエンティティを作成する](webapi/create-entity-web-api.md#create-a-new-entity-from-another-entity) を参照してください。

### <a name="using-organization-service"></a>組織サービスの使用

 エンティティ間のマッピングが存在する既存のレコードのコンテキストで新しいレコードを作成する場合、<xref:Microsoft.Crm.Sdk.Messages.InitializeFromRequest> メッセージを使用して、マッピングに指定された値を含む新しいレコードを定義できます。 <xref:Microsoft.Xrm.Sdk.IOrganizationService> が使用可能になります。
 レコードを保存する <xref:Microsoft.Xrm.Sdk.IOrganizationService.Create*> メソッド。 この方法で、ユーザーが定義したあらゆるマッピングが適用されます。  

 エンティティの関連付けを作成すると、有効なエンティティ マップが作成されます。 エンティティ マップによって指定されたエンティティ ペアの属性マップを取得するには、`entity_map_attribute_maps` エンティティ関連付けを使用します。  
 属性マップのレコードを作成または更新できます。 その際、属性マップに関する以下の要件を満たす必要があります。  
- <xref:Microsoft.Xrm.Sdk.Metadata.AttributeMetadata> の型が一致している必要があります。
- ターゲット フィールドの長さはソース フィールドの長さ以上にする必要があります。
- 形式が一致している必要があります。
- ターゲット フィールドが別のマッピングに使用されていない必要があります。
- ソース フィールドがエンティティ フォーム上で表示可能である必要があります。
- ターゲット フィールドが、ユーザーがデータを入力可能なフィールドである必要があります。
- アドレス ID の値はマップできません。
- <xref:Microsoft.Xrm.Sdk.Metadata.AttributeMetadata>.<xref:Microsoft.Xrm.Sdk.Metadata.AttributeMetadata.AttributeType> が <xref:Microsoft.Xrm.Sdk.Metadata.AttributeTypeCode>.PartyList である PartyList 属性はマッピングすることができません。

<a name="bkmk_Automapping"></a>

## <a name="auto-mapping-attributes-between-entities"></a>エンティティ間の属性の自動マッピング

 マッピングをサポートするエンティティの関連付けに対して、エンティティ間の属性マッピングを編集できます。 

 各属性マップを手動で作成する以外に、`AutoMapEntity` メッセージ (<xref href="Microsoft.Dynamics.CRM.AutoMapEntity?text=AutoMapEntity Action" /> または <xref:Microsoft.Crm.Sdk.Messages.AutoMapEntityRequest> クラス) を使用して新しい属性マッピング セットを生成することもできます。 このメッセージは、ツール バーの**その他の操作**メニューの**マッピングの生成**の操作を実行します ([フィールド マッピングを自動的に生成する](../../maker/common-data-service/map-entity-fields.md#automatically-generate-field-mappings)を参照して下さい) 。 このメッセージにより、同じ属性名と種類を持つ 2 つの関連するエンティティ間の属性すべてがマップされます。 このメッセージでは、すべての属性マッピングを手動で追加する必要がないため、生産性が向上します。 一連の類似したマッピングを生成することで、要件に合わせて個々のマッピングを追加または削除するための手動による作業を削減できます。 

> [!NOTE]
> この方法でマッピングを自動生成することにより、以前に定義した、不要なマッピングが含まれている可能性がある属性マッピングは削除されます。  

<a name="BKMK_mapping"></a>

## <a name="retrieve-the-entity-and-attribute-mappings"></a>エンティティ マッピングおよび属性マッピングの取得

 作成されているマッピングを確認する簡単な方法は、次の FetchXML クエリを使用することです。 このクエリの実行方法の詳細については、[FetchXML でデータをクエリする](use-fetchxml-construct-query.md)を参照してください。

```xml

<fetch version='1.0' mapping='logical' distinct='false'>
   <entity name='entitymap'>
      <attribute name='sourceentityname'/>
      <attribute name='targetentityname'/>
      <link-entity name='attributemap' alias='attributemap' to='entitymapid' from='entitymapid' link-type='inner'>
         <attribute name='sourceattributename'/>
         <attribute name='targetattributename'/>
      </link-entity>
   </entity>
 </fetch>
```

### <a name="see-also"></a>関連項目

 [エンティティ フィールドのマップ](../../maker/common-data-service/map-entity-fields.md)