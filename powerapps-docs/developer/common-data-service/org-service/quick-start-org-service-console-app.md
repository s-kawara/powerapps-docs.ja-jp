---
title: 'クイック スタート: 組織サービス サンプル (C#) (Common Data Service for Apps) | Microsoft Docs'
description: このクイック スタートでは、Common Data Service for Apps の組織サービスに接続する方法を説明します
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
# <a name="quick-start-organization-service-sample-c"></a>クイック スタート: 組織サービス サンプル (C#)

ここでは、Common Data Service for Apps を使用してデータを操作するために .NET SDK アセンブリの使用を開始できます。

このクイック スタートでは、<xref:Microsoft.Xrm.Tooling.Connector.CrmServiceClient> クラスを使用して組織サービスに接続するために最小限のコンソール アプリケーションを作成します。 コンストラクターに渡された接続文字列を使用して接続情報を渡します。

<xref:Microsoft.Xrm.Sdk.IOrganizationService>.<xref:Microsoft.Xrm.Sdk.IOrganizationService.Execute*> メソッドを使用して、 <xref:Microsoft.Crm.Sdk.Messages.WhoAmIRequest> クラスのインスタンスを渡し、<xref:Microsoft.Crm.Sdk.Messages.WhoAmIResponse>.<xref:Microsoft.Crm.Sdk.Messages.WhoAmIResponse.UserId>  値を表示します。

> [!NOTE]
> このクイック スタートの例には、エラー処理は含まれません。 これは、組織サービスに接続して使用するための最小の例です。


## <a name="prerequisites"></a>前提条件

 - Visual Studio (2017 を推奨)
 - インターネット接続
 - Common Data Service for Apps インスタンスの有効なユーザー アカウント
    - ユーザー名
    - パスワード
 - 接続に使用する CDS for Apps 環境の URL
 - Visual C# 言語の基本的な理解

## <a name="create-visual-studio-project"></a>Visual Studio プロジェクトの作成

1. .NET Framework 4.6.2 を使用して新しいコンソール アプリ (.NET Framework) を作成する

    ![コンソール アプリケーション プロジェクトを開始する](../media/quick-start-org-service-console-app-1.png)

    > [!NOTE]
    > このスクリーンショットは、`OrgServiceQuickStart` という名前を示していますが、必要に応じてプロジェクトとソリューションに名前を指定することを選択できます。 

1. **ソリューション エクスプローラー**で、作成したプロジェクトを右クリックして、コンテキスト メニューで **NuGet Packages の管理...** を選択します。

    ![NuGet パッケージの追加](../media/quick-start-org-service-console-app-2.png)

1. NuGet パッケージ `Microsoft.CrmSdk.XrmTooling.CoreAssembly` の最新バージョンを参照して、インストールします。

    ![Microsoft.CrmSdk.XrmTooling.CoreAssembly NuGet パッケージをインストールする](../media/quick-start-org-service-console-app-3.png)

> [!NOTE]
> **ライセンスの承認** ダイアログで **同意する** を選択する必要があります。

## <a name="edit-programcs"></a>Program.cs を編集する

1. `Program.cs` の一番上にステートメントを使用してこれらを追加する

    ```csharp
    using Microsoft.Crm.Sdk.Messages;
    using Microsoft.Xrm.Tooling.Connector;
    ```

1. `Main` メソッドを次のコードに置き換えます。

    ```csharp
    static void Main(string[] args)
    {            
        // e.g. https://yourorg.crm.dynamics.com
        string url = "<your environment url>";
        // e.g. you@yourorg.onmicrosoft.com
        string userName = "<your user name>";
        // e.g. y0urp455w0rd
        string password = "<your password>";

        string conn = $@"
        Url = {url};
        AuthType = Office365;
        UserName = {userName};
        Password = {password};
        RequireNewInstance = True";

        using (var svc = new CrmServiceClient(conn))
        {

            WhoAmIRequest request = new WhoAmIRequest();

            WhoAmIResponse response = (WhoAmIResponse)svc.Execute(request);

            Console.WriteLine("Your UserId is {0}", response.UserId);

            Console.WriteLine("Press any key to exit.");
            Console.ReadLine();
        }
    }
    ```

1. 環境の情報を追加するには、次の値を編集します。

    ```csharp
    // e.g. https://yourorg.crm.dynamics.com
    string url = "<your environment url>";
    // e.g. you@yourorg.onmicrosoft.com
    string userName = "<your user name>";
    // e.g. y0urp455w0rd
    string password = "<your password>";
    ```

## <a name="run-the-program"></a>プログラムを実行する

1. F5 キーを押してプログラムを実行します。 出力は次のように表示されます。

    ```
    Your UserId is 969effb0-98ae-478c-b547-53a2968c2e75
    Press any key to exit.
    ```

### <a name="congratulations"></a>ご報告: 

組織サービスに正常に接続されました。


## <a name="next-steps"></a>次の手順

これらのトピックでは、CDS for Apps エンティティの使用方法について説明します。

[組織サービスを使用したエンティティ操作](entity-operations.md)<br />
[組織サービスを使用したエンティティの作成](entity-operations-create.md)<br />
[組織サービスを使用してエンティティを取得する](entity-operations-retrieve.md)<br />
[組織サービスを使用したエンティティの更新と削除](entity-operations-update-delete.md)<br />
[組織サービスを使用したエンティティの関連付けまたは関連付けを解除する](entity-operations-associate-disassociate.md)