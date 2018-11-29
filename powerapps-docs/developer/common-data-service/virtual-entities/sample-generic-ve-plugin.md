---
title: 'サンプル: 汎用仮想エンティティ データ プロバイダー プラグイン (Common Data Service for Apps) | Microsoft Docs'
description: サンプルでは、汎用のカスタム Dynamics 365 仮想エンティティ プラグインの実行方法を説明しています。
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: crm-online
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: samples
applies_to:
  - Dynamics 365 (online)
ms.assetid: d329dade-16c5-46e9-8dec-4b8efb996d24
author: mayadumesh
ms.author: jdaly
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---

# <a name="sample-generic-virtual-entity-data-provider-plug-in"></a>サンプル: 汎用仮想エンティティ データ プロバイダー プラグイン

## <a name="demonstrates"></a>説明

このサンプルは、[Dropbox](https://www.dropbox.com/) ファイル共有サービスのための汎用の CDS for Apps 仮想エンティティ データ プロバイダー プラグインである **DropboxRetrieveMultiplePlugin** の最小の実装を示します。 これはカスタム ビジター クラス **DropBoxExpressionVisitor** の作成により <xref:Microsoft.Xrm.Sdk.Query.QueryExpression> を変換する「ベア メタル」アプローチを使用します。 <xref:Microsoft.Xrm.Sdk.EntityCollection> として検索条件を満たすファイルのコレクションを返します。 

## <a name="getting-started"></a>作業の開始

このサンプルを作成するには、まず [Dropbox.Api](https://www.nuget.org/packages/Dropbox.Api/) および [Microsoft.CrmSdk.Data](https://www.nuget.org/packages/Microsoft.CrmSdk.Data/) NuGet パッケージをユーザーのソリューションにインストールする必要があります。  また、**DropboxClient** のインスタンスを作成するときには、DropBox アカウントおよび実際のアクセス トークンが必要です。

以下の using ステートメントをコードに追加する必要があります。

```csharp
using Microsoft.Xrm.Sdk;
using Microsoft.Xrm.Sdk.Query;
using Dropbox.Api;
using Dropbox.Api.Files;
```

## <a name="sample-code"></a>サンプル コード  

```csharp  

public class DropBoxExpressionVisitor : QueryExpressionVisitorBase
{
    public string SearchKeyWords { get; private set; }

    public override QueryExpression Visit(QueryExpression query)
    {
        // Very simple visitor that extracts search keywords
        var filter = query.Criteria;
        if (filter.Conditions.Count > 0)
        {
            foreach (ConditionExpression condition in filter.Conditions)
            {
                if (condition.Operator == ConditionOperator.Like && condition.Values.Count > 0)
                {
                    string exprVal = (string)condition.Values[0];

                    if (exprVal.Length > 2)
                    {
                        this.SearchKeyWords += " " + exprVal.Substring(1, exprVal.Length - 2);
                    }
                }
            }
            return query;
        }
    }
}

public class DropboxRetrieveMultiplePlugin : IPlugin
{
    public void Execute(IServiceProvider serviceProvider)
    {
        var context = (IPluginExecutionContext)serviceProvider.GetService(typeof(IPluginExecutionContext));
        var qe = (QueryExpression)context.InputParameters["Query"];
        if (qe != null)
        {
            var visitor = new DropBoxExpressionVisitor();
            qe.Accept(visitor);
            using (var dbx = new DropboxClient(AccessToken))
            {
                if (visitor.SearchKeyWords != string.Empty)
                {
                    var searchCriteria = new SearchArg(string.Empty, visitor.SearchKeyWords);
                    var task = Task.Run(() => this.SearchFile(dbx, searchCriteria));
                    context.OutputParameters["BusinessEntityCollection"] = task.Result;
                }
            }
        }
    }

    public async Task<EntityCollection> SearchFile(DropboxClient dbx, SearchArg arg)
    {
        EntityCollection ec = new EntityCollection();
        var list = await dbx.Files.SearchAsync(arg);
        foreach (var item in list.Matches)
        {
            if (item.Metadata.IsFile)
            {
                Entity e = new Entity("new_dropbox");
                e.Attributes.Add("new_dropboxid", Guid.NewGuid());
                e.Attributes.Add("new_filename", item.Metadata.AsFile.Name);
                e.Attributes.Add("new_filesize", item.Metadata.AsFile.Size);
                e.Attributes.Add("new_modifiedon", item.Metadata.AsFile.ServerModified);
                ec.Entities.Add(e);
            }
        }
        return ec;
    }
}

``` 

### <a name="see-also"></a>関連項目

[仮想エンティティに関する入門情報](get-started-ve.md)<br />
[仮想エンティティの API に関する考慮事項](api-considerations-ve.md)<br />
[カスタム仮想エンティティ データ プロバイダー](custom-ve-data-providers.md)