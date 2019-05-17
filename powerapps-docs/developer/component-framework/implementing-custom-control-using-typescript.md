---
title: TypeScript を使用したカスタム コントロールの実装 | MicrosoftDocs
description: TypeScript を使用してカスタム コントロールを実装する方法
manager: kvivek
ms.date: 04/23/2019
ms.service: powerapps
ms.author: nabuthuk
---

# <a name="implement-controls-using-typescript"></a>TypeScript を使用してコントロールを実装する

このチュートリアルは Typescript で新しいカスタム コントロールを作成する方法を説明します。 サンプルのコントロールは、線形入力コントロールです。 線形入力コントロールを使用すると、直接値を入力する代わりに視覚的なスライダーを使用して数値を入力できます。


## <a name="implementing-manifest"></a>マニフェストの実装

カスタム コントロールは `Manifest.xml` マニフェスト ファイルの情報で定義されます。 線形入力コントロールでは、スライダー入力の数値を格納するためのプロパティが定義されます。

1. コード エディタ (Visual Studio Code) で `Manifest.xml` ファイルを開きます。 `Manifest.xml` ファイルは `sampleProperty` と呼ばれる初期のコントロール プロパティを定義します。

    ```XML
    <property name="sampleProperty" display-name-key="Property_Display_Key" description-key="Property_Desc_Key" of-type="SingleLine.Text" usage="bound" required="true" /> 
    ```

2. `sampleProperty` の名前を変更してプロパティの種類を変更する

    ```XML
    <property name="sliderValue" display-name-key=" sliderValue _Display_Key" description-key=" sliderValue_Desc_Key" of-type-group="numbers" usage="bound" required="true" /> 
    ```

3. of-type-group 属性は、許容された数のグループを参照します。 マニフェストの <property> 要素に兄弟として次の種類グループ要素を追加します。 種類グループはコントロール値を指定し、整数、通貨、浮動小数点、または 10 進数値を含めることができます。

    ```XML
    <type-group name="numbers"> 
      <type>Whole.None</type> 
      <type>Currency</type> 
      <type>FP</type> 
      <type>Decimal</type> 
     </type-group> 
    ```


4. `ControlManifest.Input.xml` ファイルに加えた変更を保存します。
5. コマンド `npm run build` を使ってコントロール プロジェクトを構築します。
6. ビルドは更新された Typescript 型の宣言ファイルを `TSLinearInputControl/generated folder` に生成します  `ManifestTypes.d.ts` ファイルは独自のコントロールが Typescript ソースコードにアクセスするプロパティを定義します。

## <a name="implementing-control-logic"></a>コントロール ロジックの実装

カスタム コントロールのソースは `index.ts` ファイルで実装されます。 `index.ts` ファイルは PowerApps コンポーネント フレームワークに必要なインターフェース メソッドの足場を含みます。 

1. 任意の選択したコード エディタで `index.ts` ファイルを開きます。
2. 以下のように `TSLinearInputControl` クラスを更新します

```TypeScript
export class TSLinearInputControl implements ComponentFramework.StandardControl<IInputs, IOutputs> {
// Value of the field is stored and used inside the control 
private _value: number;
// PowerApps component framework framework delegate which will be assigned to this object which would be called whenever any update happens. 
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
    
public init(context: ComponentFramework.Context<IInputs>, notifyOutputChanged: () => void, state: ComponentFramework.Dictionary, container:HTMLDivElement)
  {
     this._context = context;
     this._container = document.createElement("div");
     this._notifyOutputChanged = notifyOutputChanged;
     this._refreshData = this.refreshData.bind(this);
     // creating HTML elements for the input type range and binding it to the function which refreshes the control data
     this.inputElement = document.createElement("input");
     this.inputElement.setAttribute("type","range");
     this.inputElement.addEventListener("input",this._refreshData);
     //setting the max and min values for the control.
     this.inputElement.setAttribute("min","1");
     this.inputElement.setAttribute("max","1000");
     this.inputElement.setAttribute("class","linearslider");
     this.inputElement.setAttribute("id","linearrangeinput");
     // creating a HTML label element that shows the value that is set on the linear range control
     this.labelElement = document.createElement("label");
     this.labelElement.setAttribute("class", "TS_LinearRangeLabel");
     this.labelElement.setAttribute("id","lrclabel");
     // retrieving the latest value from the control and setting it to the HTMl elements.
     this._value = context.parameters.sliderValue.raw;
     this.inputElement.setAttribute("value",context.parameters.sliderValue.formatted ? context.parameters.sliderValue.formatted : "0");
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

public refreshData(evt: Event) : void
  {
      this._value = (this.inputElement.value as any)as number;
      this.labelElement.innerHTML = this.inputElement.value;
      this._notifyOutputChanged();
    }
        
public updateView(context: ComponentFramework.Context<IInputs>): void
 {
      // storing the latest context from the control.
    this._value = context.parameters.sliderValue.raw;
    this._context = context;
    this.inputElement.setAttribute("value",context.parameters.sliderValue.formatted ? context.parameters.sliderValue.formatted : "");
    this.labelElement.innerHTML = context.parameters.sliderValue.formatted ? context.parameters.sliderValue.formatted : "";
        }
    
public getOutputs(): IOutputs
  {
     return {
            sliderValue : this._value
            };
        }
        
public destroy()
   {
     this.inputElement.removeEventListener("input", this._refreshData);
        }
    }
```

3. コマンド `npm run build` を使ってコントロール プロジェクトを再構築します。 
 
4. コントロールは `/out/controls/TSLinearInputControl` フォルダにコンパイルされます。 ビルドで生成されるのは以下を含みます:

   - bundle.js – バンドルされたコントロールのソースコード 
   - ControlManifest.xml – Common Data Service 組織にアップロードされる実際のコントロール マニフェスト ファイル。

## <a name="adding-style-to-the-custom-control"></a>カスタム コントロールにスタイルを追加する

線形入力コントロールの `init` メソッドは入力要素を作り、クラス属性を `linearslider` に設定します。 `linearslider` クラスのスタイルは別に `css` ファイルで定義されます。 さらにカスタマイズをサポートするため `css` ファイルのような追加のコントロール リソースをカスタム コントロールに含めることができます。

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
    background:transparent; 
   -webkit-appearance:none; 
    width:100%;padding:0; 
    height:24px; 
   -webkit-tap-highlight-color:transparent 
    } 
    .SampleNamespace\.TSLinearInputControl input[type=range].linearslider:focus { 
     outline: none; 
     } 
    .SampleNamespace\.TSLinearInputControl input[type=range].linearslider::-webkit-slider-runnable-track {    
     background: #666; 
     height:2px; 
     cursor:pointer 
     }    
     .SampleNamespace\.TSLinearInputControl input[type=range].linearslider::-webkit-slider-thumb {    
     background: #666;    
     border:0 solid #f00; 
     height:24px; 
     width:10px; 
     border-radius:48px; 
     cursor:pointer; 
     opacity:1; 
    -webkit-appearance:none; 
     margin-top:-12px 
     }     
    .SampleNamespace\.TSLinearInputControl input[type=range].linearslider::-moz-range-track {    
     background: #666;    
     height:2px; 
     cursor:pointer   
     }    
     .SampleNamespace\.TSLinearInputControl input[type=range].linearslider::-moz-range-thumb {    
     background: #666;    
     border:0 solid #f00; 
     height:24px; 
     width:10px; 
     border-radius:48px; 
    cursor:pointer; 
    opacity:1; 
   -webkit-appearance:none; 
   margin-top:-12px 
   }    
   .SampleNamespace\.TSLinearInputControl input[type=range].linearslider::-ms-track {    
    background: #666;    
    height:2px; 
    cursor:pointer   
     }     
    .SampleNamespace\.TSLinearInputControl input[type=range].linearslider::-ms-thumb {    
    background: #666;    
    border:0 solid #f00; 
    height:24px; 
    width:10px; 
    border-radius:48px; 
   cursor:pointer; 
   opacity:1; 
   -webkit-appearance:none; 
    } 
   ```

5. `TS_LinearInputControl.css` を保存します。 
6. コマンド `npm run build ` を使用してコントロール プロジェクトを再構築します。
7. `./out/controls/TSLinearInputControl` にあるビルド出力を調査して、`TS_LinearInputControl.css` ファイルがコンパイル済みビルド生成物に含まれていることを確認します。 


### <a name="see-also"></a>関連項目

[既存の PowerApps コンポーネント フレームワーク コントロールを更新する](updating-existing-controls.md)
