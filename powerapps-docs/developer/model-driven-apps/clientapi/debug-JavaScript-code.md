---
title: モデル駆動型アプリ用 JavaScript コードのデバッグ | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: conceptual
applies_to:
  - Dynamics 365 (online)
ms.assetid: 3edad039-4397-4984-a29b-9307a7a2aaee
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="debug-your-javascript-code-for-model-driven-apps"></a>モデル駆動型アプリ用 JavaScript コードのデバッグ



各ブラウザーは特定の種類のデバッグ拡張機能を提供します。 Microsoft Edge および Internet Explorer には、モデル駆動型アプリ内のスクリプトをデバッグするために使用可能な F12 開発者ツールが用意されています。 F12 開発者ツールは、Microsoft Edge または Internet Explorer を使用してページを表示するときに F12 を押すと開くことができます。 詳細については、[F12 開発者ツール ガイド](https://docs.microsoft.com/microsoft-edge/f12-devtools-guide) を参照してください。

Google Chrome の場合は、F12 を押して開発者ツールを開きます。 Firebug は、Mozilla Firefox を使用する Web 開発の一般的なブラウザー拡張機能です。 Apple Safari では、最初に**高度な設定**の**開発を表示**メニューを選択する必要があります。 次に**開発**メニューから **Web 検査の表示**を選択できます。

モデル駆動型アプリで JavaScript ライブラリを使用するとき、ライブラリは Web ページでロードされます。 デバッグ環境では、自分の特定なライブラリを分離することが困難な場合があります。 Microsoft Edge でデバッグ ツールを使用している場合、**デバッガー**タブで、左上隅でフォルダー アイコンをクリックして、使用可能なスクリプトを展開し、次に示す **new_myCustomJavaScript.js** Web リソースなど JavaScript Web リソース名に対応する名前を持つスクリプトを検索します。 検索ボックスにファイル名を入力することにより、JavaScript ライブラリも検索できます。

![JavaScript のデバッグ](../media/form-script-debugging.png)

さまざまなブラウザーのデバッグ ツールは、同様の機能を備えています。 ライブラリを見つけたら、ブレーク ポイントを設定し、コードが実行する原因となるイベントを再作成します。

また、JavaScript コードのデバッグの詳細については、当チーム ブログ サイトのブログ投稿、[ブログ: ブラウザの開発者ツールを使用して CRM でカスタム JavaScript コードをデバッグする](https://blogs.msdn.microsoft.com/crm/2015/11/29/debugging-custom-javascript-code-in-crm-using-browser-developer-tools/) を参照してください。

## <a name="select-appropriate-frame-to-debug-your-code"></a>コードをデバッグするために適したフレームを選択する

モデル駆動型アプリのフォームは複数のフレームで構成されます。 ブラウザー開発者ツールの**コンソール**で動作するコードの場合、適切なフレームを選択する必要があります。 
- Web クライアント フォームでは、**ClientApiWrapper** という名前のフレームを選択します。 
- 新しい統一インターフェイス フォームでは、**ClientApiFrame_[n]** という名前のフレームを選択する必要があります。ここで n は内部ページ ID です。 [n] の最も大きい値のフレームを選択する必要があります。

## <a name="write-messages-to-the-console"></a>コンソールにメッセージを作成する

JavaScript のデバッグ時に [window.alert](https://msdn.microsoft.com/library/ms535933(v=vs.85).aspx) メソッドを使用することは、アプリケーション内のコードをトラブルシューティングするための一般的な方法です。 最近のすべてのブラウザーでは、デバッグ ツールへ簡単にアクセスできますが、デバッグしているアプリケーションを他の人が使用している場合、ベスト プラクティスではありません。

代わりにコンソールにメッセージを記述することを検討してください。 次に、ライブラリに追加できる小さな関数を示します。それにより、コンソールを開いたときに表示するメッセージを送信するために使用できます。

```JavaScript
function writeToConsole(message)
{
 if (typeof console != 'undefined') {
  console.log(message);
 }
}
```

alert メソッドとは異なり、この関数を使用するコードを削除することを忘れた場合は、アプリケーションを使用するユーザーにはメッセージが表示されません。
