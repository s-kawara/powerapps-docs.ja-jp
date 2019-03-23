---
title: Concurrent 関数 | Microsoft Docs
description: 構文を含む PowerApps の Concurrent 関数の参照情報
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: anneta
ms.date: 06/26/2018
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: e9c63d1814b72cae0c675be6b33773799cfb3b8f
ms.sourcegitcommit: 5b2b70c3fc7bcba5647d505a79276bbaad31c610
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/22/2019
ms.locfileid: "58357094"
---
# <a name="concurrent-function-in-powerapps"></a>PowerApps の Concurrent 関数
複数の数式をそれぞれ同時に評価します。

## <a name="description"></a>説明
**Concurrent** 関数では、同時に複数の数式を評価します。 通常、複数の数式はと共にそれらを連鎖させることにより評価されます、 [ **;**](operators.md)演算子で、それぞれの順序で順番に評価されます。 アプリによって操作を同時に実行すると、同じ結果がユーザーに返されるまでの時間は短くなります。

アプリの [ **OnStart**](../controls/control-screen.md) プロパティで、**Concurrent** を使用すると、アプリがデータを読み込む際のパフォーマンスが向上します。 前の呼び出しが完了するまで、データ呼び出しが開始されない場合、アプリはすべての要求時間を合計した期間、待機する必要があります。 データ呼び出しが同時に開始される場合、アプリは最長の要求時間を待機するだけで済みます。 Web ブラウザーは、多くの場合、データ操作を同時に実行することによってパフォーマンスを向上させます。

**Concurrent** 関数内の数式が評価を開始および終了する順番は予測できません。 **Concurrent** 関数内の数式には、同じ **Concurrent** 関数内の他の数式との依存関係を含めないでください。それを行うと、PowerApps によってエラーが表示されます。 **Concurrent** 関数内にある数式は、この関数の外側にある数式に安全に依存することができます。外側にある数式は **Concurrent** 関数が開始する前に完了するからです。 後の数式、**同時**関数が数式内での依存を安全にすること: すべての前に完了します、**同時**関数が完了し、チェーン内の次の数式に上に移動します (場合します。使用して、 **;** 演算子)。 副作用がある関数またはサービス メソッドを呼び出す場合は、微妙な順序の依存関係に注意してください。

組み合わせて数式を連結することができます、 **;** への引数の中で演算子**同時**します。 たとえば、**Concurrent( Set( a, 1 ); Set( b, a+1 ), Set( x, 2 ); Set( y, x+2 ) )** は **Set( a, 1 ); Set( b, a+1 )** を **Set( x, 2 ); Set( y, x+2 )** と同時に評価します。 この場合、数式内の依存関係は問題ありません: **a** は **b** の前に設定されます。**x** は **y** の前に設定されます。

アプリが実行されているデバイスまたはブラウザーによっては、実際には少数の数式しか同時に評価されない可能性があります。 **Concurrent** は使用可能な機能を使用し、すべての数式が評価されるまで完了しません。

**[数式レベルのエラー管理]** (詳細設定) を有効にした場合、引数の順序で最初に発生したエラーが **Concurrent** から返されます。それ以外の場合は、”*空白*” が返されます。 すべての数式が成功すると、*true* が返されます。 1 つの数式が失敗した場合、その数式の残りの部分は停止しますが、他の数式は引き続き評価されます。

**Concurrent** は、[動作の数式](../working-with-formulas-in-depth.md)内でのみ使用できます。

## <a name="syntax"></a>構文
**Concurrent**( *Formula1*, *Formula2* [, ...] )

* *Formula(s)* - 必須。 同時に評価する数式の数。 2 つ以上の数式を指定する必要があります。

## <a name="examples"></a>例

#### <a name="loading-data-faster"></a>データの読み込みが速くなる

1. アプリを作成し、Common Data Service、SQL Server、または SharePoint から 4 つのデータ ソースを追加します。 

    この例では、[SQL Azure 上のサンプル Adventure Works データベース](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal)からの 4 つの表を使用します。 データベースを作成したら、完全修飾サーバー名 (たとえば、srvname.database.windows.net) を使用して PowerApps からデータベースに接続します。

    ![Azure 内の Adventure Works データベースに接続する](media/function-concurrent/connect-database.png)

2. **[[ボタン]](../controls/control-button.md)** コントロールを追加し、その **OnSelect** プロパティに次の式を設定します。

    ```powerapps-dot
    ClearCollect( Product, '[SalesLT].[Product]' );
    ClearCollect( Customer, '[SalesLT].[Customer]' );
    ClearCollect( SalesOrderDetail, '[SalesLT].[SalesOrderDetail]' ); 
    ClearCollect( SalesOrderHeader, '[SalesLT].[SalesOrderHeader]' )
    ```

3. [Microsoft Edge](https://docs.microsoft.com/microsoft-edge/devtools-guide/network) または [Google Chrome](https://developers.google.com/web/tools/chrome-devtools/network-performance/) で、アプリが実行されている間にネットワーク トラフィックを監視する開発者ツールを有効にします。

1. (省略可能) 帯域幅調整をオンにして、この比較の結果を強調します。

4. Alt キーを押しながら、ボタンを選択し、ネットワーク トラフィックを監視します。

    ツールには、次の例のように、順に実行された 4 つの要求が表示されます。  実際の時間は大幅に変動するため、削除されています。  グラフでは、各呼び出しは 1 つ前の呼び出しが完了してから開始されているのがわかります。

    ![4 つのネットワーク要求の時間グラフであり (各要求は 1 つ前の要求が終了してから開始されている)、期間全体をカバーしている](media/function-concurrent/chained-network.png)

5. アプリを保存し、閉じてから、もう一度開きます。

    PowerApps ではデータがキャッシュされるので、ボタンをもう一度選択しても 4 つの新しい要求が発生するとは限りません。 パフォーマンスをテストするたびに、アプリを閉じて再度開きます。 帯域幅調整がオンになっている場合、別のテストの準備が整うまで帯域幅調整をオフにしておきたい場合があります。

1. 2 つ目の **[[ボタン]](../controls/control-button.md)** コントロールを追加し、その **OnSelect** プロパティに次の式を設定します。

    ```powerapps-dot
    Concurrent( 
        ClearCollect( Product, '[SalesLT].[Product]' ), 
        ClearCollect( Customer, '[SalesLT].[Customer]' ),
        ClearCollect( SalesOrderDetail, '[SalesLT].[SalesOrderDetail]' ),
        ClearCollect( SalesOrderHeader, '[SalesLT].[SalesOrderHeader]' )
    )
    ```

    最初のボタンに対するものと同じ **ClearCollect** 呼び出しを追加しましたが、今回は **Concurrent** 関数内にラップされ、コンマで区切られていることに注目してください。

2. ブラウザーでネットワーク モニターをオフにします。

1. 帯域幅調整を以前に使用していた場合は、再度オンにします。

3. Alt キーを押しながら、2 番目のボタンを選択し、ネットワーク トラフィックを監視します。

    ツールには、次の例のように、同時に実行された 4 つの要求が表示されます。  繰り返しますが、実際の時間は大幅に変動するため、削除されています。  グラフでは、すべての呼び出しがほぼ同時に開始され、前の呼び出しが終了するまで待機していないことがわかります。

    ![4 つのネットワーク要求の時間グラフであり (4 つの要求は一緒に開始されている)、期間全体をカバーしている](media/function-concurrent/concurrent-network.png)

    これらのグラフは、同じスケールに基づいています。 **Concurrent** を使用することにより、これらの操作が完了するまでに要した合計時間を半減させることができます。 

5. アプリを保存し、閉じてから、もう一度開きます。

#### <a name="race-condition"></a>競合状態

1. [Microsoft Translator](../connections/connection-microsoft-translator.md) サービスへの接続をアプリに追加します。

2. [**[テキスト入力]**](../controls/control-text-input.md) コントロールを追加し、別の名前になっている場合は **TextInput1** に名前を変更します。

3. **[ボタン]** コントロールを追加し、その **OnSelect** プロパティに次の式を設定します。

    ```powerapps-dot
    Set( StartTime, Value( Now() ) );
    Concurrent(
        Set( FRTrans, MicrosoftTranslator.Translate( TextInput1.Text, "fr" ) ); 
            Set( FRTransTime, Value( Now() ) ),
        Set( DETrans, MicrosoftTranslator.Translate( TextInput1.Text, "de" ) ); 
            Set( DETransTime, Value( Now() ) )
    );
    Collect( Results,
        { 
            Input: TextInput1.Text,
            French: FRTrans, FrenchTime: FRTransTime - StartTime, 
            German: DETrans, GermanTime: DETransTime - StartTime, 
            FrenchFaster: FRTransTime < DETransTime
        }
    )
    ```

4. [**[データ テーブル]**](../controls/control-data-table.md) コントロールを追加し、その **Items** プロパティを **Results** に設定します。

1. 右側のウィンドウの **[プロパティ]** タブで、**[結果]** を選択して **[データ]** ウィンドウを開きます。

1. フィールドのリストで、データ テーブル内にすべてのフィールドが表示されるように各フィールドのチェック ボックスをオンにします。

1. (省略可能) **[入力]** フィールドをリストの先頭にドラッグし、**FrenchFaster** フィールドをリストの一番下にドラッグします。

    ![結果コレクション内のフィールドのリスト](media/function-concurrent/field-list.png) 

6. **[テキスト入力]** コントロールで、翻訳する語句を入力するか貼り付けます。

7. Alt キーを押しながら、ボタンを複数回選択してテーブルに入力します。

    時間はミリ秒単位で表示されます。
  
    ![文字列 "Hello World" をフランス語とドイツ語に翻訳した結果が含まれるデータ テーブルの表示。 フランス語への翻訳がドイツ語への翻訳より速い場合もあれば、逆の場合もあります。](media/function-concurrent/race-condition.png) 

    場合によっては、フランス語への翻訳はドイツ語への翻訳よりも速く行われます。その逆もあります。 両方が同時に開始されても、ネットワーク待機時間やサーバー側の処理など、さまざまな理由により、一方の翻訳が他方の翻訳よりも前に返されます。

    アプリが最初に終了した 1 つの翻訳に依存している場合は、[競合状態](https://en.wikipedia.org/wiki/Race_condition)が発生します。 さいわいにも、PowerApps では、検出できるほとんどのタイミングの依存関係にフラグを付けています。
