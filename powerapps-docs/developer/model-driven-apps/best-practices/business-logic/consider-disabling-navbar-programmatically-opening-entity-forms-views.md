---
title: エンティティ フォームやビューをプログラムから開くときに NavBar の無効化を検討する | MicrosoftDocs
description: URLでエンティティ フォームやビューを開く時にナビゲーション バー (NavBar) が有効だと、待ち時間が長いネットワークでクライアントのパフォーマンスが低下する可能性があります。
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
ms.date: 3/04/2019
ms.author: jowells
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="consider-disabling-navbar-when-programmatically-opening-entity-forms-or-views"></a>エンティティ フォームやビューをプログラムから開くときに NavBar の無効化を検討する

**カテゴリ**: 設計、パフォーマンス

**影響の可能性**: 中程度

<a name='symptoms'></a>

## <a name="symptoms"></a>現象

URLでエンティティ フォームやビューを開く時にナビゲーション バー (NavBar) が有効だと、待ち時間が長いネットワークでクライアントのパフォーマンスが低下する可能性があります。

<a name='guidance'></a>

## <a name="guidance"></a>ガイダンス

URLを通じてエンティティ フォームやビューを開くカスタマイズを作成するときに、ユーザーが完全なナビゲーション バーを表示する必要があるか判断します。 ほとんどの場合で、ユーザーはエンティティ フォームを開くリンクをクリックして、なにか簡単な作業をして、そしてレコードを閉じます。  ナビゲーション バーを無効にすることで、ロードされるリソースの量が少なくなり、行われるネットワーク要求の数が少なくなります。  

エンティティ フォームやビューを開く URL を構築するときは、`main.aspx` ページのクエリ文字列パラメータに `navbar=off` を実装してください。 次の例では、ナビゲーション バーが無効な状態で取引先企業エンティティ フォームを開きます。

```JavaScript
function disableNavBar() {
    var globalContext = Xrm.Utility.getGlobalContext();
    return globalContext.getClientUrl() + "/main.aspx?appid=9411ee28-4310-e811-a839-000d3a33a7cb&etc=1&id={00000000-0000-0000-00AA-000010001004}&pagetype=entityrecord&navbar=off";
}
```

> [!IMPORTANT]
> navbar = off クエリ文字列パラメータは `main.aspx` ページでのみ利用可能です。 

<a name='problem'></a>

## <a name="problematic-patterns"></a>問題となるパターン

> [!WARNING] 
> これらのシナリオを回避する必要があります。 

ナビゲーション バー (NavBar) が有効でも、ユーザーがパフォーマンスの問題を経験するわけではありません。 ただし、追加のネットワーク要求が必要なエンティティフォームやビューには、追加のリソースをロードする必要があります。  遅延性が高いネットワークでは、これがユーザー エクスペリエンスの低下につながることが確認されています。

NavBar を有効にした構築済み URL の例を示します

```JavaScript
function enabledNavBar() {
    var globalContext = Xrm.Utility.getGlobalContext();
    // By default, NavBar is set to true if you do not include the parameter in the query string:
    return globalContext.getClientUrl() + "/main.aspx?appid=9411ee28-4310-e811-a839-000d3a33a7cb&etc=1&id={00000000-0000-0000-00AA-000010001004}&pagetype=entityrecord";
}

function enabledNavBarExplicit() {
    var globalContext = Xrm.Utility.getGlobalContext();
    // Explicitly defining that the NavBar will be enabled
    return globalContext.getClientUrl() + "/main.aspx?appid=9411ee28-4310-e811-a839-000d3a33a7cb&etc=1&id={00000000-0000-0000-00AA-000010001004}&pagetype=entityrecord&navbar=on";
}
```

<a name='additional'></a>

## <a name="additional-information"></a>追加情報

モデル駆動型アプリから他のレコードを開くと、サイトマップ内に定義された領域とサブエリアと一緒にナビゲーション バーがロードされます。  さらに、ユーザーがアクセスできる Office 365 アプリを表示する [Office アプリ起動ツール](https://support.office.com/article/Meet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a) も表示します。<br/>
![NavBar の有効化と無効化の比較](../media/navbar_comparison_enabled_disabled.png)

<a name='seealso'></a>

### <a name="see-also"></a>関連項目

[URL を使用してフォーム、ビュー、ダイアログ、およびレポートを開く](../../open-forms-views-dialogs-reports-url.md)
