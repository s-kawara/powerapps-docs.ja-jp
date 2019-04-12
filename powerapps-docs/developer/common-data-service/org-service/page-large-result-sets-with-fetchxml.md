---
title: FetchXML による大量の結果セットのページング (Common Data Service) | Microsoft Docs
description: ページング Cookie を使用することで、FetchXML クエリの結果をページングする方法を説明します。
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
# <a name="page-large-result-sets-with-fetchxml"></a>FetchXML による大量の結果セットのページング

ページング Cookie を使用することで、FetchXML クエリの結果をページングできます。 ページング Cookie は、アプリケーション内で大きなデータセットのページングを高速に実行するためのパフォーマンス機能です。 一連のレコードにクエリを実行すると、その結果にページング Cookie の値が含まれます。 より良いパフォーマンスを得ることを目的として、次の一連のレコードを取得するときにその値を渡すことができます。  
  
 FetchXML と <xref:Microsoft.Xrm.Sdk.Query.QueryExpression> では、ページング Cookie の形式が異なります。 <xref:Microsoft.Crm.Sdk.Messages.FetchXmlToQueryExpressionRequest> メッセージまたは<xref:Microsoft.Crm.Sdk.Messages.QueryExpressionToFetchXmlRequest> メッセージを使用して、クエリ形式を別の形式に変換すると、ページング Cookie の値は無視されます。 また、連続していないページを要求した場合も、ページング Cookie の値は無視されます。  
  
 ページング Cookie を FetchXML で使用するときは、正しいエンコードを使用していることを確認してください。 FetchXML でページング Cookie を使用するときの正しいエンコードの例を次に示します。  
  
```csharp  
strQueryXML = @"  
<fetch mapping='logical' paging-cookie='&lt;cookie page=&quot;1&quot;&gt;&lt;accountid last=&quot;{E062B974-7F8D-DC11-9048-0003FF27AC3B}&quot; first=&quot;{60B934EF-798D-DC11-9048-0003FF27AC3B}&quot;/&gt;&lt;/cookie&gt;' page='2' count='2'>  
 <entity name='account'>  
  <all-attributes/>  
 </entity>  
</fetch>";  
```  
  
## <a name="fetchxml-and-the-paging-cookie-example"></a>FetchXML とページング Cookie の例  
 次の例は、ページング Cookie を FetchXML クエリで使用する方法を示しています。 サンプル コード全体は、「[サンプル: ページング Cookie を使用した FetchXML の使用](samples/use-fetchxml-paging-cookie.md)」を参照してください。  
  
```csharp
// Define the fetch attributes.
// Set the number of records per page to retrieve.
int fetchCount = 3;
// Initialize the page number.
int pageNumber = 1;
// Initialize the number of records.
int recordCount = 0;
// Specify the current paging cookie. For retrieving the first page, 
// pagingCookie should be null.
string pagingCookie = null;

// Create the FetchXml string for retrieving all child accounts to a parent account.
// This fetch query is using 1 placeholder to specify the parent account id 
// for filtering out required accounts. Filter query is optional.
// Fetch query also includes optional order criteria that, in this case, is used 
// to order the results in ascending order on the name data column.
string fetchXml = string.Format(@"<fetch version='1.0' 
                                mapping='logical' 
                                output-format='xml-platform'>
                                <entity name='account'>
                                    <attribute name='name' />
                                    <attribute name='emailaddress1' />
                                    <order attribute='name' descending='false'/>
                                    <filter type='and'>
                            <condition attribute='parentaccountid' 
                                            operator='eq' value='{0}' uiname='' uitype='' />
                                    </filter>
                                </entity>
                            </fetch>",
                                _parentAccountId);

Console.WriteLine("Retrieving data in pages\n"); 
Console.WriteLine("#\tAccount Name\t\t\tEmail Address");

while (true)
{
    // Build fetchXml string with the placeholders.
    string xml = CreateXml(fetchXml, pagingCookie, pageNumber, fetchCount);

    // Excute the fetch query and get the xml result.
    RetrieveMultipleRequest fetchRequest1 = new RetrieveMultipleRequest
    {
        Query = new FetchExpression(xml)
    };

    EntityCollection returnCollection = ((RetrieveMultipleResponse)_service.Execute(fetchRequest1)).EntityCollection;
    
    foreach (var c in returnCollection.Entities)
    {
        System.Console.WriteLine("{0}.\t{1}\t\t{2}", ++recordCount, c.Attributes["name"], c.Attributes["emailaddress1"] );
    }                        
    
    // Check for morerecords, if it returns 1.
    if (returnCollection.MoreRecords)
    {
        Console.WriteLine("\n****************\nPage number {0}\n****************", pageNumber);
        Console.WriteLine("#\tAccount Name\t\t\tEmail Address");
        
        // Increment the page number to retrieve the next page.
        pageNumber++;

        // Set the paging cookie to the paging cookie returned from current results.                            
        pagingCookie = returnCollection.PagingCookie;
    }
    else
    {
        // If no more records in the result nodes, exit the loop.
        break;
    }
}
```
  
### <a name="see-also"></a>関連項目  
 [サンプル: ページング Cookie を使用した FetchXML の使用](samples/use-fetchxml-paging-cookie.md)   
 [FetchXML を使用したクエリの構築](/dynamics365/customer-engagement/developer/org-service/build-queries-fetchxml)   
 [FetchXML の会計日クエリ演算子および older than 日付/時刻クエリ演算子](../use-fetchxml-fiscal-date-older-datetime-query-operators.md)   
 [FetchXML の使用](../use-fetchxml-construct-query.md)   
 [QueryExpression を使用して大きな結果セットをページングする](page-large-result-sets-with-queryexpression.md)
