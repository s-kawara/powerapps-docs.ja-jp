---
title: HTTP および HTTPS リソースと非同期にやり取りする | MicrosoftDocs
description: モデル駆動型アプリの JavaScript クライアント拡張を作成する場合は、HTTP リソースおよび HTTPS リソースと非同期に対話する必要があります。
services: ''
suite: powerapps
documentationcenter: na
author: jowells
manager: austinj
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/20/2018
ms.author: jowells
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="interact-with-http-and-https-resources-asynchronously"></a>HTTP および HTTPS リソースを非同期に操作

**カテゴリ**: パフォーマンス

**影響の可能性**: 高い

<a name='symptoms'></a>

## <a name="symptoms"></a>現象

同期要求は、次のことが発生する原因となる可能性のある、そのほかのスクリプトの実行をブロックします:

- モデル駆動アプリおよびキャンバス アプリが応答しない
- クライアント対話が遅くなる

<a name='guidance'></a>

## <a name="guidance"></a>ガイダンス

可能な場合に HTTP および HTTPS リソースと非同期にやり取りします。 ユーザーは、実際のページの読み込み時間または認識したページの読み込み速度が改善したことに気がつきます。 ページの応答性も向上します。

次のオプションを最新のブラウザーで選択して、サービスと非同期的にやり取りすることができます。

> [!NOTE]
> 非同期のやり取りを追加するには、同期のやり取りとは異なるスタイルの設計が必要です。 コールバックは非決定論的な順序で実行できます。これは、ページ フローおよび整合性が常に正しいことを確認するためのより複雑な設計が必要になることを意味します。 たとえば、すべての依存サービスの呼び出しが戻るまで管理が有効にならないようにするための対策を講じる必要があります。 いくつかの追加手順を踏まえることで、より快適なユーザー エクスペリエンスを実現することができます。

- 従来のリボン ルールが同期要求で作成されるのは、true/false を返す必要があるためです。 統一インターフェイスは、ブール値よりも Promise を返すことをサポートします。これにより、リボン ルールが非同期のネットワーク要求を出すことができます。 詳細については、[リボンの有効化ルールの定義](/powerapps/developer/model-driven-apps/define-ribbon-enable-rules#custom-rule) を参照してください。

- [`XMLHttpRequest`](https://developer.mozilla.org/docs/Web/API/XMLHttpRequest) 非同期パラメーターが省略されているか、true に設定されている

  ```javascript
  // Missing the async parameter, which is the third parameter. It defaults to true, which is the value you want.
  var requestXhr = new XMLHttpRequest();
  requestXhr.open('GET', '/test/test.txt');

  // Explicitly setting the async parameter.
  requestXhr.open('GET', '/test/test.txt', true);
  ```

- [フェッチ](https://developer.mozilla.org/docs/Web/API/Fetch_API) API の使用

  > [!IMPORTANT]
  > このオプションに進む前に、カスタマイズの操作に使用するブラウザーのサポートが利用できることを確認します。 [フェッチ](https://developer.mozilla.org/docs/Web/API/Fetch_API) ドキュメントの **ブラウザーの互換性** セクションを確認します。

<a name='problem'></a>

## <a name="problematic-patterns"></a>問題となるパターン

サーバーと対話する方法、またはリソースを要求する方法は複数あります。 同期通信を有効にする一般的な方法には次のものが含まれます:

> [!WARNING]
> これらのシナリオを回避する必要があります。

- `open` 関数呼び出しの `async` パラメーター値に `false` を渡す `XMLHttpRequest` オブジェクトを使用する

  ```javascript
  var requestXhr = new XMLHttpRequest();

  // Explicitly setting the async parameter to false or supplying a variable with a value of false will force this as a synchronous call.
  requestXhr.open('GET', '/test/test.txt', false);
  ```

- `async` パラメーター値に `false` を渡す [`jQuery`](https://www.jquery.com) [`ajax` 関数](http://api.jquery.com/jquery.ajax/) を使用する

  ```javascript
  // Explicitly setting the async parameter to false or supplying a variable with a value of false will force this as a synchronous call.
  var requestAjax = $.ajax({ async: false, url: '/test/test.txt' });
  ```

- Dynamics 365 サービスとのやり取りに固有です。製品との一般的なやり取りのための明示的な操作を提供する JavaScript ライブラリがあります。 一般的なライブラリには次のものがあります（ただし、これらに限られません）: [`SDK.REST.js`](https://msdn.microsoft.com/library/gg334427(v=crm.7).aspx#BKMK_SDKREST), [`SDK.Soap.js`](https://code.msdn.microsoft.com/sdksoapjs-9b51b99a) および [`XrmServiceToolkit.js`](https://github.com/XrmServiceToolkit/XrmServiceToolkit)。
  - これには、同期の操作のみをサポートする関数があります。それ以外では、パラメーターとしてコールバック関数を渡して非同期を true に設定する必要があります。 ほとんどの既定の動作では、`XMLHttpRequest` オブジェクトのオープン呼び出しに対して、基盤となる非同期パラメーターを false に設定します。

<a name='additional'></a>

## <a name="additional-information"></a>追加情報

### <a name="performance"></a>パフォーマンス

ブラウザーは単一スレッドでスクリプトを解釈します。 スレッドを使用してプロセスを非同期的に実行する場合、ブラウザーはプロセスが完了するまでの間ユーザーの対話に応答しません（「フリーズします」）。 同期呼び出しでは、複数のやり取りを同時に実行できる機能も削除され、実際には、すべての呼び出しが強制的に順次処理されます。 多くの場合、これがユーザーのフラストレーションにつながります。 非同期サービス呼び出しを組み込むことで、ユーザーの応答性を最適化します。

### <a name="browser-support"></a>ブラウザーのサポート

`XMLHttpRequest` の仕様には、同期的な使用は廃止されるため標準から削除されると記載されています。 現在、ブラウザーには警告のみ表示されますが、今後は、値 false が非同期パラメーターに渡された場合は `InvalidAccessError` 例外がスローされる可能性があります。 最新のブラウザーでは、メイン スレッドで実行される同期要求は廃止済みとして宣言されました。

> [!NOTE]
> 同期処理のオプションを提供しない最新の API が導入されています。 詳細については、[API の取得](https://developer.mozilla.org/docs/Web/API/Fetch_API) のドキュメントを参照してください。

### <a name="windowsettimeout"></a>window.setTimeout

`window.setTimeout` 関数へのパラメーターとしてスクリプト ブロックを含めてページ実行の標準の同期フローを分割しても、並列処理は実現しません。

```javascript
window.setTimeout(
    function () {
        var oReq = new XMLHttpRequest();
        oReq.open('GET', '/test/action', false);
    }, 0);
```

この例の方法では、ブラウザーをロックして、主要ブラウザーの UI スレッド上で処理を行います。

<a name='seealso'></a>

### <a name="see-also"></a>関連項目

[リボンの有効化ルールの定義](/powerapps/developer/model-driven-apps/define-ribbon-enable-rules#custom-rule)
[XMLHttpRequest](https://docs.microsoft.com/microsoft-edge/dev-guide/performance/xmlhttprequest)<br />
[XMLHttpRequest 仕様 (同期廃止文あり)](https://xhr.spec.whatwg.org/#the-open()-method)<br />
[フェッチ API 仕様](https://fetch.spec.whatwg.org/#fetch-api)<br />
[フェッチ API](https://developer.mozilla.org/docs/Web/API/Fetch_API)
