---
title: Acceleration、App、Compass、Connection、Location の各シグナル | Microsoft Docs
description: PowerApps の各種センサー (Acceleration、App、Compass、Connection、Location) についての構文と例を含んだリファレンス情報です。
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: anneta
ms.date: 11/07/2015
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 147766eb9e9b17698882241e8eb3bd0ae7ba7e78
ms.sourcegitcommit: 0dbbf53aea319e53edadc1d3a9efa5728856ebd8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2019
ms.locfileid: "58172635"
---
# <a name="acceleration-app-compass-connection-and-location-signals-in-powerapps"></a>PowerApps の Acceleration、App、Compass、Connection、Location の各シグナル
ユーザーが地球上のどこにいて、どの画面が表示されているかなど、アプリの環境に関する情報を取得することができます。  

## <a name="description-and-syntax"></a>説明と構文
すべてのシグナルは、情報の[レコード](../working-with-tables.md#records)を返します。 この情報は、レコードとして使用や保存ができるほか、**.** [演算子](operators.md).

> [!NOTE]
> **アクセラレータ**と**Compass**関数は、iOS または Android などのネイティブのプレーヤーで正確な値を返しますが、その関数は、作成するか、ブラウザーでアプリを変更するときにゼロ値を返します。

### <a name="acceleration"></a>Acceleration
**Acceleration** シグナルは、デバイスの画面に対して相対的な 3 次元におけるデバイスの加速度を返します。 加速度は、9.81 m/秒<sup>2</sup> 単位または 32.2 ft/秒<sup>2</sup> 単位、つまり *g* (地球の重力によって地上の物体に与えられる加速度) で表されます。

| プロパティ | 説明 |
| --- | --- |
| **Acceleration.X** |左右。  正数は右を表します。 |
| **Acceleration.Y** |前後。  正数は前を表します。 |
| **Acceleration.Z** |上下。  正数は上を表します。 |

### <a name="app"></a>App
**App** シグナルは、実行中のアプリに関する情報を返します。

| プロパティ | 説明 |
| --- | --- |
| **App.ActiveScreen** | 表示されている画面。 スクリーン オブジェクトを返します。このオブジェクトを使って画面のプロパティを参照したり、別の画面と比較してどちらの画面が表示されているかを調べたりすることができます。 表示された画面を変更するには、使用、 **[戻る](function-navigate.md)** または**[Navigate](function-navigate.md)** 関数。 |
| **App.Width** | アプリが実行されているウィンドウの幅を返します。 設定すると、数式でこのプロパティを使用することができます、**幅**応答性の高いアプリを構築する画面のプロパティ。  |
| **App.Height** | アプリが実行されているウィンドウの高さを返します。 設定すると、数式でこのプロパティを使用することができます、**高さ**応答性の高いアプリを構築する画面のプロパティ。 |
| **App.DesignWidth** | PowerApps Studio でアプリの幅を返します。 設定すると、数式でこのプロパティを使用することができます、**幅**応答性の高いアプリでの最小の幅を確認するための画面のプロパティ。  |
| **App.DesignHeight** | PowerApps Studio でアプリの高さを返します。 設定すると、数式でこのプロパティを使用することができます、**高さ**応答性の高いアプリでの最小の高さを確認するための画面のプロパティ。  |

**アプリ**オブジェクトも、[動作の数式](../working-with-formulas-in-depth.md)を設定できます。

| プロパティ  | 説明 |
| --- | --- |
| **OnStart** | ユーザーが開始したときのアプリの動作です。 通常、このプロパティは取得し、コレクションにデータをキャッシュに使用、 **[収集](function-clear-collect-clearcollect.md)** 関数、変数を設定、 **[設定](function-set.md)** 関数とでの最初の画面に移動し、 **[Navigate](function-navigate.md)** 関数。 最初の画面が表示されるまでは、次の数式が評価されます。 画面が読み込まれていない、コンテキスト変数を設定することはできませんので、 **[UpdateContext](function-updatecontext.md)** 関数。 ただし、コンテキスト変数を渡すことができます、 **Navigate**関数。 |

**アプリ**左側のナビゲーション ウィンドウでコントロールの階層リストの上部にあるオブジェクトが表示され、画面上のコントロールと同様に、このオブジェクトを選択することができます。 オブジェクトを選択した後は、表示し、数式バーの左側のドロップダウン リストでそのプロパティを選択する場合、いずれかのプロパティを編集します。  

変更した後、 **OnStart**プロパティ、それをテストできますでポインターを合わせると、**アプリ**左側のナビゲーション ウィンドウが表示されたら、省略記号 (...) を選択すると、および選択し、オブジェクト**実行OnStart**します。 異なり、アプリが初めて読み込まれるときに、既存のコレクションおよび変数は既に設定されます。 使用して、 **[ClearCollect](function-clear-collect-clearcollect.md)** 関数の代わりに、**収集**関数の最初に空のコレクション。

 ![OnStart の実行とアプリの項目のコンテキスト メニュー](media/appobject-runonstart.png)

### <a name="compass"></a>Compass
**Compass** シグナルは、画面上部のコンパスの方位を返します。 方位は磁北に基づきます。

| プロパティ | 説明 |
| --- | --- |
| **Compass.Heading** |方位 (度)。  0 を北として、0 ～ 360 の数値を返します。 |

### <a name="connection"></a>Connection
**Connection** シグナルは、ネットワーク接続に関する情報を返します。 従量制課金接続では、そのネットワーク上で送受信するデータ量を制限したい場合があります。

| プロパティ | 説明 |
| --- | --- |
| **Connection.Connected** |デバイスがネットワークに接続されているかどうかを示すブール値 **true** または **false** を返します。 |
| **Connection.Metered** |従量制課金接続であるかどうかを示すブール値 **true** または **false** を返します。 |

### <a name="location"></a>Location
**Location** 信号は、GPS (Global Positioning System) やその他のデバイス情報 (携帯電話の基地局通信、IP アドレスなど) に基づくデバイスの位置を返します。

ユーザーは、位置情報に初めてアクセスするとき、その情報へのアクセスを許可するようデバイスから求められる場合があります。

位置との従属関係は、位置が変化する過程で絶えず再計算され、デバイスのバッテリが消費されます。 バッテリの駆動時間を節約するために、**[Enable](function-enable-disable.md)** 関数と **[Disable](function-enable-disable.md)** 関数を使って位置情報の更新のオンとオフを切り替えることができます。 表示されている画面が位置情報に依存していない場合は、位置情報が自動的にオフになります。

| プロパティ | 説明 |
| --- | --- |
| **Location.Altitude** |海抜で測った高度 (フィート) を示す数値を返します。 |
| **Location.Latitude** |赤道との角度で表される緯度を示す -90 ～ 90 の数値を返します。 正数は、赤道より北の位置を示します。 |
| **Location.Longitude** |イギリスのグリニッジから西に向かって測定された経度を示す 0 ～ 180 の数値を返します。 |

## <a name="examples"></a>例
野球フィールドでは、ピッチャーは、ピッチャーの塚からホーム ベースのキャッチャーにスマート フォンをスローします。 スマートフォンは、地面に対して平らに置かれており、画面の上部は、キャッチャーの方を向いています。また、ピッチャーは回転を一切加えません。 この位置でスマートフォンは、従量制課金の移動体通信ネットワーク サービスを利用できますが、WiFi は利用できません。 **PlayBall** 画面は表示されています。   

| 数式 | 説明 | 結果 |
| --- | --- | --- |
| **Location.Latitude** |現在位置の緯度を返します。 フィールドがマップの座標 47.591 N, 122.333 w です。 |47.591<br><br>ピッチャーからキャッチャーまでボールが移動する間、緯度は絶えず変化します。 |
| **Location.Longitude** |現在位置の経度を返します。 |122.333<br><br>ピッチャーからキャッチャーまでボールが移動する間、経度は絶えず変化します。 |
| **Location** |現在位置の緯度と経度をレコードとして返します。 |{&nbsp;Latitude:&nbsp;47.591, Longitude:&nbsp;122.333&nbsp;} |
| **Compass.Heading** |画面上部のコンパスの方位を返します。 このフィールドに、ホーム ベースは、ピッチャーの塚からおよそ南西部です。 |230.25 |
| **Acceleration.X** |デバイスの左右の加速度を返します。 ピッチャーは、スマートフォンを画面の上部に対してまっすぐに投げるので、デバイスの左右方向の加速度はゼロです。 |0 |
| **Acceleration.Y** |デバイスの前後の加速度を返します。 ピッチャーはデバイスを投げる際、最初に大きな加速度を与えます。時速 0 マイルの状態から 0.5 秒後には時速 90 マイル (毎秒 132 フィート) に達します。 デバイスが空中に放たれた後は、デバイスがそれ以上加速することはありません (空気摩擦は無視します)。 デバイスは減速し、キャッチャーが受けた時点で停止します。 |ピッチャーがデバイスを投げている間は 8.2 となります。<br><br>デバイスが空中にある間は 0 になります。<br><br>キャッチャーがデバイスを受けたときは、-8.2 になります。 |
| **Acceleration.Z** |デバイスの上下の加速度を返します。 空中を飛んでいるデバイスは重力の影響を受けます。 |ピッチャーがデバイスを投げる前は 0 です。<br><br>デバイスが空中にある間は 1 になります。<br><br>キャッチャーがデバイスを受けた後は 0 になります。 |
| **Acceleration** |加速度をレコードとして返します。 |{X:0、Y:264, Z:0} ピッチャーとして、デバイスがスローされます。 |
| **Connection.Connected** |デバイスがネットワークに接続されているかどうかを示すブール値を返します。 |**true** |
| **Connection.Metered** |従量制課金接続であるかどうかを示すブール値を返します。 |**true** |
| **App.ActiveScreen = PlayBall** |**PlayBall** が表示されているかどうかを示すブール値を返します。 |**true** |
| **App.ActiveScreen.Fill** |表示画面の背景色を返します。 |**Color.Green** |

