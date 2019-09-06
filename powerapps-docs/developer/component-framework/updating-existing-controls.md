---
title: PowerApps コンポーネント フレームワーク ツールを使用して既存のカスタム コンポーネントを更新する | Microsoft Docs
description: PowerApps コンポーネント フレームワーク ツールを使用してコンポーネントを更新する
keywords: PowerApps コンポーネント フレームワーク、カスタム コンポーネント、コンポーネント フレームワーク
ms.author: nabuthuk
author: Nkrb
manager: kvivek
ms.date: 04/23/2019
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d2cbf58a-9112-45c2-b823-2c07a310714c
---
# <a name="updating-existing-custom-components"></a>既存のユーザー定義コンポーネントを更新する 

[!INCLUDE[cc-beta-prerelease-disclaimer](../../includes/cc-beta-prerelease-disclaimer.md)]

PowerApps コンポーネント フレームワークのプライベート プレビュー参加者で、既にカスタム コンポーネントを作成している場合は、新しい ALM 中心のプロジェクト構造と互換性を保つために、いくつかマイナー アップデートを行う必要があります。 新しい PowerApps コンポーネント フレームワークのビルド ツールを既存の PowerApps コンポーネント フレームワークのカスタム コンポーネント ソースとともに使用するには、いくつか変更が必要です。

## <a name="creating-an-empty-project"></a>空のプロジェクトを作成する

カスタム コンポーネントに新しい空のプロジェクトを作成するには、PowerApps CLI を使用します。 詳細: [ツールを使用してコンポーネントを作成する](create-custom-controls-using-pcf.md).
プロジェクトが作成されたら、カスタム コンポーネントのソースを新しいプロジェクトに移行します:

1. コンポーネント ソースを古いソース ファイルから **index.ts** にコピーするか置き換えます。
2.  **ControlManifest.xml** の内容を **ControlManifest.Input.xml** ファイルにコピーまたは置き換えます。
3. css、resx、img など他のすべての周辺コンポーネント リソースを、古いプロジェクトから新しいプロジェクトの対応するサブフォルダーにコピーします。

## <a name="updating-manifest-file"></a>マニフェスト ファイルの更新

カスタム コンポーネントのプロパティを定義する `ControlManifest.xml` ファイルは `ControlManifest.Input.xml` ファイルに置き換えられました。 それ以外の場合、ふたつのファイル間のスキーマにほとんど変更はありません。
重要なセマンティックの変更点がいくつかあります。

1. `code` リソース エントリはカスタム コンポーネントの事前コンパイルされたソース ファイルを指すようになりました。 ファイル名は既定で **index.ts** になりました。
たとえばコンポーネント ソースが `MyControl.ts` と呼ばれるファイルに実装された場合、`ControlManifest.Input.xml` の `code` エントリはそのファイルを指す必要があります。 `code` ファイルも有効な Typescript ファイルである必要があります。 これは `code` エントリでコンパイルされた JS 出力ファイルを指定した、従来のマニフェスト ファイルとは対照的です。
2. `code` や `css` のようなリソース要素の `path` 属性は、現在ディスクのファイルへのローカル パスを参照します。 たとえば、

    ```XML
   <resources>
    <css path="css/YourControlName" order="1"/>
    </resources>
    ```

上記の `path` 属性は、`YourControlName.css` ファイルが `ControlManifest.Input.xml` がディスク上に存在する現在のディレクトリを基準にした `css` サブフォルダにあることを示します。
次のように ControlManifest.Input.xml ファイルを更新します:

1. `ControlManifest.Input.xml` の `code` エントリを、カスタム コンポーネントの事前コンパイルのソース ファイルに編集します (通常これはindex.tsです)。
2. ディスク上のファイルへの相対パスを正しく参照するように、リソースのすべてのパスを編集します。

## <a name="using-es6-module-syntax"></a>ES6 モジュール構文を使用する

ビルド ツールはコンポーネント ソースが標準の ES6 モジュール形式を使用してエクスポートされることを意図します。 従来のコントロールは通常、内部モジュール (別名名前空間) としてエクスポートされます。 新しいビルド ツールに合わせて、コンポーネント ソースを次のように修正する必要があります。

1. カスタム コンポーネントを実装するソース ファイル (たとえば index.ts) を開きます。
2. モジュール宣言を削除して標準の ES6 エクスポート構文を使用します

     削除前:
     ```TypeScript
     module SampleNamespace
     {
    export class TSLinearInputControl implements ComponentFramework.StandardControl<InputsOutputs.IInputBag, InputsOutputs.IOutputBag> {
          <your class implementation>
           }
            }
     
      ```
    以下の後で:
    ```TypeScript
     export class YourControlName implements ComponentFramework.StandardControl<IInputs, IOutputs> { 
          <your class implementation>
          }
   ```

## <a name="using-generated-manifest-typing-file"></a>生成されたマニフェスト タイピング ファイルの使用

従来のプロジェクトでは手動で `inputsOutputs.d.ts` タイピング ファイルを作成し編集する必要がありました。 このファイルは通常 `private_typing` サブフォルダの下にあります。 新しいツールはビルド時に自動的にこのファイルを生成します。 Code-genは、コンポーネントのソースコードで使われる `type` の定義が、コンポーネント マニフェスト ファイルで定義された `types` と同期していることを保証します。  
タイピング ファイルは `ManifestTypes.d.ts` という名前に変更され、現在は `generated` という名前のサブフォルダに生成されます。 さらに、`InputsOutputs.IInputBag` と `InputsOutputs.IOutputBag` 型は `IInputs` と `IOutputs` にそれぞれ名前が変更されます。
新しいタイピング ファイルを使用するには:

1. コンポーネントのソース ファイルの先頭に次の行を追加して、新しい `ManifestTypes.d.ts` ファイルをインポートします。`./generated/ManifestTypes` から { IInputs、IOutputs } をインポートします。
2. **InputsOutputs.IInputBag** の参照をすべて **IInputs** に名前を変更します。
3. **InputsOutputs.IOutputBag** の参照をすべて IOutputs** に名前を変更します。
4. コマンド `npm run build` を使って、プロジェクトをビルドして新しい **ManifestTypes.d.ts** ファイルを生成します。

### <a name="see-also"></a>関連項目

[PowerApps コンポーネント フレームワークの制限](limitations.md)<br/>
[PowerApps コンポーネント フレームワークの API リファレンス](reference/index.md)<br/>
[PowerApps コンポーネント フレームワークの概要](overview.md)
