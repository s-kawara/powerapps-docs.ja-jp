---
title: window.top の使用を回避 | MicrosoftDocs
description: JavaScript のカスタマイズで window.top を使用することと関連する、スクリプトエラーと誤ったアプリケーション動作を回避する方法について説明します。
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
ms.date: 1/15/2019
ms.author: jowells
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="avoid-using-windowtop"></a>window.top を使用しないでください

**カテゴリ**: サポート可能性、アップグレードの準備、オンライン移行

**影響の可能性**: 高い

<a name='symptoms'></a>

## <a name="symptoms"></a>現象

- 次のスクリプト エラーがユーザーに表示されるか、またはエラー ログに含まれます: `Error: Blocked a frame with origin "https://<yourinstance>.dynamics.com" from accessing a cross-origin frame.`
- Dynamics 365 App for Outlook、Dynamics 365 for phones and tablets、または Iframe 内でアプリ用 Common Data Service をホストする外部アプリケーションのコンテキストでは、カスタマイズが正しく動作しない場合があります。

  > [!NOTE]
  > エラー処理がエラーをマスクしてスクリプト処理を続行する場合、予期しない動作を引き起こす可能性があります。

<a name='guidance'></a>

## <a name="guidance"></a>ガイダンス

Dynamics 365 App for Outlook、Dynamics 365 for phones and tablets、または Iframe 内でアプリ用 Common Data Service をホストする外部アプリケーションのコンテキストで動作しているスクリプトで `window.top` を使用しないでください。 これらのシナリオが現在は組織に当てはまらないとしても、`window.top` を使わないようにするか、この問題を回避してください。

 > [!IMPORTANT]
 > `window.parent` または親階層のバリエーション（例えば `window.parent.parent`）を使用した場合も同様の症状が発生する可能性があります。

推奨されている方法を次に示します:

- `window.top` オブジェクトの使用を完全に避けてください。

- `window.top` を使用することが唯一可能なオプションである場合は、まず以下のスクリプトを使用して `window.top` にアクセス可能か判断するためにテストをしてください。 これを利用できない場合は、代わりのロジックまたは代替ユーザー エクスペリエンスを提供してください。

  > [!NOTE]
  > あくまで `window.top` を使わないことをお勧めしますが、このスクリプトはそれが唯一の可能なオプションである特殊なケースに含まれています。

    ```javascript
    function isTopAccessible() {
        try {
                window.top.location;
                return true;
            }
            catch (err) {
                return false;
            }
        }
    }

    var canAccess = isTopAccessible();
    alert(canAccess);
    ```

<a name='problem'></a>

## <a name="problematic-patterns"></a>問題となるパターン

可能な限り、いかなる `window.top` の使用も避ける必要があります。 以下は一般的なパターンの例です。

> [!WARNING]
> これらのシナリオを回避する必要があります。

```javascript
// Getting or setting variables at the top level
var myValue = window.top.myGlobalVariable;

// Attempting to access the Xrm namespace at the top level
myValue = window.top.Xrm.Page.getAttribute("field1");
```

<a name='additional'></a>

## <a name="additional-information"></a>追加情報

前述のシナリオで `window.top` は Dynamics 365 の外部のアプリケーション コンテキストが所有するウィンドウを参照します。 オリジンが異なるため、ブラウザはユーザーにクロス オリジン セキュリティ エラーを提示します。

### <a name="see-also"></a>関連項目
[JavaScript を使用するモデル駆動型アプリでクライアント スクリプトを使用してビジネス ロジックを適用](/powerapps/developer/model-driven-apps/client-scripting)<br/>
[モデル駆動型アプリのフォームとグリッド内のイベント](/powerapps/developer/model-driven-apps/clientapi/events-forms-grids)<br/>