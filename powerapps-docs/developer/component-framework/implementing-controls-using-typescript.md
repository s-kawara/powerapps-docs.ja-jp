---
title: TypeScript を使用したカスタム コンポーネントの実装 | MicrosoftDocs
description: TypeScript を使用してカスタム コンポーネントを実装する方法
manager: kvivek
ms.date: 04/23/2019
ms.service: powerapps
ms.topic: index-page
ms.assetid: 18e88d702-3349-4022-a7d8-a9adf52cd34f
ms.author: nabuthuk
---

# <a name="implement-components-using-typescript"></a>TypeScript を使ってコンポーネントを実装する

[!INCLUDE[cc-beta-prerelease-disclaimer](../../includes/cc-beta-prerelease-disclaimer.md)]

このチュートリアルは Typescript で新しいカスタム コンポーネントを作成する方法を説明します。 サンプルのコンポーネントは、線形入力コンポーネントです。 線形入力コンポーネントを使用すると、直接値を入力する代わりに視覚的なスライダーを使用して数値を入力できます。 

## <a name="creating-a-new-component-project"></a>新しいコンポーネント プロジェクトを作成する

新しいプロジェクトを作成するには、以下の手順に従います:

1. VS 2017 ウィンドウの開発者コマンド プロンプトを開きます。
2. コマンド `mkdir LinearControl` を使用してプロジェクトの新しいフォルダを作成します。
3. 新しいディレクトリに `cd` して、コマンド `cd LinearControl` を実行します。 
4. コマンド `pac pcf init --namespace SampleNamespace --name TSLinearInputControl --template field` を使用してコンポーネント プロジェクトを作成します 
5. コマンド `npm install` を使用してプロジェクトのビルド ツールをインストールします 
6. 任意の開発者環境でプロジェクトを開き、カスタム コンポーネント開発の実装を開始します。

## <a name="implementing-manifest"></a>マニフェストの実装

カスタム コンポーネントは `ControlManifest.Input.xml` マニフェスト ファイルの情報で定義されます。 このチュートリアルで、このファイルは `<Your component Name>` サブフォルダーに作成されます。 線形入力コンポーネントにはスライダー入力の数値を格納するためのプロパティが定義されます。

1. コード エディタ (Visual Studio コード ) で `ControlManifest.Input.xml` ファイルを開きます。 `ControlManifest.Input.xml` ファイルは `sampleProperty` と呼ばれる初期のコンポーネント プロパティを定義します。

    ```XML
    <property name="sampleProperty" display-name-key="Property_Display_Key" description-key="Property_Desc_Key" of-type="SingleLine.Text" usage="bound" required="true" /> 
    ```

2. `sampleProperty` の名前を変更してプロパティの種類を変更する

    ```XML
    <property name="sliderValue" display-name-key="sliderValue_Display_Key" description-key="sliderValue_Desc_Key" of-type-group="numbers" usage="bound" required="true" /> 
    ```

3. of-type-group 属性は、許容された数のグループを参照します。 マニフェストの <property> 要素に兄弟として次の種類グループ要素を追加します。 種類グループはコンポーネント値を指定し、整数、通貨、浮動小数点、または 10 進数値を含めることができます。

    ```XML
    <type-group name="numbers"> 
      <type>Whole.None</type> 
      <type>Currency</type> 
      <type>FP</type> 
      <type>Decimal</type> 
     </type-group> 
    ```

4. `ControlManifest.Input.xml` ファイルに加えた変更を保存します。
5. 次に、LinearControl フォルダー内に新しいフォルダーを作成し、cssという名前を付けます。
6. [カスタム コンポーネントにスタイルを追加する](#adding-style-to-the-custom-component) ために、cssファイルを作成します。
7. コマンド `npm run build` を使用してコンポーネント プロジェクトをビルドします
8. ビルドは更新された Typescript 型の宣言ファイルを `TSLinearInputControl/generated folder` に生成します  `ManifestTypes.d.ts` ファイルは独自のコンポーネントが Typescript ソースコードにアクセスするプロパティを定義します。

## <a name="implementing-component-logic"></a>コンポーネント ロジックの実装

カスタム コンポーネントのソースは `index.ts` ファイルで実装されます。 `index.ts` ファイルは PowerApps コンポーネント フレームワークに必要なインターフェース メソッドの足場を含みます。 

1. 任意の選択したコード エディタで `index.ts` ファイルを開きます。
2. 以下のように `TSLinearInputControl` クラスを更新します

```TypeScript
export class TSLinearInputControl implements ComponentFramework.StandardControl<IInputs, IOutputs> {
  // Value of the field is stored and used inside the control 
  private _value: number;
  // PCF framework delegate which will be assigned to this object which would be called whenever any update happens. 
  private _notifyOutputChanged: () => void;
  // label element created as part of this control
  private labelElement: HTMLLabelElement;
  // input element that is used to create the range slider
  private inputElement: HTMLInputElement;
  // Reference to the control container HTMLDivElement
  // This element contains all elements of our custom control example
  private _container: HTMLDivElement;
  // Reference to ComponentFramework Context object
  private _context: ComponentFramework.Context<IInputs>;
  // Event Handler 'refreshData' reference
  private _refreshData: EventListenerOrEventListenerObject;

  constructor() {
  }

  public init(context: ComponentFramework.Context<IInputs>, notifyOutputChanged: () => void, state: ComponentFramework.Dictionary, container: HTMLDivElement) {
    this._context = context;
    this._container = document.createElement("div");
    this._notifyOutputChanged = notifyOutputChanged;
    this._refreshData = this.refreshData.bind(this);
    // creating HTML elements for the input type range and binding it to the function which refreshes the control data
    this.inputElement = document.createElement("input");
    this.inputElement.setAttribute("type", "range");
    this.inputElement.addEventListener("input", this._refreshData);
    //setting the max and min values for the control.
    this.inputElement.setAttribute("min", "1");
    this.inputElement.setAttribute("max", "1000");
    this.inputElement.setAttribute("class", "linearslider");
    this.inputElement.setAttribute("id", "linearrangeinput");
    // creating a HTML label element that shows the value that is set on the linear range control
    this.labelElement = document.createElement("label");
    this.labelElement.setAttribute("class", "TS_LinearRangeLabel");
    this.labelElement.setAttribute("id", "lrclabel");
    // retrieving the latest value from the control and setting it to the HTMl elements.
    this._value = context.parameters.sliderValue.raw;
    this.inputElement.setAttribute("value", context.parameters.sliderValue.formatted ? context.parameters.sliderValue.formatted : "0");
    this.labelElement.innerHTML = context.parameters.sliderValue.formatted ? context.parameters.sliderValue.formatted : "0";
    // appending the HTML elements to the control's HTML container element.
    this._container.appendChild(this.inputElement);
    this._container.appendChild(this.labelElement);
    container.appendChild(this._container);
  }

  /**
  * Updates the values to the internal value variable we are storing and also updates the html label that displays the value
  * @param context : The "Input Properties" containing the parameters, control metadata and interface functions
  */

  public refreshData(evt: Event): void {
    this._value = (this.inputElement.value as any) as number;
    this.labelElement.innerHTML = this.inputElement.value;
    this._notifyOutputChanged();
  }

  public updateView(context: ComponentFramework.Context<IInputs>): void {
    // storing the latest context from the control.
    this._value = context.parameters.sliderValue.raw;
    this._context = context;
    this.inputElement.setAttribute("value",context.parameters.sliderValue.formatted ? context.parameters.sliderValue.formatted : "");
    this.labelElement.innerHTML = context.parameters.sliderValue.formatted ? context.parameters.sliderValue.formatted : "";
  }

  public getOutputs(): IOutputs {
    return {
      sliderValue: this._value
    };
  }

  public destroy() {
    this.inputElement.removeEventListener("input", this._refreshData);
  }
}
```

3. コマンド `npm run build` を使ってコントロール プロジェクトを再構築します。 
 
4. コンポーネントは `out/controls/TSLinearInputControl` フォルダにコンパイルされます。 ビルドで生成されるのは以下を含みます:

   - bundle.js – バンドルされたコンポーネントのソースコード 
   - ControlManifest.xml – Common Data Service 組織にアップロードされる実際のコンポーネント マニフェスト ファイル。

## <a name="adding-style-to-the-custom-component"></a>カスタム コンポーネントにスタイルを追加する

線形入力コントロールの `init` メソッドは入力要素を作り、クラス属性を `linearslider` に設定します。 `linearslider` クラスのスタイルは別に `css` ファイルで定義されます。 さらにカスタマイズをサポートするため `css` ファイルのような追加のコンポーネント リソースをカスタム コンポーネントに含めることができます。

1. <resources> 要素内に追加の `css` リソースを含めるために `ControlManifest.Input.xml` ファイルを編集します
 
    ```XML
    <resources> 
      <code path="index.ts" order="1"/> 
      <css path="css/TS_LinearInputControl.css" order="1"/> 
    </resources> 
     ```

2. `TSLinearInputControl` フォルダーの下に新しい `css` サブフォルダーを作成します。 
3. `css` サブ フォルダーに新しい `TS_LinearInputControl.css` ファイルを作成します。 
4. 以下のスタイル コンテンツを `TS_LinearInputControl.css` ファイルに追加します

    ```CSS
    .SampleNamespace\.TSLinearInputControl input[type=range].linearslider {
      margin: 1px 0;
      background: transparent;
      -webkit-appearance: none;
      width: 100%;
      padding: 0;
      height: 24px;
      -webkit-tap-highlight-color: transparent
    }

    .SampleNamespace\.TSLinearInputControl input[type=range].linearslider:focus {
      outline: none;
    }

    .SampleNamespace\.TSLinearInputControl input[type=range].linearslider::-webkit-slider-runnable-track {
      background: #666;
      height: 2px;
      cursor: pointer
    }

    .SampleNamespace\.TSLinearInputControl input[type=range].linearslider::-webkit-slider-thumb {
      background: #666;
      border: 0 solid #f00;
      height: 24px;
      width: 10px;
      border-radius: 48px;
      cursor: pointer;
      opacity: 1;
      -webkit-appearance: none;
      margin-top: -12px
    }

    .SampleNamespace\.TSLinearInputControl input[type=range].linearslider::-moz-range-track {
      background: #666;
      height: 2px;
      cursor: pointer
    }

    .SampleNamespace\.TSLinearInputControl input[type=range].linearslider::-moz-range-thumb {
      background: #666;
      border: 0 solid #f00;
      height: 24px;
      width: 10px;
      border-radius: 48px;
      cursor: pointer;
      opacity: 1;
      -webkit-appearance: none;
      margin-top: -12px
    }

    .SampleNamespace\.TSLinearInputControl input[type=range].linearslider::-ms-track {
      background: #666;
      height: 2px;
      cursor: pointer
    }

    .SampleNamespace\.TSLinearInputControl input[type=range].linearslider::-ms-thumb {
      background: #666;
      border: 0 solid #f00;
      height: 24px;
      width: 10px;
      border-radius: 48px;
      cursor: pointer;
      opacity: 1;
      -webkit-appearance: none;
    }
    ```

5. `TS_LinearInputControl.css` を保存します。 
6. コマンド  を使ってコントロール プロジェクトを再構築します。 
   ```CLI
   npm run build
   ```
7. **./out/controls/TSLinearInputControl** にあるビルド出力を調査して、 **TS_LinearInputControl.css** ファイルがコンパイル済みビルド生成物に含まれていることを確認します。 

## <a name="debugging-your-custom-component"></a>ユーザー定義コンポーネントのデバッグ

カスタム コンポーネント ロジックの実装が完了したら、次のコマンドを実行してデバッグ処理を開始します 

```CLI
npm start
```

## <a name="packaging-your-custom-components"></a>ユーザー定義コンポーネントのパッケージ化

[ソリューション](https://docs.microsoft.com/dynamics365/customer-engagement/customize/solutions-overview) ファイルを作成してインポートするには、次の手順に従います。

1. **LinearComponent** フォルダー内の新しい フォルダー **ソリューション** 作成し、フォルダーに移動します。 
2. コマンドを使用して **LinearComponent** フォルダに新しいソリューション プロジェクトを作成します。 
 
    ```CLI
     pac solution init --publisherName developer --customizationPrefix dev 
    ```

   > [!NOTE]
   > [publisherName](https://docs.microsoft.com/powerapps/developer/common-data-service/reference/entities/publisher) と [cutomizationPrefix](https://docs.microsoft.com/powerapps/maker/common-data-service/change-solution-publisher-prefix) の値は環境に固有である必要があります。
 
3. 新しいソリューション プロジェクトを作成したら、その作成したコンポーネントが配置される場所を参照する必要があります。 コマンド  を使用して参照を追加できます

    ```CLI
     pac solution add-reference --path c:\users\LinearComponent
    ```

4. ソリューション プロジェクトから zip ファイルを生成するには、ソリューション プロジェクト ディレクトリに `cd` して、コマンドを使ってプロジェクトをビルドする必要があります。 

    ```CLI
     msbuild /t:restore
    ```

5. 次のコマンドmsbuildを再度実行します。
    ```CLI
     msbuild
    ```

    > [!NOTE]
    > **NuGet ターゲットおよび構成タスク** を確認してください。 有効にするには、次の手順を行います。
    > - **Visual Studio インストーラー** 開きます。
    > - VS 2017 の場合は、 **変更** をクリックします。
    > - **個別のコンポーネン** をクリックします。
    > - **コード ツール** の **NuGetターゲットとビルド タスク** を参照してください。

6. 生成されたソリューションの zip ファイルは `Solution\\bin\debug\` にあります。
7. zip ファイルの準備ができたら Web ポータルを使用して、手動で [ソリューションをインポート](https://docs.microsoft.com/dynamics365/customer-engagement/customize/import-update-export-solutions) する必要があります。

## <a name="adding-custom-components-to-a-field-or-an-entity"></a>ユーザー定義コンポーネントをフィールドやエンティティに追加する。

データセット コンポーネントや単純なテーブル コンポーネントのようなカスタム コンポーネントをグリッドやビューに追加するには、トピック [フィールドやエンティティにコントロールを追加する](add-custom-controls-to-a-field-or-entity.md) で説明する手順に従います。

### <a name="see-also"></a>関連項目

[サンプル コンポーネントをダウンロード](https://go.microsoft.com/fwlink/?linkid=2088525)<br/>
[既存の PowerApps コンポーネント フレームワーク コントロールを更新する](updating-existing-controls.md)<br/>
[PowerApps コンポーネント フレームワークの API リファレンス](reference/index.md)<br/>
[PowerApps コンポーネント フレームワークの概要](overview.md)
