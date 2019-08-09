---
title: PowerApps CLI の更新| Microsoft Docs
description: PowerApps CLI の更新
keywords: PowerApps コンポーネント フレームワーク、カスタム コンポーネント、コンポーネント フレームワーク
ms.author: nabuthuk
manager: kvivek
ms.date: 05/23/2019
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 47c4426c-e963-4ef6-a4b7-d56591ca8ac2
---

# <a name="updating-tooling-to-latest-version"></a>ツーリングを最新バージョンに更新

Microsoft PowerApps CLI を 最新バージョン 02.856.1 に更新し、最新機能をすべて利用して、VS 2017 の開発者のコマンド プロンプトで次のコマンドを実行します。

```CLI
pac install latest
```

## <a name="what-else-do-i-need-to-know"></a>ほかに知る必要があることは？

ソリューション プロジェクトまたは PowerApps component frameworkプロジェクトをすでに作成している場合は、必ずこれらのプロジェクトを最新のパッケージに更新してください。 これにより、既存のプロジェクトで新しく追加された機能を利用できます。 新しく作成されたプロジェクトには、すでにこれらの設定が含まれます。

- PowerApps component framework プロジェクト フォルダにある `pcfproj` の バージョン タグを更新します:

   ```XML
   <PackageReference Include="Microsoft.PowerApps.MSBuild.Pcf" Version="0.*"/>
   ```
- ソリューション プロジェクト フォルダにある `cdsproj` の バージョン タグを更新します:

   ```XML
   <PackageReference Include="Microsoft.PowerApps.MSBuild.Solution" Version="0.*"/>
   ```

    > [!NOTE] 
    > 上記の変更を行った後、正しいバージョン `msbuild /t:restore` でプロジェクトを作成するコマンドを実行します。


- PowerApps component framework プロジェクト フォルダにある `package.json` ファイル の バージョン タグを更新します:

  ```JSON
  "devDependencies":{
   "pcf-scripts": "^0",
   "pcf-start": "^0"
    }
  ```
   > [!NOTE]
   > 上記の変更を行った後、コマンド プロンプトで 'npm 更新プログラム' を使用すると、常にプロジェクトが正しいバージョンに更新されます。
