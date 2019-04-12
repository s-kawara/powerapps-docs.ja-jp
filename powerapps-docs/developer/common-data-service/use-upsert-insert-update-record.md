---
title: Upsert を使用したレコードの挿入または更新 (Common Data Service) | Microsoft Docs
description: UpsertRequest (更新または挿入) メッセージのヘルプは、Dynamics 365 にレコードが存在するかどうかわからない場合にさまざまなデータ統合シナリオを簡略化するのに役立ちます。 このような場合、UpdateRequest または CreateRequest 操作を呼び出す必要があるかどうかが分かりません。 この結果、適切な操作を実行する前に、そのレコードが存在するかどうかを決定するために、最初にそのレコードをクエリすることになります。 UpsertRequest メッセージはそのような問題の解決に役立ちます
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
# <a name="use-upsert-to-insert-or-update-a-record"></a>Upsert を使用してレコードを挿入または更新

<xref:Microsoft.Xrm.Sdk.Messages.UpsertRequest> メッセージを使用して、データ統合のシナリオに含まれる複雑さを減らすことができます。 データを外部システムから Common Data Service の Customer Engagement に読み込むとき、大量データの統合の場合など、レコードが Common Data Service に既に存在するかが分からない場合があります。 このような場合、<xref:Microsoft.Xrm.Sdk.Messages.UpdateRequest> または <xref:Microsoft.Xrm.Sdk.Messages.CreateRequest> 操作を呼び出す必要があるかどうかが分かりません。 この結果、適切な操作を実行する前に、そのレコードが存在するかどうかを決定するために、最初にそのレコードをクエリすることになります。 現在は、新しい <xref:Microsoft.Xrm.Sdk.Messages.UpsertRequest> (更新または送信) メッセージを使用して、この複雑さを減らしてデータを Common Data Service により効率よく読み込むことができます。  
  
<a name="BKMK_UsingUpsert"></a>   
## <a name="using-upsert"></a>Upsert の使用  
 レコードが存在するかどうかが確かでない場合にのみ、<xref:Microsoft.Xrm.Sdk.Messages.UpsertRequest> を使用することをお勧めします。 つまり、<xref:Microsoft.Xrm.Sdk.Messages.CreateRequest> または <xref:Microsoft.Xrm.Sdk.Messages.UpdateRequest> 操作を呼び出す必要があるかどうか確かでない場合です。 <xref:Microsoft.Xrm.Sdk.Messages.UpsertRequest> の使用は、<xref:Microsoft.Xrm.Sdk.Messages.CreateRequest> の使用に比べて、パフォーマンスの低下があります。 レコードが存在しないことが確実な場合は、<xref:Microsoft.Xrm.Sdk.Messages.CreateRequest> を使用します。  
  
 <xref:Microsoft.Xrm.Sdk.Messages.UpsertRequest> には、<xref:Microsoft.Xrm.Sdk.Messages.UpsertRequest.Target> という名前のプロパティが含まれています。 このプロパティには、<xref:Microsoft.Xrm.Sdk.Messages.UpdateRequest> または <xref:Microsoft.Xrm.Sdk.Messages.CreateRequest> 操作で使用されるエンティティ定義が含まれています。 これには、また、レコードが存在しない場合にそのレコードを作成できるように、<xref:Microsoft.Xrm.Sdk.Messages.CreateRequest> によって要求される、対象のエンティティの種類に対するすべての属性も含まれています。  
  
 <xref:Microsoft.Xrm.Sdk.Messages.UpsertResponse.RecordCreated> を確認して、レコードが作成されたかどうか判断することができます。 <xref:Microsoft.Xrm.Sdk.Messages.UpsertResponse.RecordCreated> は、レコードが存在せず作成された場合に true になります。 レコードが既に存在し、更新された場合は false です。 <xref:Microsoft.Xrm.Sdk.Messages.UpsertResponse.Target> は、存在することが判明したレコード、または作成されたレコードに対する `EntityReference` となります。  
  
 <xref:Microsoft.Xrm.Sdk.Messages.UpsertRequest> の動作の詳細については、次のセクションを参照してください。  
  
<a name="BKMK_upsert"></a>   
## <a name="understanding-the-upsert-process"></a>Upsert プロセスの詳細  
 次の手順では、<xref:Microsoft.Xrm.Sdk.Messages.UpsertRequest> を受け取ったときの、処理ロジックについて説明します。  
  
1. 作成または挿入の操作ために十分なデータう付けて、<xref:Microsoft.Xrm.Sdk.Messages.UpsertRequest> を送信します。  
  
2. Common Data Service は、ターゲット エンティティの対象となるレコードを検索します。  
  
3. レコードが存在する場合は、次の手順を実行します。  
  
   1.  見つかったレコードの ID で、ターゲット エンティティの ID プロパティを設定します。  
  
   2.  [更新] を呼び出します。  
  
   3.  <xref:Microsoft.Xrm.Sdk.Messages.UpsertResponse.RecordCreated> を `false` に設定します。  
  
   4.  更新のターゲット エンティティから <xref:Microsoft.Xrm.Sdk.EntityReference> を <xref:Microsoft.Xrm.Sdk.Messages.UpsertResponse.Target> の値として作成します。  
  
   5.  <xref:Microsoft.Xrm.Sdk.Messages.UpsertResponse> を返します。  
  
4. レコードが存在しない場合は、次の手順を実行します。  
  
   1.  代替キーの値をターゲット エンティティの属性にコピーします。  
  
   2.  `Create` を呼び出します。  
  
   3.  <xref:Microsoft.Xrm.Sdk.Messages.UpsertResponse.RecordCreated> を `true` に設定します。  
  
   4.  ターゲット エンティティの種類と `Create` 要求の結果得られた ID から <xref:Microsoft.Xrm.Sdk.EntityReference> を、<xref:Microsoft.Xrm.Sdk.Messages.UpsertResponse.Target> の値として作成します。  
  
   5.  <xref:Microsoft.Xrm.Sdk.Messages.UpsertResponse> を返します。  
  
   次の図は、<xref:Microsoft.Xrm.Sdk.Messages.UpsertRequest> を受け取ったときに展開されるプロセスを示しています。  
  
   ![upsert プロセス フロー](media/upsert-flowchart-dynamics-crm-2015.png "upsert プロセス フロー")  
  
<a name="BKMK_SampleCode"></a>   
## <a name="sample-code"></a>サンプル コード  
 [Upsert を使用してレコードを挿入または更新](http://go.microsoft.com/fwlink/p/?LinkId=532924) のサンプル ファイル [ProductUpsertSample.cs](https://code.msdn.microsoft.com/Insert-or-update-a-record-aa160870/sourcecode?fileId=136218&pathId=1243320355) には `ProcessUpsert` メソッドが含まれています。このメソッドは、`UpsertRequest` メッセージを XML ファイルのコンテンツに適用して、新しいレコードを作成するか、または既存のレコードを更新します。  
  
```csharp
public void ProcessUpsert(String Filename)
{
    Console.WriteLine("Executing upsert operation.....");
    XmlTextReader tr = new XmlTextReader(Filename);
    XmlDocument xdoc = new XmlDocument();
    xdoc.Load(tr);
    XmlNodeList xnlNodes = xdoc.DocumentElement.SelectNodes("/products/product");

    foreach (XmlNode xndNode in xnlNodes)
    {
        String productCode = xndNode.SelectSingleNode("Code").InnerText;
        String productName = xndNode.SelectSingleNode("Name").InnerText;
        String productCategory = xndNode.SelectSingleNode("Category").InnerText;
        String productMake = xndNode.SelectSingleNode("Make").InnerText;

        //use alternate key for product
        Entity productToCreate = new Entity("sample_product", "sample_productcode", productCode);

        productToCreate["sample_name"] = productName;
        productToCreate["sample_category"] = productCategory;
        productToCreate["sample_make"] = productMake;
        UpsertRequest request = new UpsertRequest()
        {
            Target = productToCreate
        };

        try
        {
            // Execute UpsertRequest and obtain UpsertResponse. 
            UpsertResponse response = (UpsertResponse)_serviceProxy.Execute(request);
            if (response.RecordCreated)
                Console.WriteLine("New record {0} is created!", productName);
            else
                Console.WriteLine("Existing record {0} is updated!", productName);
        }

        // Catch any service fault exceptions that Microsoft Dynamics CRM throws.
        catch (FaultException<Microsoft.Xrm.Sdk.OrganizationServiceFault>)
        {
            throw;
        }

    }
    // Prompts to view the sample_product entity records.
    // If you choose "y", IE will be launched to display the new or updated records.
    if (PromptForView())
    {
        ViewEntityListInBrowser();
    }

}
```
  
### <a name="see-also"></a>関連項目  
 [変更の追跡を使用してデータを外部システムに同期](use-change-tracking-synchronize-data-external-systems.md)   
 [エンティティの代替キーの定義](define-alternate-keys-entity.md)   
 [代替キーの使用](use-alternate-key-create-record.md)
