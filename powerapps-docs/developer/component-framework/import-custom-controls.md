---
title: インポート コントロール | Microsoft Docs
description: カスタム コントロールのインポート処理
keywords: null
ms.author: nabuthuk
manager: kvivek
ms.date: 06/20/2019
ms.service: powerapps
ms.suite: ''
ms.topic: article
---

# <a name="package-a-custom-component"></a>ユーザー定義コンポーネントをパッケージ化する

このトピックはカスタム コントロールを Common Data Service にインポートする方法を示します。 PowerApps CLI でカスタム コントロールを開発した後、次のステップはそれらのコントロールをインポートすることで、これで実行時にコントロールを表示できます。

ソリューション ファイルを作成してインポートする手順を示します:

1. `cd <your new folder>` の後で `pac solution init --publisherName <enter your publisher name> --customizationPrefix <enter your publisher name>` コマンドを使用して、選択したディレクトリに新しいソリューション プロジェクトを作成します。

   > [!NOTE]
   > `publisherName` と `cutomizationPrefix` の値は環境に固有である必要があります。
 
2. 新しいソリューション プロジェクトを作成したら、その作成したコントロールが配置される場所を参照する必要があります。 コマンド `pac solution add-reference --path <path of your PowerApps component framework project on disk>` を使用して参照を追加できます
3. ソリューション プロジェクトから zip ファイルを生成するには、ソリューション プロジェクト ディレクトリに `cd` してから `msbuild /t:build /restore` コマンドを使ってプロジェクトをビルドする必要があります

    > [!NOTE]
    > - msbuild 15 がパスにない場合は、Vs 2017 の開発者コマンド プロンプトを開いて msbuild コマンドを実行します。    
    > - *デバッグ* 構成でソリューションをビルドして、アンマネージド ソリューション パッケージを生成します。 管理ソリューション パッケージは、*リリース* 構成でソリューションを構築することにより生成されます。 これらの設定は、cdsproj ファイルで SolutionPackageType プロパティを指定することでオーバーライドできます。
    > - 運用ビルドを発行するために`Release` にmsbuild構成を設定できます。 例: `msbuild /p:configuration=Release` 

4. 生成されたソリューション ファイルは `\bin\debug\` にあります。
5. Webポータルを使用して手動でソリューションをインポートする必要があります。

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

[エンティティやフィールドにコントロールを追加](add-custom-controls-to-a-field-or-entity.md)<br/>
[PowerApps コンポーネント フレームワークの API リファレンス](reference/index.md)<br/>
[PowerApps コンポーネント フレームワークの概要](overview.md)
