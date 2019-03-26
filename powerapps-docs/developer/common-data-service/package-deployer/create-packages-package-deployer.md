---
title: Package Deployer ツールのためにパッケージを作成する (アプリ用 Common Data Service) | Microsoft Docs
description: アプリ用 Common Data Service インスタンスで管理者が展開できるパッケージを作成します。
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: shmcarth
ms.author: jdaly
manager: ryjones
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="create-packages-for-the-package-deployer"></a>Package Deployer のパッケージを作成する

Package Deployer はアプリ用 Common Data Service インスタンスで管理者がパッケージを展開できるようにします。 *パッケージ*は、次の一部またはすべてで構成されます。  

- 1 つ以上のアプリ用 CDS ソリューション ファイル。  
- フラット ファイルまたは Configuration Migration ツールからエクスポートされた構成データ ファイル。 ツールの詳細については、[構成移行ツールでインスタンスと組織間を移動する構成データを移動](/dynamics365/customer-engagement/admin/manage-configuration-data) を参照してください。  
- パッケージの前、間、または後に実行できるカスタム コードは、アプリ用 CDS インスタンスに展開されます。  
- 展開プロセスの最初か最後に表示可能なパッケージに固有の HTML コンテンツ。 これは、パッケージに展開されるソリューションおよびファイルの説明を提供するのに便利です。  

アプリ用 CDS には、アプリ用 CDS インスタンスに展開するために Package Deployer ツールと共に使用することができる、これらのパッケージを作成するための Visual Studio テンプレートが用意されています。

<a name="Prereq"></a>
 
## <a name="prerequisites"></a>前提条件  

- パッケージに含めるすべてのソリューションとファイルがそろっていることを確認します。  
- Microsoft .NET Framework 4.6.2
- Visual Studio 2015 または Visual Studio 2017
- [Visual Studio 2015](https://visualstudiogallery.msdn.microsoft.com/5d345edc-2e2d-4a9c-b73b-d53956dc458d) 向け NuGet パッケージ マネージャ
    - Visual Studio 2017 では、NuGet および NuGet Package Manager は任意の .NET-related ワークロードを選択するときに自動的にインストールされました。
- パッケージ テンプレートを含む Visual Studio 用の Microsoft Dynamics CRM SDK テンプレート。 [Microsoft Dynamics CRM SDK テンプレート](http://go.microsoft.com/fwlink/p/?LinkId=400925) をダウンロードして `CRMSDKTemplates.vsix` ファイルをダブルクリックし、テンプレートを Visual Studio にインストールすることにより取得できます。  



<a name="HowTo"></a>
   
## <a name="create-a-package"></a>パッケージを作成する  

 パッケージを作成するには、次の 5 手順に従います。  

- [ステップ 1: テンプレートを使用してプロジェクトを作成する](create-packages-package-deployer.md#Step1)  
- [手順 2: ファイルをプロジェクトに追加する](create-packages-package-deployer.md#Step2)  
- [手順3: HTML ファイルを更新](create-packages-package-deployer.md#Step3)  
- [手順 4: パッケージの構成値を指定する](create-packages-package-deployer.md#Step4)  
- [ステップ 5: パッケージ用のカスタム コードを定義する](create-packages-package-deployer.md#Step5)  

<a name="Step1"></a>  
 
#### <a name="step-1-create-a-project-using-the-template"></a>ステップ 1: テンプレートを使用してプロジェクトを作成する  

1. Visual Studio を起動し、新しいプロジェクトを作成します。  
2. **新しいプロジェクト** ダイアログ ボックスで以下を実行します。 

   1. インストールされているテンプレートの一覧から、**Visual C#** を展開し、**Dynamics 365 SDK のテンプレート**を選択します。  
   2. **.NET Framework 4.6.2** が選択されていることを確認します。  
   3. **Dynamics 365 パッケージ**を選択します。  
   4. プロジェクトの名前と場所を指定し、**OK** をクリックします。  

    ![カスタム パッケージを作成するための新しいプロジェクト](../media/crm-sdkv6-packagedeployer-01.png)

<a name="Step2"></a>   

#### <a name="step-2-add-your-files-to-the-project"></a>手順 2: ファイルをプロジェクトに追加する  

1.  **ソリューション エクスプ ローラー**ウィンドウで、**PkgFolder** フォルダーの下にソリューションとファイルを追加します。  
2.  **PkgFolder** フォルダーの下に追加するファイルごとに、**プロパティ**ウィンドウで、**出力ディレクトリにコピー**の値を**常にコピー**に設定します。  これにより、ファイルが、生成されたパッケージで利用できます。  

<a name="Step3"></a>  
 
#### <a name="step-3-update-the-html-files-english-and-other-languages"></a>ステップ 3: HTML ファイルを更新する: 英語および他の言語  

1.  ソリューション エクスプローラ ウィンドウで、**PkgFolder** > **コンテンツ** > **en-us** を展開します。 `EndHTML` および `WelcomeHTML` という名前の 2 つのフォルダーが見つかります。 これらのフォルダーには、パッケージの展開プロセスの最初と最後に情報を表示するための HTML と関連ファイルが含まれます。 これらのフォルダーの HTML フォルダー内のファイルを編集して、パッケージの情報を追加します。  

2.  パッケージに他の言語の HTML ファイルを追加できます。それにより、ユーザーのコンピューターのロケール設定に基づいた言語で、HTML コンテンツが表示されます。 それには、次を実行します。  

    1.  **en-us** フォルダーのコピーを **PkgFolder** > **コンテンツ**の下に作成します。  
    2.  コピーしたフォルダーの名前を適切な言語に変更します。 たとえば、スペイン語には、名前を**es-ES**に変更します。  
    3.  HTML ファイルのコンテンツを変更して、スペイン語のコンテンツを追加します。  

<a name="Step4"></a>   

#### <a name="step-4-specify-the-configuration-values-for-the-package"></a>手順 4: パッケージの構成値を指定する  

1. **PkgFolder** にある **ImportConfig.xml** ファイル内にパッケージに関する情報を追加することにより、パッケージ構成を定義します。 編集するファイルをダブルクリックして、開きます。 以下のリストは、構成ファイル内の各パラメーターとノードに関する情報を提供します。  

    `installsampledata`  
    `True` または `false`。 `true` の場合は、サンプル データをアプリ用 CDS インスタンスにインストールします。 これはアプリ用 CDS 内の **設定** > **データ管理**領域からインストールすることができるのと同じサンプル データです。  

    `waitforsampledatatoinstall`  
   **true** または **false**。 **true**が設定されており、**installsampledata** も**true**に設定されている場合、パッケージを展開する前に、サンプル データがインストールされるのを待ちます。  

   > [!NOTE]
   >  `waitforsampledatatoinstall`を**true**に設定している場合、**installsampledata**を**true**に設定していることを確認してください。  

    `agentdesktopzipfile`  
    解凍する zip ファイルの名前。 ここで.zip ファイル名を指定する場合は、パッケージの展開プロセス中に、ファイルのコンテンツを解凍する場所を選択するように求める画面を追加します。  

    これは、Unified Service Desk for Dynamics 365 のパッケージを作成するのによく使用されます。 Unified Service Desk の詳細については、[Unified Service Desk 3.0 の管理者ガイド](/dynamics365/customer-engagement/unified-service-desk/administration-guide-unified-service-desk-3) を参照してください。  

    `agentdesktopexename`  
    展開プロセスの最後に呼び出される zip ファイルまたは URL の .exe または .msi ファイルの名前。  

    これは、Unified Service Desk のパッケージを作成するのによく使用されます。  

    `crmmigdataimportfile`  
    Configuration Migration ツールを使用してエクスポートされた、既定の構成データ ファイル (.zip) のファイル名。  

   - Package Deployer の実行中、新しいランタイム設定を使用して指定されたロケール ID (LCID) に基づいて構成データ ファイルのローカライズ済みファイルをインポートできます。 `<cmtdatafile>` ノード (後で説明) を使用してパッケージ内のローカライズ済みの構成データ ファイルを指定し、 `OverrideConfigurationDataFileLanguage` メソッド (後で説明) を使用してランタイム設定を使用して指定されたロケール ID に基づいて構成データ ファイルをインポートするためのロジックを指定します。 パッケージを使用して一度に複数の構成データ ファイルをインポートすることはできません。  

   - アプリ用 CDS (設置型) の場合、構成データ ファイルにユーザー情報が含まれており、ソースとターゲットのアプリ用 CDS インスタンスの両方が同じ Active Directory ドメイン上にある場合、ユーザー情報は対象のアプリ用 CDS インスタンスにインポートされます。 異なるドメインのアプリ用 CDS (設置型) インスタンスにユーザー情報をインポートするには、プロジェクトで 構成移行ツールを使用して生成されたユーザー マップ ファイル (.xml) を含め、それを後で説明される `<cmtdatafile>` ノードの `usermapfilename` 属性を使用して構成データ ファイルに沿って指定する必要があります。 ユーザー情報はアプリ用 CDS インスタンスにインポートすることはできません。  
     `<solutions>`ノード  
     インポートするソリューションについて説明する`<configsolutionfile>`ノードの配列が含まれます。 このノードの下のソリューションの順序は、ターゲットアプリ用 CDS インスタンス上にソリューションがインポートされる順序を示します。  

     `<configsolutionfile>`ノード  
     `<solutions>` ノードの下のこのノードを使用して、個々のソリューションおよびインポートする各ソリューションの次の情報を指定します:  

   - `solutionpackagefilename`: ソリューションの .zip ファイル名を指定します。 必須。  

   - `overwriteunmanagedcustomizations`: 対象 Dynamics 365 インスタンスにすでに存在するソリューションをインポートするときに、アンマネージド カスタマイズをすべて上書きするかをどうかを指定します。 これはオプションで、この属性を指定しない場合、既定では、既存のソリューションのアンマネージド カスタマイズは対象の Dynamics 365 インスタンスで保持されます。  

   - `publishworkflowsandactivateplugins`: ワークフローを公開するか、ソリューションがインポートされた後にターゲット Dynamics 365 インスタンスのプラグインをアクティブ化するかどうかを指定します。 これはオプションで、この属性を指定しないように指定した場合、既定では、ワークフローは公開され、プラグインは、ソリューションがターゲット Dynamics 365 インスタンスにインポートされた後にアクティブ化されます。  

     `<configsolutionfile>`ノードを必要なだけ追加することによって、パッケージに複数のソリューションのファイル名を追加できます。 たとえば、3 つのソリューション ファイルをインポートする場合、次のように追加します。  

   ```xml  

   <solutions>  
   <configsolutionfile solutionpackagefilename="SampleSolutionOne_1_0_managed.zip"  
   overwriteunmanagedcustomizations="false"  
   publishworkflowsandactivateplugins="true"/>  
   <configsolutionfile solutionpackagefilename="SampleSolutionTwo_1_0_managed.zip"  
   overwriteunmanagedcustomizations="false"  
   publishworkflowsandactivateplugins="true"/>  
   <configsolutionfile solutionpackagefilename="SampleSolutionThree_1_0_managed.zip" />  
   </solutions>  

   ```  

    `<filestoimportnode>`ノード  
    インポートする個々のファイルとzip ファイルを別々に説明するのに使用する`<configimportfile>`と`<zipimportdetails>`ノードの配列が含まれます。  

    `<configimportfile>`ノード  
    `<configimportfile>` ノードの下のこのノードを使用して、アプリ用 CDS インポートされるファイルを説明します。 `<configimportfile>`ノードを必要なだけ追加することによって、パッケージに複数のファイルを追加できます。  

   ```xml  

   <filestoimport>  
   <configimportfile filename="File.csv"  
   filetype="CSV"  
   associatedmap="FileMap"  
   importtoentity="FileEntity"  
   datadelimiter=""  
   fielddelimiter="comma"  
   enableduplicatedetection="true"  
   isfirstrowheader="true"  
   isrecordownerateam="false"  
   owneruser=""  
   waitforimporttocomplete="true" />  
   <configimportfile filename="File.zip"  
   filetype="ZIP"  
   associatedmap="FileMapName"  
   importtoentity="FileEntity"  
   datadelimiter=""  
   fielddelimiter="comma"  
   enableduplicatedetection="true"  
   isfirstrowheader="true"  
   isrecordownerateam="false"  
   owneruser=""  
   waitforimporttocomplete="true"/>  

   </filestoimport>  

   ```  

    これには、次の属性があります。  

   |属性|内容|
   |--|-|
   |`filename`| インポート データを格納しているファイルの名前。 ファイルが.zip ファイルの場合、`<zipimportdetails>` ノードは、.zip ファイル内の各ファイル用の `<zipimportdetail>` ノードと共にあります。 |
   |`filetype`|これは、csv、xml、または zipになります。          |
   |`associatedmap`|このファイルで使用するアプリ用 CDS インポート データ マップの名前。 空白の場合、このファイルにシステムが決定したインポート データ マップ名を使用しようとします。|
   |`importtoentity`| プロセスの最後に呼び出すリンクを提供する zip ファイル内の exe ファイル、URL、または .msi ファイルの名前になります。|
   |`datadelimiter`| インポート ファイルで使用される、データ区切り文字の名前。 有効な値は singlequote または doublequotesです。|
   |`fielddelimiter`|インポート ファイルで使用される、フィールド区切り文字の名前。 有効な値は、comma または colon、または singlequoteです。|
   |`enableduplicatedetection`|データのインポート時に重複データ検出ルールを有効にするかどうかを示します。 有効な値は、**true** または **false**です。|
   |`isfirstrowheader`|インポート ファイルの最初の行にフィールド名が含まれていることを示すのに使用します。 有効な値は、`true` または `false`。 |
   |`isrecordownerateam`|インポート時のレコードの所有者をチームにするかどうかを示します。 有効な値は、`true` または `false`。|
   |`owneruser`|レコードを所有するユーザー ID を示します。 既定値は、現在ログオンしているユーザーです。  |
   |`waitforimporttocomplete`|`true` の場合、システムは続行する前にインポートの完了を待ちます。 `false` の場合、ジョブをキューして次に進みます。|

    `<zipimportdetails>`ノード  
    このノードには、Dynamics 365 にインポートするために使用される zip ファイルに含まれるファイルについて説明する `<zipimportdetail>` ノードの配列が含まれます。  

    `<zipimportdetail>`ノード  
    `<zipimportdetails>`ノードの下のこのノードを使用して、`<configimportfile>`ノードで指定されている、.zip ファイル内の個々のファイルの情報を提供します。  

   ```xml  
   <filestoimport>  
   ...  
   ...  
   <zipimportdetails>  
   <zipimportdetail filename="subfile1.csv" filetype="csv" importtoentity="account" />  
   <zipimportdetail filename="subfile2.csv" filetype="csv" importtoentity="contact" />  
   </zipimportdetails>  
   </filestoimport>  

   ```  

    これには、次の属性があります。  

   |属性|内容|  
   |---------------|-----------------|  
   |`filename`|インポート データを格納しているファイルの名前。|  
   |`filetype`|これは csv または xml です。|  
   |`importtoentity`|プロセスの最後に呼び出すリンクを提供する、.zip ファイル内の exe ファイル、URL、または .msi ファイルの名前になります。|  

    `<filesmapstoimport>`ノード  
    このノードには、インポートする`<configmapimportfile>`ノードの配列が含まれます。 このノードのマップ ファイルの順序は、インポートされた順序を示します。 データ マップの詳細については、[インポート用データ マップの作成](../create-data-maps-for-import.md) を参照してください。  

    `<configimportmapfile>`ノード  
    `<filesmapstoimport>` ノードの下にあるこのノードを使用して、アプリ用 CDS でインポートする個々のマップ ファイルに関する情報を提供します。  

   ```xml  
   <filesmapstoimport>  
   <configimportmapfile filename="FileMap.xml" />  
   </filesmapstoimport>  
   ```  

    `<cmtdatafiles>`ノード  
    このノードには、インポートするローカライズ済みの構成データ ファイルを含む `<cmtdatafile>` ノードの配列が含まれます。  

    `<cmtdatafile>`ノード  
    `<cmtdatafiles>` ノード下でこのノードを使用して、ロケール ID (必須) およびユーザー情報マップ ファイル (オプション) と共にローカライズ済みの構成データ ファイルを指定します。 たとえば、次のようになります。  

   ```xml  
   <cmtdatafiles>  
   <cmtdatafile filename="data_1033.zip" lcid="1033" usermapfilename="UserMap.xml" />  
   <cmtdatafile filename="data_1041.zip" lcid="1041" usermapfilename="" />  
   </cmtdatafiles>  
   ```  

    ランタイム設定を使用して指定されたロケール ID (LCID) の値 (後で説明) に基づいて、既定の構成データ ファイル (crmmigdataimportfile で指定) の代わりに、`OverrideConfigurationDataFileLanguage` メソッドでカスタム ロジックを定義して、ローカライズ済みの構成データ ファイルをインポートすることができます。  

2. **すべてを保存**をクリックします。  

    次に示すものは、サンプル `ImportConfig.xml` ファイルの目次です。  

   ```xml  
   <?xml version="1.0" encoding="utf-16"?>  
   <configdatastorage xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  
   xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
   installsampledata="true"  
   waitforsampledatatoinstall="true"  
   agentdesktopzipfile=""  
   agentdesktopexename=""  
   crmmigdataimportfile="data_1033.zip">  
   <solutions>  
   <configsolutionfile solutionpackagefilename="SampleSolutionOne_1_0_managed.zip"  
   overwriteunmanagedcustomizations="false"  
   publishworkflowsandactivateplugins="true"/>  
   <configsolutionfile solutionpackagefilename="SampleSolutionTwo_1_0_managed.zip"  
   overwriteunmanagedcustomizations="false"  
   publishworkflowsandactivateplugins="true"/>  
   <configsolutionfile solutionpackagefilename="SampleSolutionThree_1_0_managed.zip" />  
   </solutions>  
   <filestoimport>  
   <configimportfile filename="SampleOption.csv"  
   filetype="CSV"  
   associatedmap="SampleOption"  
   importtoentity="sample_option"  
   datadelimiter=""  
   fielddelimiter="comma"  
   enableduplicatedetection="true"  
   isfirstrowheader="true"  
   isrecordownerateam="false"  
   owneruser=""  
   waitforimporttocomplete="false"/>  
   <configimportfile filename="File.zip"  
   filetype="ZIP"  
   associatedmap="FileMapName"  
   importtoentity="FileEntity"  
   datadelimiter=""  
   fielddelimiter="comma"  
   enableduplicatedetection="true"  
   isfirstrowheader="true"  
   isrecordownerateam="false"  
   owneruser=""  
   waitforimporttocomplete="true"/>  
   <zipimportdetails>  
   <zipimportdetail filename="subfile1.csv"  
   filetype="csv"  
   importtoentity="account" />  
   <zipimportdetail filename="subfile2.csv"  
   filetype="csv"  
   importtoentity="contact" />  
   </zipimportdetails>  
   </filestoimport>  
   <filesmapstoimport>  
   <configimportmapfile filename="SampleOption.xml" />  
   </filesmapstoimport>  
   <cmtdatafiles>  
   <cmtdatafile filename="data_1033.zip"  
   lcid="1033"  
   usermapfilename="UserMap.xml" />  
   <cmtdatafile filename="data_1041.zip"  
   lcid="1041"  
   usermapfilename="" />  
   </cmtdatafiles>  
   </configdatastorage>  

   ```  

<a name="Step5"></a>  
 
#### <a name="step-5-define-custom-code-for-your-package"></a>ステップ 5: パッケージ用のカスタム コードを定義する  

1. ソリューション エクスプローラ ウィンドウで、ルートにある **PackageTemplate.cs** ファイルをダブルクリックして編集します。  

2. PackageTemplate.cs ファイルでは、以下の内容を実行することができます。  

   1. パッケージが`InitializeCustomExtension`のオーバーライド メソッドの定義で初期化されるときに実行するカスタム コードを入力します。  

       パッケージの実行中、このメソッドは、ユーザーがランタイム パラメータを使用できるようにするのに使用することができます。 開発者として、ユーザーの入力によって処理するコードが存在する限り、<xref:Microsoft.Xrm.Tooling.PackageDeployment.CrmPackageExtentionBase.IImportExtensions2.RuntimeSettings> プロパティを使用することで、任意のランタイム パラメーターのサポートをパッケージに追加することができます。  

       たとえば、次のサンプル コードは、可能性のある 2 つの値 true または false を持つパッケージに対して `SkipChecks` と呼ばれるランタイム パラメーターを有効にします。 サンプル コードは、ユーザーが Package Deployer の実行中 (コマンドラインまたはPowerShellのいずれかを使用して) に、いずれかのランタイム パラメーターを指定しているかどうかをチェックして、次にそれに従って情報を処理します。 パッケージの実行中にユーザーがランタイム パラメーターを指定しない場合、<xref:Microsoft.Xrm.Tooling.PackageDeployment.CrmPackageExtentionBase.IImportExtensions2.RuntimeSettings> プロパティの値は null になります。  

      ```csharp  
      public override void InitializeCustomExtension()  
      {  
      // Do nothing.  

      // Validate the state of the runtime settings object.  
      if (RuntimeSettings != null)  
      {  
      PackageLog.Log(string.Format("Runtime Settings populated.  Count = {0}", RuntimeSettings.Count));  
      foreach (var setting in RuntimeSettings)  
      {  
      PackageLog.Log(string.Format("Key={0} | Value={1}", setting.Key, setting.Value.ToString()));  
      }  

      // Check to see if skip checks is present.  
      if ( RuntimeSettings.ContainsKey("SkipChecks") )  
      {  
      bool bSkipChecks = false;  
      if (bool.TryParse((string)RuntimeSettings["SkipChecks"], out bSkipChecks))  
      OverrideDataImportSafetyChecks = bSkipChecks;  
      }  
      }  
      else  
      PackageLog.Log("Runtime Settings not populated");  
      }  
      ```  

       これによって、管理者はコマンド ラインまたは [Import-CrmPackage](/powershell/module/microsoft.xrm.tooling.packagedeployment/import-crmpackage) コマンドレットを使用して、パッケージをインポートするために、Package Deployer ツールの実行中にセーフティ チェックを回避するかどうかを指定することができます。 詳細情報: [Dynamics 365 Package Deployer および Windows PowerShell を使用してパッケージを展開する](/dynamics365/customer-engagement/admin/deploy-packages-using-package-deployer-windows-powershell)  

   2. ソリューションが `PreSolutionImport` tの上書きメソッドの定義にインポートされる前に実行するカスタム コードを入力して、対象のアプリ用 CDS インスタンスの指定されたソリューションの更新中に、カスタマイズを維持または上書きするかどうか、プラグインとワークフローを自動的にアクティブ化するかどうかを指定します。  

   3. `RunSolutionUpgradeMigrationStep` の上書きメソッド定義を使用して、データ転送を実行または 2 つのバージョンのソリューション間でアップグレードします。このメソッドは、ユーザーがインポートするソリューションが既に対象のアプリ用 CDS インスタンスに存在する場合にのみ呼び出されます。  

        この関数は、次のパラメーターが必要です。  

        |    パラメーター    |            内容             |
        |-----------------|------------------------------------|
        | `solutionName`  |        ソリューションの名前        |
        |  `oldVersion`   | 古いソリューションのバージョン番号。 |
        |  `newVersion`   | 新しいソリューションのバージョン番号。 |
        | `oldSolutionId` |     古いソリューションのGUID。      |
        | `newSolutionId` |     新しいソリューションのGUID。      |


   4. ソリューションのインポートが`BeforeImportStage`メソッドの上書き定義で完了する前に実行するカスタム コードを入力します。 ソリューションのインポートが完了する前に、`ImportConfig.xml` ファイルで指定されたソリューションのサンプル データおよびいくつかのフラット ファイルがインポートされます。  

   5. `OverrideConfigurationDataFileLanguage`の上書きメソッドの定義を使用して構成データのインポートに対して現在選択されている言語を上書きします。 指定した言語の指定されたロケール ID (LCID) がパッケージの利用可能な言語の一覧にない場合、既定のデータ ファイルがインポートされます。  

       `ImportConfig.xml` ファイルの `<cmtdatafiles>` ノードの構成データに対して利用可能な言語を指定します。 既定の構成データ インポート ファイルは `crmmigdataimportfile` ファイルの`ImportConfig.xml` 属性で指定されます 。  

       Skipping data checks (<xref:Microsoft.Xrm.Tooling.PackageDeployment.CrmPackageExtentionBase.IImportExtensions2.OverrideDataImportSafetyChecks> = true) のスキップは、対象のアプリ用 CDS インスタンスにデータ何も含まれていないことがはっきりしている場合に、ここで有効にすることができます。  

   6. インポートが `AfterPrimaryImport`>メソッドの上書き定義で完了した後に実行するカスタム コードを入力します。 ソリューションのインポートが開始する前に、これまでにインポートされなかった残りのフラット ファイルがインポートされるようになりました。  

   7. PkgFolder から必要なパッケージ名に、パッケージ フォルダーの既定の名前を変更します。 そのようにするには、**ソリューション エクスプローラー**ペインの `PkgFolder`>フォルダーを名前変更してから、`GetImportPackageDataFolderName` プロパティの下の戻り値を編集します。  

      ```csharp  
      public override string GetImportPackageDataFolderName  
      {  
      get  
      {  
      // WARNING this value directly correlates to the folder name in the Solution Explorer where the ImportConfig.xml and sub content is located.  
      // Changing this name requires that you also change the correlating name in the Solution Explorer  
      return "PkgFolder";  
      }  
      }  
      ```  

   8. `GetNameOfImport`プロパティで戻り値を編集することによって、パッケージの名前を変更します。  

      ```csharp  
      public override string GetNameOfImport(bool plural)  
      {  
      return "Package Short Name";  
      }  
      ```  

       これは、Dynamics 365 Package Deployer ウィザードのパッケージの選択ページで表示されるパッケージの名前です。  

   9. `GetImportPackageDescriptionText`プロパティで戻り値を編集することによって、パッケージの説明を変更します。  

       ```csharp  

       public override string GetImportPackageDescriptionText  
       {  
       get { return "Package Description"; }  
       }  

       ```  

        これは、Package Deployer のウィザードのパッケージの選択ページで、パッケージの名前の横に表示されるパッケージの説明です。  

   10. `GetLongNameOfImport`プロパティで戻り値を編集することによって、パッケージの詳しい名前を変更します。  

       ```csharp  

       public override string GetLongNameOfImport  
       {  
       get { return "Package Long Name"; }  
       }  

       ```  

        インストールするパッケージを選択した後、次のページで、パッケージの長い名前が表示されます。  

3. また、次の関数と変数はパッケージに使用できます。  


   |名前|種類|説明|
   |--|--|--|
   |<xref:Microsoft.Xrm.Tooling.PackageDeployment.CrmPackageExtentionBase.ImportExtension.CreateProgressItem(System.String)> |関数|ユーザー インターフェイス (UI) で新しい処理中項目を作成するときに使用します。 |
   |<xref:Microsoft.Xrm.Tooling.PackageDeployment.CrmPackageExtentionBase.ImportExtension.RaiseUpdateEvent(System.String,Microsoft.Xrm.Tooling.PackageDeployment.CrmPackageExtentionBase.ProgressPanelItemStatus)> |関数| <xref:Microsoft.Xrm.Tooling.PackageDeployment.CrmPackageExtentionBase.ImportExtension.CreateProgressItem(System.String)>.の呼び出しによって作成された処理中の更新に使用します。<br /><br /> <xref:Microsoft.Xrm.Tooling.PackageDeployment.CrmPackageExtentionBase.ProgressPanelItemStatus> は次の値の列挙体です。<br /><br /> 作業中 = 0<br />完了 = 1<br />失敗 = 2<br />警告 = 3<br />不明 = 4 |
   |<xref:Microsoft.Xrm.Tooling.PackageDeployment.CrmPackageExtentionBase.ImportExtension.RaiseFailEvent(System.String,System.Exception)>|関数|現在の状態のインポートが失敗する場合に例外メッセージと共に使用します。|
   |<xref:Microsoft.Xrm.Tooling.PackageDeployment.CrmPackageExtentionBase.ImportExtension.IsRoleAssoicatedWithTeam(System.Guid,System.Guid)>|関数|ロールが特定のチームに関連付けられているかどうかを判断する場合に使用します。|
   |<xref:Microsoft.Xrm.Tooling.PackageDeployment.CrmPackageExtentionBase.ImportExtension.IsWorkflowActive(System.Guid)>|関数|指定したワークフローがアクティブになっているかどうかを判断する場合に使用します。 |
   |<xref:Microsoft.Xrm.Tooling.PackageDeployment.CrmPackageExtentionBase.ImportExtension.PackageLog>| クラスのポインター|これは、パッケージの初期化されたログ インターフェイスへのポインターです。 このインターフェイスは、パッケージのログ ファイルにメッセージと例外をログするのに、パッケージによって使用されます。|
   |<xref:Microsoft.Xrm.Tooling.PackageDeployment.CrmPackageExtentionBase.ImportExtension.RootControlDispatcher>|プロパティ|パッケージの展開時に、コントロールが独自の UI をレンダリングするのを許可するのに使用されるディスパッチャーのインターフェイスです。 UI 要素やコマンドをラップするのにも、このインターフェイスを使用します。 値を設定しているかどうかわからないので、それを使用する前にnull 値のこの変数を確認することは重要です。  |
   |<xref:Microsoft.Xrm.Tooling.PackageDeployment.CrmPackageExtentionBase.ImportExtension.CrmSvc>|プロパティ |これは、パッケージがパッケージ内から Dynamics 365 に対応できるようにする <xref:Microsoft.Xrm.Tooling.Connector.CrmServiceClient> クラスに対するポインターです。 これを使用して、上書きされたメソッドで SDK メソッドと他のアクションを実行します。|
   |<xref:Microsoft.Xrm.Tooling.PackageDeployment.CrmPackageExtentionBase.IImportExtensions2.DataImportBypass> |プロパティ|これを使用して、Dynamics 365 Package Deployer が、アプリ用 CDS サンプル データ、フラット ファイル データ、および構成移行ツールからエクスポートされたデータのインポートなどのすべてのデータ インポート操作をスキップするかどうかを指定します。 true または false を指定します。 既定は`false`です。|
   | <xref:Microsoft.Xrm.Tooling.PackageDeployment.CrmPackageExtentionBase.IImportExtensions2.OverrideDataImportSafetyChecks> |プロパティ|これを使用して、インポートのパフォーマンスの向上に役立つ、安全チェックの一部を、Dynamics 365 Package Deployer がスキップするかどうかを指定します。 `true`または`false`を指定します。 既定は`false`です。<br /><br /> 対象のアプリ用 CDS インスタンスにデータが含まれていない場合のみ、これを `true` に設定する必要があります。|


4. プロジェクトを保存し、ビルドして (**ビルド** > **ソリューションのビルド**) パッケージを作成します。 パッケージは *\<Project>* \Bin\Debug フォルダーの下の以下のファイルです。  

   - **\<PackageName> フォルダー**: フォルダー名はこのセクション (ステップ 5: パッケージのカスタム コードの定義) のステップ 2.g のパッケージ フォルダー名に対して変更したものと同じです。 このフォルダーには、パッケージのすべてのソリューション、構成データ、 フラット ファイル、および目次が含まれます。  

   - **\<PackageName>.dll**: アセンブリには、パッケージのカスタム コードが含まれています。 既定では、アセンブリ名は Visual Studio のプロジェクト名と同じです。  

     次のステップは、パッケージの展開です。  

<a name="UsethePackage"></a> 
  
## <a name="deploy-a-package"></a>パッケージ展開  

 パッケージを作成した後、Package Deployer ツールまたは Windows PowerShell のいずれかを使用して、アプリ用 CDS インスタンスに展開することができます。 

 Package Deployer ツールは [Microsoft.CrmSdk.XrmTooling.PackageDeployment.WPF](https://www.nuget.org/packages/Microsoft.CrmSdk.XrmTooling.PackageDeployment) NuGet パッケージの一部として配布されます。Package Deployer ツールをダウンロードするには、[NuGet からツールをダウンロード](../download-tools-nuget.md) を参照してください。

 詳細については、「[Dynamics 365 Package Deployer または Windows PowerShell を使用してパッケージを展開する](/dynamics365/customer-engagement/admin/deploy-packages-using-package-deployer-windows-powershell)」を参照してください。  

<a name="BestPractices"></a>   

## <a name="best-practices-for-creating-and-deploying-packages"></a>パッケージを作成し、展開するためのベスト プラクティス  

パッケージの作成中に、開発者はパッケージのアセンブリが署名されていることを確認する必要があります。  

パッケージを展開するときに、アプリ用 CDS 管理者は、次をする必要があります。  

- 署名付きパッケージのアセンブリに対して主張して、アセンブリをそのソースにまで追跡できます。  
- 運用環境インスタンスにそれを実行する前に、事前運用インスタンス (可能であれば、運用環境インスタンスのミラー イメージ) にパッケージをテストします。  
- パッケージを展開する前に、運用環境インスタンスをバックアップします。  



