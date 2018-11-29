---
title: 'ベストプラクティス: モデル駆動型アプリにおけるクライアント スクリプト | MicrosoftDocs'
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: article
applies_to:
  - Dynamics 365 (online)
ms.assetid: 16271bd8-cfa8-4a7f-802a-60fbff7c3722
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="best-practices-client-scripting-in-model-driven-apps"></a>ベストプラクティス: モデル駆動型アプリにおけるクライアント スクリプト



これらは、モデル駆動型アプリの JavaScript コードを記述する際に考慮すべきベスト プラクティスとなるヒントの一部です。

## <a name="define-unique-javascript-function-names"></a>一意のJavaScript 関数名を定義する

JavaScript ライブラリ内で使用する関数を記述する場合は、その関数を他の JavaScript ライブラリと共にフォームに読み込むことができます。 指定した関数と同じ名前の関数が他のライブラリに含まれている場合は、そのページに対してどちらの関数を読み込むかが定義されます。 設計した関数が他のライブラリの関数によって上書きされないようにするには、設計した関数に一意の名前を付ける必要があります。 次のストラテジーを使用できます:

- **一意な関数プレフィックス**: 次の例に示すように、一意の命名規則を含む標準の構文で一貫性のある名前を使用して各関数を定義します。
    ```JavaScript
    function MyUniqueName_performMyAction()
    {
        // Code to perform your action.
    }
    ```
- **ネームスペースライブラリの名前**: 次の例に示すように、各関数を JavaScript オブジェクトに関連付けて、関数を呼び出す場合に使用する一種の名前空間を作成します。
    ```JavaScript
    //If the MyUniqueName namespace object isn’t defined, create it.
    if (typeof (MyUniqueName) == "undefined")
       { MyUniqueName = {}; }
       // Create Namespace container for functions in this library;
       MyUniqueName.MyFunctions = {
         performMyAction: function(){
         // Code to perform your action.
         //Call another function in your library
         this.anotherAction();
       },
       anotherAction: function(){
         // Code in another function
      }
    };
    ```

    これにより、関数を使用するときにフル ネームを指定できます。 次の例はこのことを示しています。

    ```JavaScript
    MyUniqueName.MyFunctions.performMyAction();
    ```

    別の関数内の関数を呼び出す場合は、両方の関数を格納するオブジェクトへのショートカットとしてこのキーワードを使用できます。 ただし、関数がイベント ハンドラーとして使用されている場合、 このキーワードはイベントが発生しているオブジェクトを参照します。

## <a name="avoid-using-unsupported-methods"></a>サポートされないメソッドを使用しない

インターネットでは、サポートされていないメソッドを使用するさまざまな例や提案があります。 これらは、ページ コントロールに文書化されていない内部関数を活用するものもあります。 これらのメソッドは機能するかもしれませんが、サポートされていないため、モデル駆動型アプリの将来のバージョンでも引き続き使用できるとは期待できません。

## <a name="avoid-using-jquery-for-form-scripts"></a>フォーム スクリプトに jQuery の使用を避ける

フォーム スクリプトおよびリボン コマンドで jQuery を使用することをお勧めしません。 jQuery が提供する最大の益は、DOM のクロスブラウザー操作が簡単になることです。 これにより、フォーム スクリプトとリボン コマンドは明示的にサポートされていません。 スクリプトを制限して、[Xrmオブジェクト モデル](understand-clientapi-object-model.md)で使用可能なオブジェクトおよびメソッドを使用します。 

モデル駆動型アプリで有用な jQuery のそのほかの機能を使用し、**$.ajax** を使用する機能を含めることにした場合、次のことを考慮します。

- 最良のパフォーマンスを得るには、必要でない場合はページで jQuery をロードしないでください。
- モデル駆動型アプリ Web サービスに対して要求を実行するために **$.ajax** を使用することはサポートされていますが、代替手段があります。 **$.ajax** を使用する代替策は、ブラウザーの **XMLHttpRequest** オブジェクトを直接使用することです。 jQuery **$.ajax** メソッドは、このオブジェクトのラッパーのみです。 ネイティブ **XMLHttpRequest** オブジェクトを直接使用する場合、jQuery を読み込む必要はありません。
- ページに読み込まれる jQuery の各バージョンは、違うバージョンの場合があります。 jQuery のさまざまなバージョンはさまざまな動作をするので、jQuery の複数バージョンが同じページで読み込まれるときは、問題が発生する可能性があります。 これはこの問題を軽減する手法ですが、jQuery ライブラリおよび jQuery に依存する他のライブラリの編集によって異なります。


## <a name="write-your-code-for-multiple-browsers"></a>複数のブラウザーで コード を記述する

モデル駆動型アプリは複数のブラウザーをサポートします。 使用する任意のスクリプトが、サポートされているすべてのブラウザーで機能することを確認してください。 Internet Explorer と他のブラウザーの重要な違いのほとんどは、HTML および XML DOM の操作と関係しています。 HTML DOM の操作がサポートされていないため、スクリプト ロジックだけがサポートされる操作を実行し、[Xrm オブジェクトモデル](understand-clientapi-object-model.md) を使用している場合、他のブラウザーをサポートするために大きな変更は必要ではありません。 
