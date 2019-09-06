---
title: コンポーネントのインポート | Microsoft Docs
description: カスタム コンポーネントのインポート処理
keywords: null
ms.author: nabuthuk
manager: kvivek
ms.date: 06/20/2019
ms.service: powerapps
ms.suite: ''
ms.topic: article
author: Nkrb
---

# <a name="package-a-custom-component"></a>ユーザー定義コンポーネントをパッケージ化する

このトピックではカスタム コンポーネント Common Data Service にインポートする方法について説明します。 PowerApps CLI を使用してカスタム コンポーネントを開発した後は、それらコンポーネントをインポートします。これにより、実行時にコンポーネントを確認できるようになります。

ソリューション ファイルを作成してインポートする手順を示します:

1. `cd <your new folder>`の後に `pac solution init --publisher-name <enter your publisher name> --publisher-prefix <enter your publisher name>` コマンドを実行して、任意のディレクトリに新しいソリューション プロジェクトを作成します。 ソリューション プロジェクトは、環境へのインポートに使用するソリューションzipファイルにカスタム コンポーネントをパッケージ化するために使用されます。

   > [!NOTE]
   > `publisher-name` と `publisher-prefix` の値は環境に固有である必要があります。
 
2. 新しいソリューション プロジェクトを作成したら、その作成したコンポーネントが配置された場所を参照する必要があります。 以下のコマンド を使用して参照を追加することができます。 この参照は、構築において追加するカスタム コンポーネントをソリューション プロジェクトに通知し、単一のソリューション プロジェクト内で複数のコンポーネントへの参照を追加することができます。

    ```CLI   
    pac solution add-reference --path<path of your PowerApps component framework project on disk>
    ```

3. ソリューションプロジェクトから zipファイルを生成するには、 `cd` をソリューション プロジェクトのディレクトリに配置し、 `msbuild /t:build /restore`コマンドを使用してプロジェクトを構築する必要があります。 このコマンドは MSBuild を使用して、リストアの一部として NuGet の依存関係を文かいすることで、ソリューション プロジェクトを構築します。 初めてソリューションプロジェクトを構築する際には `/restore` のみを使用します。 以降の各構築処理ごとに、 `msbuild`コマンドを実行することができます。

    > [!NOTE]
    > - msbuild 15.9.*がパスに存在しない場合は、VS2017の開発者コマンドプロンプトを開いて `msbuild` コマンドを実行します。    
    > - *デバッグ* 構成でソリューションをビルドして、アンマネージド ソリューション パッケージを生成します。 管理ソリューション パッケージは、*リリース* 構成でソリューションを構築することにより生成されます。 これらの設定は、cdsproj ファイルで SolutionPackageType プロパティを指定することでオーバーライドできます。
    > - 運用ビルドを発行するために`Release` にmsbuild構成を設定できます。 例: `msbuild /p:configuration=Release` 

4. 構築の完了後、生成されたソリューション ファイルは `\bin\debug\` に配置されます。
5. Webポータルを使用して手動でソリューションをインポートすることができます。

## <a name="how-to-remove-components-from-a-solution"></a>ソリューションからコンポーネントを削除する方法

ソリューションからカスタム コンポーネントを削除する場合は、次の手順に従ってください。

1.  ソリューション プロジェクト ディレクトリ の cdsproj ファイルを編集し、コンポーネントへの参照を削除します。 以下は、コンポーネント リファレンスの例です:

```XML
<ItemGroup>
    <ProjectReference Include="..\pcf_component\pcf_component.pcfproj">
      <Project>0481bd83-ffb0-4b70-b526-e0b3dd63e7ef</Project>
      <Name>pcf_component </Name>
      <Targets>Build</Targets>
      <ReferenceOutputAssembly>false</ReferenceOutputAssembly>
      <OutputItemType>Content</OutputItemType>
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
    </ProjectReference>
</ItemGroup>
```

2.  コマンドを実行して再構築 (またはクリーンアップ) を実行します。
   ```CLI
   msbuild /t:rebuild
   ```

### <a name="see-also"></a>関連項目

[エンティティやフィールドにコントロールを追加する](add-custom-controls-to-a-field-or-entity.md)<br/>
[PowerApps コンポーネント フレームワークの API リファレンス](reference/index.md)<br/>
[PowerApps コンポーネント フレームワークの概要](overview.md)
