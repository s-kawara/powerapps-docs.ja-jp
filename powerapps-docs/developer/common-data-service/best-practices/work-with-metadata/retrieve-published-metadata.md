---
title: 公開済みメタデータの取得 | MicrosoftDocs
description: 非公開メタデータを取得すると、要求自体の処理にオーバーヘッドが追加され、処理が遅くなるだけでなく、要求者が予期しないメタデータを返す可能性もあります。
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
# <a name="retrieve-published-metadata"></a>公開済みメタデータの取得

**カテゴリ**: パフォーマンス、使用法

**影響の可能性**: 高い

<a name='symptoms'></a>

## <a name="symptoms"></a>現象

非公開メタデータを取得すると、次のことが発生する可能性があります。

- パフォーマンスの低下
- ユーザーの混乱

<a name='guidance'></a>

## <a name="guidance"></a>ガイダンス

非公開のカスタマイズを取得することは一般的ではなく、そのようなカスタマイズを取得する必要はほとんどありません。

非公開カスタマイズを取得する必要がある例として、カスタマイズ可能なメタデータを編集するアプリケーションを作成する場合が挙げられます。  たとえば、ユーザー定義メタデータのエディターを作成する場合は、それらのアイテムの非公開の定義を取得する必要があります。 開発者の定義した一部の変更が公開されていないときは、アプリケーションで取得して、開発者が最新のカスタマイズを取得していることを確認できる必要があります。 それができない場合、非公開カスタマイズが失われることになります。

ただし、エディターを作成しない場合や、非公開の定義を取得する必要がない場合は、公開済みの定義のみを取得します。 以下の例は、公開済みカスタマイズを取得する方法を示しています。

### <a name="default-behavior"></a>既定の動作

既定では、メタデータを取得すると、公開済みのカスタマイズのみが取得されます

```csharp
public RetrieveAllEntitiesAttributesResponse GetAllEntitiesImplicit(IOrganizationService service)
{
    var request = new RetrieveAllEntitiesRequest();
    request.EntityFilters = EntityFilters.Attributes;

    return service.Execute(request) as RetrieveAllEntitiesAttributesResponse;
}
```

### <a name="explictly-controlling-the-behavior"></a>動作を明示的に制御します

`RetrieveAsIfPublished` プロパティを明示的に設定して、公開済みカスタマイズのみ取得します

```csharp
public RetrieveAllEntitiesAttributesResponse GetAllEntitiesExplicit(IOrganizationService service)
{
    var request = new RetrieveAllEntitiesRequest()
    {
        RetrieveAsIfPublished = false
        EntityFilters = EntityFilters.Attributes
    };

    return service.Execute(request) as RetrieveAllEntitiesAttributesResponse;
}
```

<a name='problem'></a>

## <a name="problematic-patterns"></a>問題となるパターン

以下の操作では、`RetrieveAsIfPublished` パラメーターを介して非公開メタデータを取得できます。

- <xref:Microsoft.Xrm.Sdk.Messages.RetrieveAllEntitiesRequest>
- <xref:Microsoft.Xrm.Sdk.Messages.RetrieveAllOptionSetsRequest>
- <xref:Microsoft.Xrm.Sdk.Messages.RetrieveAttributeRequest>
- <xref:Microsoft.Xrm.Sdk.Messages.RetrieveEntityRequest>
- <xref:Microsoft.Xrm.Sdk.Messages.RetrieveOptionSetRequest>
- <xref:Microsoft.Xrm.Sdk.Messages.RetrieveRelationshipRequest>
- <xref:Microsoft.Xrm.Sdk.Messages.RetrieveEntityKeyRequest>

非公開カスタマイズを取得する例は以下に記載されています。

> [!WARNING]
> これらのシナリオを回避する必要があります。

```csharp
public RetrieveEntityKeyResponse GetEntityKey(IOrganizationService service, string entityName, string keyName)
{
    var request = new RetrieveEntityKeyRequest()
    {
        EntityLogicalName = entityName,
        LogicalName = keyName,
        RetrieveAsIfPublished = true
    };

    return service.Execute(request) as RetrieveEntityKeyResponse;
}

public RetrieveRelationshipResponse GetRelationship(IOrganizationService service, Guid id)
{
    var request = new RetrieveRelationshipRequest()
    {
        MetadataId = id,
        RetrieveAsIfPublished = true
    };

    return service.Execute(request) as RetrieveRelationshipResponse;
}

public RetrieveEntityAttributesResponse GetEntity(IOrganizationService service, Guid id)
{
    var request = new RetrieveEntityRequest()
    {
        MetadataId = id,
        RetrieveAsIfPublished = true,
        EntityFilters = EntityFilters.Attributes
    };

    return service.Execute(request) as RetrieveEntityAttributesResponse;
}
```

## <a name="web-api-functions"></a>Web API 関数

このガイドは、次の Web API 関数にも適用されます:

- <xref href="Microsoft.Dynamics.CRM.RetrieveAllEntities?text=RetrieveAllEntities Function" />
- <xref href="Microsoft.Dynamics.CRM.RetrieveEntity?text=RetrieveEntity Function" />

<a name='additional'></a>

## <a name="additional-information"></a>追加情報

Dynamics 365 サービスでは、公開済みまたは非公開の特定のメタデータを取得できます。 Dynamics CRM 2011 以降、開発者が `RetrieveAsIfPublished` プロパティ値に明示的に`true` を割り当てていない限り、公開済みメタデータは、既定でアプリケーションのメモリ内メタデータ キャッシュから取得されます。

非公開メタデータを取得すると、要求自体の処理にオーバーヘッドが追加され、処理が遅くなるだけでなく、要求者が予期しないメタデータを返す可能性もあります。 たとえば、非公開の optionset メタデータを取得すると、ユーザー インターフェイスに表示されないラベル値が返され、エンドユーザーが混乱する原因となります。

<a name='seealso'></a>

### <a name="see-also"></a>関連項目

<xref:Microsoft.Xrm.Sdk.Messages.RetrieveEntityRequest> <xref href="Microsoft.Xrm.Sdk.Messages.RetrieveEntityRequest.RetrieveAsIfPublished?text=RetrieveAsIfPublished Property" /><br />
[組織サービスを使用したメタデータに関する作業](../../org-service/work-with-metadata.md)<br />
[Web API をメタデータで使用する](../../webapi/use-web-api-metadata.md)<br />
[カスタマイズの公開](/powerapps/developer/model-driven-apps/publish-customizations#retrieving-unpublished-metadata)