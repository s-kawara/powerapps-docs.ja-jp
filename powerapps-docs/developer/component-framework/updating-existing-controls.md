---
title: PowerApps component framework ツールを使用して既存のコードコンポーネントを更新するMicrosoft Docs
description: PowerApps component framework ツールを使用してコンポーネントを更新する
keywords: PowerApps コンポーネントフレームワーク、コードコンポーネント、コンポーネントフレームワーク
ms.author: nabuthuk
author: Nkrb
manager: kvivek
ms.date: 10/01/2019
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d2cbf58a-9112-45c2-b823-2c07a310714c
ms.openlocfilehash: 05e32fb7e098dad3aabf36f2efdaf311c1bea327
ms.sourcegitcommit: 2a3430bb1b56dbf6c444afe2b8eecd0e499db0c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2019
ms.locfileid: "72340232"
---
# <a name="update-existing-code-components"></a>既存のコードコンポーネントを更新する 

モデル駆動型アプリの PowerApps component framework プライベートプレビュー参加要素で、既にコードコンポーネントがビルドされている場合は、新しい ALM 中心のプロジェクト構造との互換性を確保するために、いくつかのマイナー更新を行う必要があります。 

既存の PowerApps コンポーネントフレームワークのコードコンポーネントで新しい PowerApps CLI ツールを使用するには、いくつかの変更が必要です。

> [!NOTE]
> このトピックは、モデル駆動型アプリのコードコンポーネントを更新する場合にのみ適用されます。これは、モデル駆動型アプリのプライベートプレビューの時点で PowerApps CLI ツールを利用できないためです。  

## <a name="creating-an-empty-project"></a>空のプロジェクトの作成

PowerApps CLI を使用して、コードコンポーネント用の新しい空のプロジェクトを作成します。 詳細情報:[ツールを使用したコンポーネントの作成](create-custom-controls-using-pcf.md)

プロジェクトが作成されたら、コードコンポーネントソースを新しいプロジェクトに移行します。

1. 以前のソースファイルのコンポーネントソースファイルをコピーするか、または変更します **。**
2. **コントロール**の内容をコピーするか、controlmanifest .xml**ファイルに**置き換えます。
3. CSS、RESX、IMG などの他のすべての周辺機器リソースを、古いプロジェクトから新しいプロジェクトに対応するサブフォルダーにコピーします。

## <a name="updating-manifest-file"></a>マニフェストファイルを更新しています

コードコンポーネントのプロパティを定義する `ControlManifest.xml` ファイルは、`ControlManifest.Input.xml` ファイルに置き換えられます。 それ以外の場合、2つのファイル間でスキーマが変更されることはほとんどありません。

ただし、いくつかの重要なセマンティック変更があります。

1. @No__t_0 リソースエントリは、コードコンポーネントのプリコンパイルされたソースファイルを指す必要があります。 ファイル名の既定値は、 **index. ts**です。

   たとえば、コンポーネントソースが `MyControl.ts` という名前のファイルに実装されている場合、`ControlManifest.Input.xml` の `code` エントリはそのファイルを指す必要があります。 @No__t_0 ファイルも有効な TypeScript ファイルである必要があります。 これは、`code` エントリでコンパイル済みの JS 出力ファイルを指定したレガシマニフェストファイルとは対照的です。
2. @No__t_1 や `css` などのリソース要素の `path` 属性は、ディスク上のファイルへのローカルパスを参照するようになりました。 例:

    ```XML
   <resources>
    <css path="css/YourControlName" order="1"/>
    </resources>
    ```

上記の `path` 属性は、`YourControlName.css` ファイルが、`ControlManifest.Input.xml` がディスク上に存在する現在のディレクトリを基準とした `css` サブフォルダーにあることを示しています。

次のようにして、ControlManifest .xml ファイルを更新します。

1. @No__t_1 の `code` エントリを、コードコンポーネントのプリコンパイルされたソースファイル (通常は、) に編集します。
2. リソースのパスを編集して、ディスク上のファイルへの相対パスを正しく参照します。

## <a name="updating-the-project-files"></a>プロジェクトファイルの更新

以前のバージョンのツールを使用してコンポーネントを作成し、最新の機能を利用する場合は、次に示すようにプロジェクトファイルを更新してください。

1. 最新のモジュールを使用するように既存のプロジェクトを更新します。
 
   - PowerApps component framework プロジェクトフォルダー内にある `pcfproj` のバージョンタグを次のように更新します。

      ```XML
      <Packagereference Include="Microsoft.PowerApps.MSBuild.Pcf" Version="1.*"/>
      ```
   - ソリューションプロジェクトフォルダー内にある `cdsproj` のバージョンタグを次のように更新します。

      ```XML
      <Packagereference Include="Microsoft.PowerApps.MSBuild.Solution" Version="1.*"/>
      ```

      > [!NOTE] 
      > 上記の変更を行った後、コマンド `msbuild /t:restore` を実行して、プロジェクトを正しいバージョンに更新します。


   - PowerApps component framework プロジェクトフォルダー内にある `package.json` ファイルのバージョンタグを更新します。

      ```JSON
      "devDependencies":{
       "pcf-scripts": "^1",
       "pcf-start": "^1"
          }
      ```
     > [!NOTE]
     > 上記の変更を行った後、`npm update` コマンドを実行して、プロジェクトを正しいバージョンに更新します。

2. 事前に認証プロファイルを作成してある場合は、再作成する必要があります。 これは、パブリックでないクラウドをサポートするために、プロファイルに新しいプロパティが追加されたためです。 これを行うには、次の手順を実行します。
 
    - コマンド `pac auth clear` を実行しています。
    - コマンド `pac auth create --url <your org url>` を実行しています。

## <a name="updating-your-project-with-the-latest-node-modules"></a>最新のノードモジュールを使用したプロジェクトの更新

レガシプロジェクトで最新の CLI 機能を利用するには、最新の npm モジュールを取得する必要があります。 以前にダウンロードしたノードモジュールを更新するには、開発者コマンドプロンプトでプロジェクトディレクトリにアクセスし、コマンド `npm update` を実行します。 

## <a name="using-es6-module-syntax"></a>ES6 module 構文の使用

ビルドツールでは、標準の ES6 モジュール形式を使用してコンポーネントソースがエクスポートされることを想定しています。 レガシコンポーネントは通常、内部モジュール (名前空間とも呼ばれます) としてエクスポートされます。 新しいビルドツールに合わせるには、次のようにコンポーネントのソースファイルを変更する必要があります。

1. コードコンポーネント (たとえば、index. ts) を実装するソースファイルを開きます。
2. 標準の ES6 export 構文を使用するには、モジュール宣言を削除します。

     以前は：
     ```TypeScript
     module SampleNamespace
     {
    export class TSLinearInputControl implements ComponentFramework.StandardControl<InputsOutputs.IInputBag, InputsOutputs.IOutputBag> {
          <your class implementation>
           }
            }
     
      ```
    行っ
    ```TypeScript
     export class YourControlName implements ComponentFramework.StandardControl<IInputs, IOutputs> { 
          <your class implementation>
          }
   ```

## <a name="using-generated-manifest-typing-file"></a>生成されたマニフェスト入力ファイルの使用

レガシプロジェクトでは、`inputsOutputs.d.ts` 入力ファイルを手動で作成して編集する必要があります。これは通常、`private_typing` サブフォルダーにあります。 PowerApps CLI ツールでは、ビルド時にこのファイルが自動的に生成されるようになりました。 

コード生成により、コンポーネントのソースコードで使用される `type` 定義が、コンポーネントマニフェストファイルで定義されている `types` と同期していることが保証されます。

入力ファイルの名前が `ManifestTypes.d.ts` に変更され、`generated` という名前のサブフォルダーに生成されるようになりました。 さらに、`InputsOutputs.IInputBag` と `InputsOutputs.IOutputBag` の種類の名前がそれぞれ `IInputs` および `IOutputs` に変更されています。

新しい入力ファイルを使用するには、次のようにします。

1. コンポーネントソースファイルの先頭に次の行を追加して、新しい `ManifestTypes.d.ts` ファイルをインポートします。

    `./generated/ManifestTypes` から {IInputs、Iinputs} をインポートします。
2. **IInputBag**のすべての参照の名前を**iinputs**に変更します。
3. **Inputsoutputs**のすべての参照を**ioutputs**に名前変更します。
4. コマンド `npm run build` を使用して、新しい**Manifesttypes.** . ts ファイルを生成するプロジェクトをビルドします。

## <a name="troubleshooting-and-workarounds"></a>トラブルシューティングと回避策

1. Pcf スクリプトがどのように使用されているかをたずねる 1 ES の通知がある場合は、これらのスクリプトはコードコンポーネントのビルドにのみ使用され、結果のコンポーネントではバンドルまたは使用されないことに注意してください。  
2. 以前にツールバージョン0.1.817.1 以前を使用してコードコンポーネントを作成していて、最新のビルドモジュールとデバッグモジュールが使用されていることを確認したい場合は、次に示すように、パッケージを更新してください。
   
    ```JSON
     "dependencies": { "@types/node": "^10.12.18", "@types/powerapps-component-framework": "1.1.0"}, "devDependencies": { "pcf-scripts": "~0", "pcf-start": "~0" } 
    ```
3. ビルドが承認の問題のために失敗した場合、ユーザーはエラー `Failed to retrieve information about Microsoft.PowerApps.MSBuild.Pcf from remote source <Feed Url>` を取得します。 この回避策を次に示します。

   - % **Appdata% uget**から nuget.exe ファイルを開きます。 ユーザーがエラーを取得するフィードは、このファイルに存在する必要があります。 
   - Nuget.exe ファイルからフィードを削除するか、PAT トークンを生成して、それを Nuget.exe ファイルに追加します。 例:

     ```XML
     <?xml version="1.0" encoding="utf-8"?>  
     <configuration>  
     <packageSources>  
         <add key="CRMSharedFeed" value="https://dynamicscrm.pkgs.visualstudio.com/_packaging/CRMSharedFeed/nuget/v3/index.json" />  
      </packageSources>  
     <packageSourceCredentials>  
      <CRMSharedFeed>  
      <add key="Username" value="anything" />  
      <add key="Password" value="User PAT" />  
    </CRMSharedFeed>  
     </packageSourceCredentials>  
   </configuration>
     ```

### <a name="see-also"></a>関連項目

[PowerApps コンポーネントフレームワークの制限事項](limitations.md)<br/>
[PowerApps コンポーネントフレームワーク API リファレンス](reference/index.md)<br/>
[PowerApps コンポーネントフレームワークの概要](overview.md)
