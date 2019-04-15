---
title: キャンバス アプリのデータ ソースについて | Microsoft Docs
description: キャンバス アプリの接続とデータ ソースの操作に関する参照情報。
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: anneta
ms.date: 03/08/2017
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 9e31ae7600663daa694b46376008161502c9c428
ms.sourcegitcommit: 825daacc9a812637815afc1ce6fad28f0cebd479
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2019
ms.locfileid: "57803414"
---
# <a name="understand-data-sources-for-canvas-apps-in-powerapps"></a>PowerApps でのキャンバス アプリのデータ ソースについて

PowerApps では、ほとんどのキャンバス アプリが、**データ ソース**と呼ばれるクラウド サービスに格納されている外部情報を使用します。 一般的な例は、OneDrive for Business に格納されている Excel ファイル内のテーブルです。 アプリは、**接続**を使用してこれらのデータ ソースにアクセスします。

この記事では、さまざまな種類のデータ ソースと、テーブル データ ソースの操作方法について説明します。

データ ソースに対する基本的な読み取りと書き込みを実行するアプリを作成するのは簡単です。 しかし、アプリのデータの入出力を細かく制御することが必要になる場合があります。  この記事では、**[Patch](functions/function-patch.md)**、**[DataSourceInfo](functions/function-datasourceinfo.md)**、**[Validate](functions/function-validate.md)**、**[Errors](functions/function-errors.md)** 関数を使用してより細かな制御を実現する方法について説明します。

## <a name="kinds-of-data-sources"></a>データ ソースの種類

データ ソースは、クラウド サービスに接続することも、アプリに対してローカルに配置することもできます。

### <a name="connected-data-sources"></a>接続されているデータ ソース

最も一般的なデータ ソースは**テーブル**で、情報の取得と保存に使用できます。 データ ソースへの**接続**を使用すれば、Microsoft Excel ブック、SharePoint リスト、SQL テーブル、その他多くの形式でデータの読み書きを行えます。それらのデータは、OneDrive for Business、DropBox、SQL Server などのクラウド サービスに格納できます。

テーブル以外のデータ ソースには、電子メール、予定表、Twitter、通知が含まれますが、この記事ではこのような他の種類のデータ ソースについては説明しません。

### <a name="local-data-sources"></a>ローカル データ ソース

**[ギャラリー](controls/control-gallery.md)**、**[表示フォーム](controls/control-form-detail.md)**、**[編集フォーム](controls/control-form-detail.md)** コントロールを使用すると、データ ソースからデータを読み書きするアプリを簡単に作成できます。  最初に、[データ フォームについて](working-with-forms.md)の記事をご覧ください。  

データからアプリを作成するよう PowerApps に要求すると、これらのコントロールが使用されます。 その背後で、アプリは、データ ソースから取得したデータを格納して操作するために内部テーブルを使用します。

特別な種類のデータ ソースに[コレクション](working-with-data-sources.md#collections)があります。コレクションは、アプリに対してローカルであり、クラウドのサービスへの接続に基づきません。したがって、同じユーザーのデバイス間または複数のユーザー間で情報を共有することはできません。 コレクションの読み込みと保存はローカルで行うことができます。

### <a name="kinds-of-tables"></a>テーブルの種類

PowerApps アプリの内部テーブルは、数や文字列が値であるのと同じように固定値を保持します。 内部テーブルはどこにも格納されず、アプリのメモリにのみ存在します。 テーブルの構造とデータを直接変更することはできません。 その代わり、数式を使用して新しいテーブルを作成することができます。その数式を使用して、元のテーブルに変更を加えたコピーを作成します。

外部テーブルはデータ ソースに格納され、後で取得して共有することができます。  PowerApps は、格納されたデータを読み書きするための "接続" を提供します。  接続内では、複数の情報テーブルにアクセスできます。  アプリで使用するテーブルを選択すると、それぞれのテーブルが別個の "*データ ソース*" になります。  

[作業テーブル](working-with-tables.md)に関するページで内部テーブルについて詳しく説明されていますが、その説明はクラウド サービスに存在する外部テーブルにも当てはまります。

## <a name="working-with-tables"></a>テーブルの操作
テーブルのデータ ソースは、PowerApps の内部テーブルと同じ方法で使用できます。  各データ ソースには、内部テーブルと同じように、[レコード](working-with-tables.md#records)、[列](working-with-tables.md#columns)、数式で使用できるプロパティがあります。 さらに、次の条件があります。

* データ ソースの列名とデータ型は、接続の基になるテーブルと同じになります。
  
    > [!NOTE]
  > 名前にスペースが使われている列を含む SharePoint および Excel のデータ ソースの場合、PowerApps ではスペースが **"\_x0020\_"** に置き換えられます。 たとえば、SharePoint または Excel の **"Column Name"** は、PowerApps のデータ レイアウトに表示されるときや数式で使用されるときは **"Column_x0020_Name"** と表示されます。
* データ ソースは、アプリが読み込まれるときにサービスから自動的に読み込まれます。  **[Refresh](functions/function-refresh.md)** 関数を使用して、強制的にデータを更新できます。
* ユーザーはアプリを実行するとき、レコードを作成、変更、削除して、その変更をサービスの基になるテーブルにプッシュ転送できます。
  * レコードを作成するには、**[Patch](functions/function-patch.md)** 関数と **[Collect](functions/function-clear-collect-clearcollect.md)** 関数を使用します。  
  * レコードを変更するには、**[Patch](functions/function-patch.md)** 関数、**[Update](functions/function-update-updateif.md)** 関数、**[UpdateIf](functions/function-update-updateif.md)** 関数を使用します。
  * レコードを削除するには、**[Remove](functions/function-remove-removeif.md)** 関数と **[RemoveIf](functions/function-remove-removeif.md)** 関数を使用します。
  * データ ソースの操作に関するエラーは、**[Errors](functions/function-errors.md)** 関数を介して利用できます。
* **[DataSourceInfo](functions/function-datasourceinfo.md)** 関数、**[Defaults](functions/function-defaults.md)** 関数、**[Validate](functions/function-validate.md)** 関数は、ユーザー エクスペリエンスを最適化するために使用できる、データ ソースに関する情報を提供します。

### <a name="creating-data-sources"></a>データ ソースの作成
PowerApps を使用して、接続されたデータ ソースを作成したり、データ ソースの構造を変更したりすることはできません。データ ソースは、既にいずれかのサービスに存在している必要があります。 たとえば、OneDrive に保存された Excel ブックにテーブルを作成するには、最初に OneDrive で Excel Online を使用してブックを作成します。 次に、アプリからそのブックへの接続を作成します。  

コレクションのデータ ソースは、アプリ内で作成と変更を "*行えます*" が、これは一時的なものです。

### <a name="display-one-or-more-records"></a>1 つまたは複数のレコードの表示
![](media/working-with-data-sources/reading-from-a-datasource.png) 上の図は、アプリがデータ ソース内の情報を読み取るときの情報の流れを示しています。

* 情報は、ストレージ サービス (この場合は Office 365 サイトの SharePoint リスト) を介して保存され、共有されます。
* 接続により、この情報をアプリで利用できるようになります。  接続は、情報にアクセスするためのユーザーの認証を処理します。
* アプリが起動されるか、**[Refresh](functions/function-refresh.md)** 関数が押されると、接続から情報がアプリのデータ ソースに取得され、ローカルで使用できるようになります。
* 数式は、情報を読み取り、その情報をユーザーに表示されるコントロールに公開するために使用されます。 データ ソースのレコードを表示するには画面と配線にギャラリーを使用して、 **[項目](controls/properties-core.md)** プロパティをデータ ソース。**Gallery.Items = DataSource**します。  コントロールの **[Default](controls/properties-core.md)** プロパティを使用して、ギャラリー内のコントロールをギャラリーに関連付けます。  
* データ ソースは、テーブルでもあります。  したがって、データ ソースを全体として使用する前に、**[Filter](functions/function-filter-lookup.md)**、**[Sort](functions/function-sort.md)**、**[AddColumns](functions/function-table-shaping.md)**、その他の関数を使用して、改良と拡張を行えます。  また、**[Lookup](functions/function-filter-lookup.md)**、**[First](functions/function-first-last.md)**、**[Last](functions/function-first-last.md)** などの関数を使用して、個々のレコードを操作することもできます。

### <a name="modify-a-record"></a>レコードの変更
前のセクションでは、データ ソースを読み取る方法を説明しました。  ここで、上の図に示されている矢印が一方向であることに注意してください。  データ ソースに加えられた変更は、データを取得したのと同じ数式を介してプッシュ転送されません。  代わりに、新しい数式が使用されます。  多くの場合 (特にモバイル デバイス上で)、レコードの編集用には、レコードを閲覧するための画面とは異なる画面が使用されます。

データ ソースの既存のレコードを変更するには、そのレコードがデータ ソースから取得されている必要があります。  レコードは、ギャラリー、[コンテキスト変数](working-with-variables.md#use-a-context-variable)、任意の数の数式を経由している可能性がありますが、その取得元はデータ ソースまでさかのぼることができる必要があります。  レコードを一意に識別する追加情報がレコードに付属することで変更対象のレコードが正しいことが保証されるため、これは重要なことです。    

![](media/working-with-data-sources/writing-to-a-datasource.png) 上の図は、データ ソースを更新するための情報の流れを示しています。

* **[編集フォーム](controls/control-form-detail.md)** コントロールは、入力カードのコンテナーを提供します。入力カードは、テキスト入力コントロール、スライダーなどのユーザー入力コントロールで構成されます。  **[DataSource](controls/control-form-detail.md)** プロパティと **[Item](controls/control-form-detail.md)** プロパティは、編集するレコードを識別するために使用します。
* 各入力カードには **[Default](controls/properties-core.md)** プロパティがあります。このプロパティは、通常はフォームの **ThisItem** レコードのフィールドに設定されます。  入力カード内のコントロールは、**[Default](controls/properties-core.md)** から入力値を受け取ります。  通常はこれを変更する必要はありません。
* 各入力カードは、**[Update](controls/control-card.md)** プロパティを公開します。  このプロパティは、ユーザーの入力を、データ ソースに書き戻すために、レコードの特定のフィールドにマップします。  通常はこれを変更する必要はありません。
* 画面上のボタンまたはイメージ コントロールを使用すると、ユーザーがレコードに加えた変更を保存できます。  そのためには、コントロールの **[OnSelect](controls/properties-core.md)** 数式で **[SubmitForm](functions/function-form.md)** 関数を呼び出します。  **[SubmitForm](functions/function-form.md)** を使用すると、カードのすべての **[Update](controls/control-card.md)** プロパティを読み取り、これを使用してデータ ソースに書き戻すことができます。
* 場合によっては問題が発生することがあります。  たとえば、ネットワーク接続が切断されている場合や、アプリが認識できないサービスによって検証チェックが行われている場合があります。  フォーム コントロールの **Error** プロパティと **[ErrorKind](controls/control-form-detail.md)** プロパティを使用すると、この情報が利用可能になり、ユーザーに表示できるようになります。  

プロセスをより細かく制御するために、**[Patch](functions/function-patch.md)** 関数と **[Errors](functions/function-errors.md)** 関数を使用することもできます。  **[編集フォーム](controls/control-form-detail.md)** コントロールでは **[Update](controls/control-form-detail.md)** プロパティが公開されるため、フォーム内のフィールドの値を読み取ることができます。  さらに、**Patch** 関数と **SubmitForm** 関数を完全にバイパスして、このプロパティを使用して接続上でカスタム コネクタを呼び出すこともできます。

### <a name="validation"></a>検証
アプリでは、レコードに変更を加える前に、変更が許容されるかどうかを確認する必要があります。  これには 2 つの理由があります。

* "*ユーザーへの即座のフィードバック*"。  問題を修正するのに最適なタイミングは、ユーザーの記憶に新鮮な、その問題が発生したときです。  実際、タッチ操作またはキー入力ごとに、入力の問題を示す赤いテキストを表示できます。
* "*ネットワーク トラフィックの削減とユーザーの待ち時間の短縮*"。  アプリで問題を多く検出できれば、問題を検出して解決するためのネットワーク経由の会話を減らすことができます。  この会話を行うのに時間がかかり、ユーザーは処理を進めるのにその都度待たなければなりません。

PowerApps には、検証用に 2 つのツールが用意されています。

* データ ソースは、有効な値と有効でない値に関する情報を提供できます。  たとえば、数値に最小値と最大値を設定したり、1 つ以上のエントリを必須に設定したりできます。  この情報には、**[DataSourceInfo](functions/function-datasourceinfo.md)** 関数を使用してアクセスできます。  
* **[Validate](functions/function-validate.md)** 関数では、これと同じ情報を使用して、1 つの列またはレコード全体の値を確認できます。

### <a name="error-handling"></a>エラー処理
これまでの操作で、レコードを検証することができました。  次は、**[Patch](functions/function-patch.md)** を使用してそのレコードを更新します。

しかし、残念ながら、まだ問題があります。  アプリは、たとえば、ネットワークがダウンしている、サービスでの検証に失敗した、ユーザーが適切なアクセス許可を持っていない、などのエラーに遭遇する可能性があります。  アプリでは、エラー状況に適切に対応して、フィードバックとエラー状況を解決するための手段をユーザーに提供する必要があります。  

データ ソースでエラーが発生すると、アプリは自動的にエラー情報を記録し、これを **[Errors](functions/function-errors.md)** 関数を介して使用できるようにします。  エラーは、問題が発生したレコードに関連付けられます。  それがユーザーによって修正可能な問題 (たとえば、検証の問題) なら、レコードを送信し直すことでエラーが解決します。

**[Patch](functions/function-patch.md)** または **[Collect](functions/function-clear-collect-clearcollect.md)** を使用してレコードが作成されたときにエラーが発生した場合、エラーが関連付けられるレコードはありません。  その場合、**[Patch](functions/function-patch.md)** によって "*空白*" が返され、これを **[Errors](functions/function-errors.md)** のレコード引数として使用できます。  作成エラーは次の操作で解決されます。

**[Errors](functions/function-errors.md)** 関数からは、エラー情報のテーブルが返されます。  特定の列にエラーの原因があると考えられる場合は、この情報に列情報を含めることができます。  列レベルのエラー メッセージは、編集画面上の列の近くにあるラベル コントロールで使用します。  エラー テーブルの **Column** が "*空白*" であるレコード レベルのエラー メッセージは、レコード全体の **[保存]** ボタンの近くの場所で使用します。  

### <a name="working-with-large-data-sources"></a>大規模なデータ ソースの操作
(数百万件のレコードが含まれる) 大規模なデータ ソースからレポートを作成する場合は、ネットワーク トラフィックが最小限になるように考慮する必要があります。 たとえば、ニューヨーク市に居住する、StatusCode が "Platinum" であるすべての顧客を報告するとします。 この顧客テーブルには、数百万件のレコードが含まれているとします。

この場合、数百万人の顧客レコードをアプリに取り込んだ後で目的のレコードを見つけることは**しません**。 代わりに、テーブルが格納されているクラウド サービス内でその選択操作を行い、選択されたレコードのみをネットワーク経由で送信するようにします。

レコードを選択するために使用できる関数の多く (すべてではありません) は "*委任*" することができます。つまり、これらの関数をクラウド サービス内で実行できます。 その方法については、[委任](delegation-overview.md)に関するページを参照してください。

## <a name="collections"></a>コレクション
コレクションは、特別な種類のデータ ソースです。  コレクションは、アプリに対してローカルであり、クラウドのサービスへの接続に基づきません。したがって、同じユーザーのデバイス間または複数のユーザー間で情報を共有することはできません。  コレクションは他のデータ ソースと同様に動作しますが、いくつかの例外があります。

* コレクションは、**[Collect](functions/function-clear-collect-clearcollect.md)** 関数を使用して動的に作成できます。  コレクションは、接続ベースのデータ ソースとは異なり、事前に確立する必要はありません。
* コレクションの列は、**[Collect](functions/function-clear-collect-clearcollect.md)** 関数を使用していつでも変更できます。
* コレクションでは、重複するレコードが許可されます。  コレクションでは、同じレコードのコピーが複数個存在できます。  **All** 引数が指定されていない限り、**[Remove](functions/function-remove-removeif.md)** などの関数は最初に見つかった一致に対して動作します。
* **[SaveData](functions/function-savedata-loaddata.md)** 関数と **[LoadData](functions/function-savedata-loaddata.md)** 関数を使用して、コレクションのコピーの保存と再読み込みを行うことができます。  情報は、他のユーザー、アプリ、またはデバイスがアクセスできないプライベートな場所に保存されます。 
* **[エクスポート](controls/control-export-import.md)** コントロールと **[インポート](controls/control-export-import.md)** コントロールを使用して、ユーザーが操作できるファイルとの間でコレクションのコピーの保存と再読み込みを行うことができます。  

データ ソースとしてのコレクションの操作方法の詳細については、[コレクションの作成と更新](create-update-collection.md)に関するページを参照してください。

コレクションは通常、アプリのグローバルな状態を保持するために使用します。  状態を管理するために使用できるオプションについては、[変数の操作](working-with-variables.md)に関するページを参照してください。

