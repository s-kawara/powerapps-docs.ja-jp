---
title: 'サンプル: Web リソースとしてファイルをインポート (モデル駆動型アプリ) | MicrosoftDocs'
description: このサンプルは、Web リソースとしてのファイルのインポートの、簡略化された例を示します。
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: KumarVivek
ms.author: kvivek
manager: shilpas
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="sample-import-files-as-web-resources"></a>サンプル: Web リソースとしてファイルをインポート

Web リソースとして使用する大量のファイルを開発する場合は、アプリケーションを通じてそれらを手動で追加する作業を削減できます。 多くの Web リソースは、モデル駆動型アプリの外部で開発およびテストし、その後インポートできます。  
  
 このサンプルでは、このプロセスを簡略化した例を提供します。  
 
 サンプルのダウンロード: [Web リソースとしてファイルをインポート](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/orgsvc/C%23/ImportWebResources)。 

## <a name="prerequisites"></a>前提条件
[!INCLUDE[sdk-prerequisite](../../includes/sdk-prerequisite.md)]
  
## <a name="requirements"></a>要件  


<!-- TODO: This should be written so that the connection helper code is not required. [!INCLUDE[sdk_SeeConnectionHelper](../../includes/sdk-seeconnectionhelper.md)] -->
  
 SDK ダウンロード パッケージに含まれているサンプル コードには、このサンプルに必要な次のファイルが含まれています。  
  
 **ImportJob.xml**  
 このファイルは、作成される Web リソース レコードに関するデータを提供します。 各ファイルには、次のデータが含まれます。  
  
- **path**: FilesToImport フォルダーからの各ファイルへのパス。  
  
- **displayName:** Web リソースの表示名。  
  
- **description:** 各ファイルの機能の説明。  
  
- **name:** Web リソースに使用される名前。  
  
  > [!NOTE]
  > - これらの各名前は、アンダースコア文字で始まります。 Web リソースの作成時に、ソリューション発行者のカスタマイズの接頭辞が名前の先頭に追加されます。 このサンプルでは、特定のカスタマイズの接頭辞をハード コーディングする代わりに、組織に既に存在する発行者レコードの現在のカスタマイズの接頭辞を検出します。  
  >   - これらの各ファイルはモデル駆動型アプリの外部で開発され、相対パスに依存して相互にアクセスするため、名前には、仮想フォルダー構造を作成するための円記号 "\" が含まれます。このため、相対リンクはモデル駆動型アプリでも機能します。  
  
- **type**: 「[Web リソースの種類](web-resources.md#BKMK_WebResourceTypes)」に記載されている整数値を使用して、作成する Web リソースの種類を指定します。
  
  **FilesToImport/ShowData.htm**  
  この HTML Web リソースは、次の表を表示するために他の各ファイルを必要とします。  
  
|||  
|-|-|  
|**名**|**姓**|  
|Apurva|Dalia|  
|Ofer|Daliot|  
|Jim|Daly|  
|Ryan|Danner|  
|Mike|Danseglio|  
|Alex|Darrow|  
  
 **FilesToImport/CSS/Styles.css**  
 このファイルは、ShowData.htm で使用される CSS スタイルを提供します。  
  
 **FilesToImport/Data/Data.xml**  
 このファイルには、表に表示される名前の一覧が含まれます。  
  
 **FilesToImport/Script/Script.js**  
 このファイルには、Data.xml ファイルと Transform.xslt ファイルの相対的な場所に関する情報を格納する JScript ライブラリが含まれます。 データを変換して ShowData.htm ページに追加する `showData` 関数も含まれます。  
  
 **FilesToImport/XSL/Transform.xslt**  
 このファイルには、データが HTML テーブルに変換される方法の XSL 定義が含まれます。  
  
## <a name="demonstrates"></a>説明  
  
### <a name="creating-web-resources-in-the-context-of-a-solution"></a>ソリューションのコンテキストでの Web リソースの作成  
 Web リソースは組織所有のレコードであるため、<xref:Microsoft.Xrm.Sdk.IOrganizationService>.<xref:Microsoft.Xrm.Sdk.IOrganizationService.Create*> メソッドを使用するか、<xref:Microsoft.Xrm.Sdk.Messages.CreateRequest> メッセージと <xref:Microsoft.Xrm.Sdk.IOrganizationService>.<xref:Microsoft.Xrm.Sdk.IOrganizationService.Execute*> メソッドを使用して作成することができます。 このサンプルでは、`SolutionUniqueName` オプション パラメーターを使用して Web リソースを作成時に特定のソリューションに関連付ける方法を示します。 これには、<xref:Microsoft.Xrm.Sdk.Messages.CreateRequest> メッセージを使用する必要があります。  
  
### <a name="uploading-files-from-disk"></a>ディスクからのファイルのアップロード  
 WebResource.Content プロパティには、ファイルのバイナリ コンテンツを表す Base 64 文字列が必要です。 次のサンプルは、ファイルを必要な種類に変換するために使用するメソッドです。  
  
```C#
//Encodes the Web Resource File
static public string getEncodedFileContents(String pathToFile)
{
    FileStream fs = new FileStream(pathToFile, FileMode.Open, FileAccess.Read);
    byte[] binaryData = new byte[fs.Length];
    long bytesRead = fs.Read(binaryData, 0, (int)fs.Length);
    fs.Close();
    return System.Convert.ToBase64String(binaryData, 0, binaryData.Length);
}
```
  
### <a name="combining-web-resource-record-data-with-file-data"></a>Web リソース レコード データとファイル データの結合  
 ImportJob.xml ファイルは、インポートされるファイルに関するデータと、作成する Web リソースに関するデータの結合方法を示します。 具体的には、関連ファイル間の相対リンクを引き続き機能させるために、作成する Web リソースの名前では、ファイル名にシミュレートされたディレクトリを使用して、ディスク上のファイルの相対位置に関する情報を保持する必要があります。 ImportJob.xml ファイル内のデータにより、これらの関連 Web リソース ファイルはすべて共通の仮想フォルダーに作成されます。  
  
> [!NOTE]
>  作成時に Web リソースを公開する必要はありません。 更新時には公開する必要があります。  
  
## <a name="example"></a>例  
 ImportWebResources.cs ファイルの次の部分には、次の変数が必要です。  
  
- `_customizationPrefix`: **MDA SDK サンプル**発行者のカスタマイズの接頭辞。 この発行者が存在しない場合は、"sample" というカスタマイズの接頭辞で作成されます。  
  
- `_ImportWebResourcesSolutionUniqueName`: このサンプルで作成された **Web リソースのインポートのサンプル ソリューション**の一意の名前。 値は `ImportWebResourcesSample` です。  
  
```C#
//Read the descriptive data from the XML file
XDocument xmlDoc = XDocument.Load("../../ImportJob.xml");

//Create a collection of anonymous type references to each of the Web Resources
var webResources = from webResource in xmlDoc.Descendants("webResource")
                   select new
                   {
                       path = webResource.Element("path").Value,
                       displayName = webResource.Element("displayName").Value,
                       description = webResource.Element("description").Value,
                       name = webResource.Element("name").Value,
                       type = webResource.Element("type").Value
                   };

// Loop through the collection creating Web Resources
int counter = 0;
foreach (var webResource in webResources)
{
    //Set the Web Resource properties
    WebResource wr = new WebResource
    {
        Content = getEncodedFileContents(@"../../" + webResource.path),
        DisplayName = webResource.displayName,
        Description = webResource.description,
        Name = _customizationPrefix + webResource.name,
        LogicalName = WebResource.EntityLogicalName,
        WebResourceType = new OptionSetValue(Int32.Parse(webResource.type))
    };

    // Using CreateRequest because we want to add an optional parameter
    CreateRequest cr = new CreateRequest
    {
        Target = wr
    };
    //Set the SolutionUniqueName optional parameter so the Web Resources will be
    // created in the context of a specific solution.
    cr.Parameters.Add("SolutionUniqueName", _ImportWebResourcesSolutionUniqueName);

    CreateResponse cresp = (CreateResponse)_serviceProxy.Execute(cr);
    // Capture the id values for the Web Resources so the sample can delete them.
    _webResourceIds[counter] = cresp.id;
    counter++;
    Console.WriteLine("Created Web Resource: {0}", webResource.displayName);
}
```
  
  作成時に Web リソースを公開する必要はありません。 更新時には公開する必要があります。  
  
### <a name="see-also"></a>関連項目  
 [Web リソース エンティティの参照](../common-data-service/reference/entities/webresource.md)<br/>
 [Web リソース](web-resources.md)
