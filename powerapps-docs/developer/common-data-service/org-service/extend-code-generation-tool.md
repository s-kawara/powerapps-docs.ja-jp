---
title: コード生成ツールの拡張機能を作成する (Common Data Service) | Microsoft Docs
description: SDK ダウンロード パッケージには、グローバル オプション セット、候補リスト、状態、ステータスの値などすべてのオプション セット値の列挙体を生成するために使用できる、CrmSvcUtil コード生成ツールへの拡張が含まれています。
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: brandonsimons
ms.author: jdaly
manager: ryjones
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="create-extensions-for-the-code-generation-tool"></a>コード生成ツール用の拡張機能の作成

追加のコマンドライン パラメーターとパラメーター値を指定することで、コード生成ツールの機能を拡張できます。 パラメーターを指定するには、コマンド ラインに /\<*parametername*>:\<*class name*>,\<*assembly name*> を追加します。 アセンブリ名に .dll 拡張子を含めないことに注意してください。 または、これらに相当する値を構成ファイル内に “<add key=”\<*parametername*>” value=”\<*class name*>,\<*assembly name*>” />” 形式で追加することもできます。  

使用できるパラメーターを次の表に示します。  

|パラメーター名|インターフェイス名|内容|  
|--------------------|--------------------|-----------------|  
|/codecustomization|ICustomizeCodeDomService|CodeDOM の生成が完成した後で呼び出されます (`ICodeGenerationService` の既定のインスタンスを使用すると仮定します)。 候補リスト内の定数など、追加のクラスを生成するには便利です。|  
|/codewriterfilter|ICodeWriterFilterService|特定のオブジェクトまたはプロパティを生成するかどうかを判断するために CodeDOM の生成中に呼び出されます (`ICodeGenerationService` の既定のインスタンスを使用すると仮定します)。|  
|/codewritermessagefilter|ICodeWriterMessageFilterService|特定のメッセージを生成するかどうかを判断するために CodeDOM の生成中に呼び出されます (`ICodeGenerationService` の既定のインスタンスを使用すると仮定します)。 Microsoft.Crm.Sdk.Proxy.dll および Microsoft.Xrm.Sdk.dll で既に生成済みであるため、これは要求/応答で使用しないでください。|  
|/metadataproviderservice|IMetadataProviderService|サーバーからメタデータを取得するために呼び出されます。 生成プロセス中に複数回呼び出されることがあるため、データはキャッシュに保存する必要があります。|  
|/codegenerationservice|ICodeGenerationService|CodeDOM 生成の中心的な実装部分。 これを変更した場合、他の拡張機能が説明どおりに動作しなくなる可能性があります。|  
|/namingservice|INamingService|オブジェクトの名前を確認するために CodeDOM 生成中に呼び出されます (既定の実装を使用すると仮定します)。|

これらのインターフェイスの実装には、次のいずれかのコンストラクターが含まれる必要があります。

`MyNamingService`()<br />
`MyNamingService`(`INamingService``defaultService`)<br />
`MyNamingService`(`IDictionary`<`string`, `string`> `parameters`)<br />
`MyNamingService`(`INamingService``defaultService`, `IDictionary`<`string`, `string`> `parameters`)

`Microsoft.Crm.Services.Utility` 名前空間は、CrmSvcUtil.exe で定義されています。 Visual Studio コード生成ツール拡張機能プロジェクトに CrmSvcUtil.exe への参照を追加します。

<a name="Generate_Enums"></a>

## <a name="sample-extension-to-generate-enumerations-for-option-sets"></a>オプション セットの列挙を生成するためのサンプル拡張機能

次のコード例は、拡張機能の作成方法を示しています。  

```csharp
using System;

using Microsoft.Crm.Services.Utility;
using Microsoft.Xrm.Sdk.Metadata;

/// <summary>
/// Sample extension for the CrmSvcUtil.exe tool that generates early-bound
/// classes for custom entities.
/// </summary>
public sealed class BasicFilteringService : ICodeWriterFilterService
{
    public BasicFilteringService(ICodeWriterFilterService defaultService)
    {
        this.DefaultService = defaultService;
    }

    private ICodeWriterFilterService DefaultService { get; set; }

    bool ICodeWriterFilterService.GenerateAttribute(AttributeMetadata attributeMetadata, IServiceProvider services)
    {
        return this.DefaultService.GenerateAttribute(attributeMetadata, services);
    }

    bool ICodeWriterFilterService.GenerateEntity(EntityMetadata entityMetadata, IServiceProvider services)
    {
        if (!entityMetadata.IsCustomEntity.GetValueOrDefault()) { return false; }
        return this.DefaultService.GenerateEntity(entityMetadata, services);
    }

    bool ICodeWriterFilterService.GenerateOption(OptionMetadata optionMetadata, IServiceProvider services)
    {
        return this.DefaultService.GenerateOption(optionMetadata, services);
    }

    bool ICodeWriterFilterService.GenerateOptionSet(OptionSetMetadataBase optionSetMetadata, IServiceProvider services)
    {
        return this.DefaultService.GenerateOptionSet(optionSetMetadata, services);
    }

    bool ICodeWriterFilterService.GenerateRelationship(RelationshipMetadataBase relationshipMetadata, EntityMetadata otherEntityMetadata,
    IServiceProvider services)
    {
        return this.DefaultService.GenerateRelationship(relationshipMetadata, otherEntityMetadata, services);
    }

    bool ICodeWriterFilterService.GenerateServiceContext(IServiceProvider services)
    {
        return this.DefaultService.GenerateServiceContext(services);
    }
}

```

[CrmSvcUtilExtensions](https://code.msdn.microsoft.com/Create-extensions-for-the-b8b24d1d) および [GeneratePickListEnums](https://code.msdn.microsoft.com/Create-extensions-for-the-3dd56a27) サンプルをダウンロードします。 

**GeneratePicklistEnums** サンプル拡張機能は、すべてのオプション セット、状態コード、およびステータス コードの列挙を含むソース コード ファイルを出力します。 これらの列挙を使用する方法の例については、`SampleCode\CS\QuickStart` サンプルを参照してください。  

これには、すべての標準の値で生成された列挙体を格納するヘルパー コード ファイルも含まれています。 これらの列挙体をコード内で使用するには、`SampleCode\CS\HelperCode\OptionSets.cs` ファイルまたは `SampleCode\VB\HelperCode\OptionSets.vb` ファイルをプロジェクトに追加します。

各列挙体を使用して、プロパティの値をテストまたは設定することができます。 通常、このプロパティはエンティティ属性ですが、他のプロパティに使用されるものもいくつかあります。

### <a name="usage-example"></a>使用例

次の例は、これらの列挙体の 1 つを使用して、`Account` エンティティの値を設定する方法を示しています。

```csharp
// Instantiate an account object. Note the use of the option set enumerations defined
// in OptionSets.cs.
Account account = new Account { Name = "Fourth Coffee" };
account.AccountCategoryCode = new OptionSetValue((int)AccountAccountCategoryCode.PreferredCustomer);
account.CustomerTypeCode = new OptionSetValue((int)AccountCustomerTypeCode.Investor);

// Create an account record named Fourth Coffee.
// Save the record reference so we can delete it during cleanup later.
Guid accountId = service.Create(account);
```

### <a name="see-also"></a>関連項目

 [コード生成ツール (CrmSvcUtil.exe) を使用して事前バインド型エンティティ クラスを作成する](/dynamics365/customer-engagement/developer/create-early-bound-entity-classes-code-generation-tool)<br />
 [作成、更新、および削除の事前バインド エンティティ クラスの使用](/dynamics365/customer-engagement/developer/use-entity-class-create-update-delete)<br />
 [トラブルシューティングのヒント](/dynamics365/customer-engagement/developer/troubleshooting-tips)<br />
 [Web サービスを使用した単純なプログラムの実行](/dynamics365/customer-engagement/developer/simple-program-web-services)
