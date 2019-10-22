---
title: " IFRAME コンポーネント |Microsoft Docs"
description: IFRAME コンポーネントの実装
ms.custom: ''
manager: kvivek
ms.date: 10/01/2019
ms.service: powerapps
ms.topic: article
ms.author: nabuthuk
author: Nkrb
ms.openlocfilehash: d10b03c478f238df02ee7e1309c0e39e758ce4c9
ms.sourcegitcommit: 2a3430bb1b56dbf6c444afe2b8eecd0e499db0c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2019
ms.locfileid: "72340462"
---
# <a name="implementing-a-iframe-component"></a>IFRAME コンポーネントの実装

このサンプルでは、コードコンポーネントをフォームの別のフィールドにバインドし、これらのフィールドの値をコンポーネントの入力プロパティとして使用する方法について説明します。  

> [!div class="mx-imgBorder"]
> ![Iframe コンポーネント](../media/iframe-control.png "iframe コンポーネント")

## <a name="available-for"></a>利用可能な対象 

モデル駆動型アプリとキャンバスアプリ (試験段階プレビュー) 

## <a name="manifest"></a>マニフェスト

```XML
<?xml version="1.0" encoding="utf-8"?>
<manifest>
    <control namespace="SampleNamespace" constructor="TSIFrameControl" version="1.0.0" display-name-key="TS_IFrameControl_Display_Key" description-key="TS_IFrameControl_Desc_Key" control-type="standard">
        <property name="stringProperty" display-name-key="stringProperty_Display_Key" description-key="stringProperty_Desc_Key" of-type="SingleLine.Text" usage="bound" required="true" />
        <property name="latitudeValue" display-name-key="Bing_Maps_Latitude_Value" description-key="latitude" of-type="FP" usage="bound" required="true" />
        <property name="longitudeValue" display-name-key="Bing_Maps_Longitude_Value" description-key="longitude" of-type="FP" usage="bound" required="true" />
        <resources>
            <code path="index.ts" order="1" />
            <css path="css/TS_IFrameControl.css" order="2" />
        </resources>
    </control>
</manifest>
```

## <a name="code"></a>コード

```TypeScript
import { IInputs, IOutputs } from "./generated/ManifestTypes";
export class TSIFrameControl
  implements ComponentFramework.StandardControl<IInputs, IOutputs> {
  // reference to Bing Map IFrame HTMLElement
  private _bingMapIFrame: HTMLElement;
  // reference to the control container HTMLDivElement
  // This element contains all elements of our custom control example
  private _container: HTMLDivElement;
  // Flag if control view has been rendered
  private _controlViewRendered: Boolean;
  /**
   * Used to initialize the control instance. Controls can kick off remote server calls and other initialization actions here.
   * Data-set values are not initialized here, use updateView.
   * @param context The entire property bag available to control via Context Object; It contains values as set up by the customizer mapped to property names defined in the manifest, as well as utility functions.
   * @param notifyOutputChanged A callback method to alert the framework that the control has new outputs ready to be retrieved asynchronously.
   * @param state A piece of data that persists in one session for a single user. Can be set at any point in a controls life cycle by calling 'setControlState' in the Mode interface.
   * @param container If control is marked control-type='standard', it receives an empty div element within which it can render its content.
   */
  public init(
    context: ComponentFramework.Context<IInputs>,
    notifyOutputChanged: () => void,
    state: ComponentFramework.Dictionary,
    container: HTMLDivElement
  ) {
    this._container = container;
    this._controlViewRendered = false;
  }
  /**
   * Called when any value in the property bag has changed. This includes field values, data-sets, global values such as container height and width, offline status, control metadata values such as label, visible, etc.
   * @param context The entire property bag available to control via Context Object; It contains values as set up by the customizer mapped to names defined in the manifest, as well as utility functions
   */
  public updateView(context: ComponentFramework.Context<IInputs>) {
    if (!this._controlViewRendered) {
      this._controlViewRendered = true;
      this.renderBingMapIFrame();
    }
    let latitude: number = context.parameters.latitudeValue.raw;
    let longitude: number = context.parameters.longitudeValue.raw;
    this.updateBingMapURL(latitude, longitude);
  }
  /**
   * Render IFrame HTML Element that hosts the Bing Map and appends the IFrame to the control container
   */
  private renderBingMapIFrame(): void {
    this._bingMapIFrame = this.createIFrameElement();
    this._container.appendChild(this._bingMapIFrame);
  }
  /**
   * Updates the URL of the Bing Map IFrame to display the updated lat/long coordinates
   * @param latitude : latitude of center point of Bing map
   * @param longitude : longitude of center point of Bing map
   */
  private updateBingMapURL(latitude: number, longitude: number): void {
    // Bing Map API:
    // https://msdn.microsoft.com/library/dn217138.aspx
    // Provide bing map query string parameters to format and style map view
    let bingMapUrlPrefix = "https://www.bing.com/maps/embed?h=400&w=300&cp=";
    let bingMapUrlPostfix = "&lvl=12&typ=d&sty=o&src=SHELL&FORM=MBEDV8";
    // Build the entire URL with the user provided latitude and longitude
    let iFrameSrc: string =
      bingMapUrlPrefix + latitude + "~" + longitude + bingMapUrlPostfix;
    // Update the IFrame to point to the updated URL
    this._bingMapIFrame.setAttribute("src", iFrameSrc);
  }
  /**
   * Helper method to create an IFrame HTML Element
   */
  private createIFrameElement(): HTMLElement {
    let iFrameElement: HTMLElement = document.createElement("iframe");
    iFrameElement.setAttribute("class", "TS_SampleControl_IFrame");
    return iFrameElement;
  }
  /**
   * It is called by the framework prior to a control receiving new data.
   * @returns an object based on nomenclature defined in manifest, expecting object[s] for property marked as “bound” or “output”
   */
  public getOutputs(): IOutputs {
    // no-op: method not leveraged by this example custom control
    return {};
  }
  /**
   * Called when the control is to be removed from the DOM tree. Controls should use this call for cleanup.
   * i.e. canceling any pending remote calls, removing listeners, etc.
   */
  public destroy() {
    // no-op: method not leveraged by this example custom control
  }
}
```

## <a name="resources"></a>リソース

```css
.SampleNamespace\.TSIFrameControl .TS_SampleControl_IFrame
{
    width: 300px;
    height: 400px;
}
```

> [!NOTE]
> PowerApps component framework では、複合フィールドがまだサポートされていないため、このコンポーネントを既定の緯度および経度のアドレスフィールドにバインドすることはできません。 コードコンポーネントを別の浮動小数点フィールドにバインドする必要があります。

このサンプルコンポーネントは、`Bing Maps URL` を表示する `IFRAME` をレンダリングします。 コンポーネントは、フォーム上の2つの浮動小数点フィールドにバインドされます。このフィールドはコンポーネントにパラメーターとして渡され、`IFRAME URL` に挿入されて、指定された入力の緯度と経度に Bing マップを更新します。  

フォーム上の2つのフィールドへのバインドを含めるように `Manifest` ファイルを更新します。  
この変更は、初期化中にこれらのバインドされたフィールドをコンポーネントに渡す必要があることと、値のいずれかが更新されるたびに、PowerApps コンポーネントフレームワークに通知します。
  
```xml

<property name="latitudeValue" display-name-key="Bing_Maps_Latitude_Value" description-key="latitude" of-type="FP" usage="bound" required="true" />  
<property name="longitudeValue" display-name-key="Bing_Maps_Longitude_Value" description-key="longitude" of-type="FP" usage="bound" required="true" />  
```

追加のバインドされたプロパティが必要な場合があります。 コンポーネントがフォームにバインドされている場合、コンポーネントの構成時にこの設定が適用されます。 これは、コンポーネントマニフェストのプロパティノードの `required` 属性を設定することによって構成できます。 コンポーネントのプロパティがフィールドにバインドされないようにする場合は、値を false に設定します。 
 
`IInputs` インターフェイスに2つのフィールドを追加するには、`ControlFramework.d.ts` を更新する必要があります。 これは、PowerApps コンポーネントフレームワークによってフィールド値が渡される形式です。 これらの値を `IInputs` インターフェイスに追加すると、TypeScript ファイルが値を参照して正常にコンパイルできるようになります。  

```TypeScript
    export interface IInputs 
    { latitudeValue: ControlFramework.PropertyTypes.NumberProperty;  
        longitudeValue: ControlFramework.PropertyTypes.NumberProperty;  
    }  
 ```

初期レンダリングでは `IFRAME` 要素が生成され、コントロールコンテナーに追加されます。 この `IFRAME` は、 **Bing マップ**を表示するために使用されます。 @No__t_0 の url は `Bing Map URL` に設定され、バインドされたフィールド (latitudeValue と longitudeValue) を url に含めて、マップを指定した場所に中央揃えで配置します。 

これらのフィールドのいずれかがフォームで更新されるたびに、 [Updateview](../reference/control/updateview.md)メソッドが呼び出されます。 このメソッドは、コンポーネントに渡された新しい緯度と経度の値を使用するように、 **Bing マップ**の IFRAME の url を更新します。 このコンポーネントを実行時に表示するには、他のコードコンポーネントと同様に、コンポーネントをフォーム上のフィールドにバインドします。

### <a name="related-topics"></a>関連トピック

[サンプルコンポーネントのダウンロード](https://go.microsoft.com/fwlink/?linkid=2088525)<br/>
[PowerApps コンポーネントフレームワークマニフェストスキーマリファレンス](../manifest-schema-reference/index.md)<br />
[PowerApps コンポーネントフレームワーク API リファレンス](../reference/index.md)<br />
[PowerApps コンポーネントフレームワークの概要](../overview.md)
