---
title: PowerApps を Web サイトなどのサービスに統合する | Microsoft Docs
description: Web サイトやその他のサービスにキャンバス アプリを埋め込みます。
author: mgblythe
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: ''
ms.date: 10/20/2017
ms.author: mblythe
ms.openlocfilehash: e48da773f34eb2abedd65c3ea88aab1bb184da02
ms.sourcegitcommit: e3f5a2bef64085d02aec82e62ff94ae8a4d01d24
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/02/2018
ms.locfileid: "39470778"
---
# <a name="integrate-powerapps-into-websites-and-other-services"></a>PowerApps を Web サイトなどのサービスに統合する
多くの場合、作成したアプリを、ユーザーが業務を行っている場所で使用できると非常に便利です。 PowerApps では、キャンバス アプリを iframe に埋め込むことで、そのアプリを Web サイトや Power BI、SharePoint などのサービスに統合できます。

このトピックでは、アプリを埋め込むためのパラメーターを設定する方法を説明した後で、Asset Ordering (資産の注文) アプリを Web サイトに埋め込みます。

![埋め込みアプリが表示された Power BI ダッシュボード](./media/embed-apps-dev/embed-dashboard.png)

次の制限事項を考慮してください。

* 埋め込みアプリにアクセスできるのは、同じテナント内の PowerApps ユーザーだけです。
* Internet Explorer 11 を使用して PowerApps にアクセスするには、互換表示をオフにする必要があります。

(iframe を使用せずに) SharePoint Online に PowerApps を統合することもできます。 詳しくは、「[PowerApps を使用して、SharePoint 内からアプリを生成する](../canvas-apps/generate-app-from-sharepoint-list-interface.md)」をご覧ください。

## <a name="set-uri-parameters-for-your-app"></a>アプリの URI パラメーターの設定
アプリを埋め込む場合は、まず Uniform Resource Identifier (URI) のパラメーターを設定して、iframe がアプリの場所を認識できるようにします。 URI の形式は次のとおりです。

```
https://web.powerapps.com/webplayer/iframeapp?source=iframe
&appId=/providers/Microsoft.PowerApps/apps/[AppID]
```

> [!NOTE]
> URI がページ上で見やすいように、改行を追加しています。

この URI の [AppID]\('[' と ']' を含む) を、対象のアプリの ID に置き換えるだけです。 ID を調べる方法は後で説明しますが、その前に、URI で使用できるすべてのパラメーターを以下に示します。

* **[appID]** - `/providers/Microsoft.PowerApps/apps/[AppID]` の形式で、 実行するアプリの ID を指定します。
* **screenColor** - ユーザーのアプリの読み込みエクスペリエンスを向上するために使用します。 このパラメーターは [RGBA (赤の値、緑の値、青の値、アルファ)](../canvas-apps/functions/function-colors.md) の形式で、アプリが読み込まれるときの画面の色を制御します。 アプリのアイコンと同じ色に設定することをお勧めします。
* **source** - アプリには影響しませんが、埋め込みのソースを示すわかりやすい名前を追加することをお勧めします。
* 最後に、[Param() 関数](../canvas-apps/functions/function-param.md) を使用してカスタムパラメーターを追加すると、その値をアプリで使用できます。 これは `[AppID]&amp;param1=value1` のように、URI の末尾に追加されます。 これらのパラメーターは、アプリの起動中は読み取り専用となります。変更が必要な場合はアプリを再起動する必要があります。

### <a name="get-the-app-id"></a>アプリ ID を調べる
アプリの ID は powerapps.com で調べることができます。 埋め込むアプリに対して次の手順を実行します。

1. [powerapps.com](https://powerapps.microsoft.com) の **[アプリ]** タブで、省略記号 ( **. . .** ) をクリックまたはタップし、**[詳細]** を選択します。
   
    ![アプリの詳細の表示](./media/embed-apps-dev/details.png)
2. **アプリ ID** をコピーします。
   
    ![詳細からのアプリ ID のコピー](./media/embed-apps-dev/app-id.png)
3. URI の `[AppID]` 値を置き換えます。 資産の注文アプリの場合、URI は次のようになります。
   
    ```
    https://web.powerapps.com/webplayer/iframeapp?source=iframe&appId=/providers/Microsoft.PowerApps/apps/76897698-91a8-b2de-756e-fe2774f114f2
    ```

## <a name="embed-your-app-in-a-website"></a>Web サイトにアプリを埋め込む
アプリの埋め込みは、サイトの HTML コード (または、Power BI や SharePoint などの iframe をサポートするその他のサービス) に iframe を追加することと同じほど、簡単にできるようになりました。

```
<iframe width="[W]" height="[H]" src="https://web.powerapps.com/webplayer/iframeapp?source=website&screenColor=rgba(165,34,55,1)&appId=/providers/Microsoft.PowerApps/apps/[AppID]" allow="geolocation; microphone; camera"/>
```

iframe の幅と高さの値を指定し、`[AppID]` を対象のアプリの ID で置き換えます。

> [!NOTE]
> `allow="geolocation; microphone; camera"` を iframe HTML コードに含めて、アプリが Google Chrome でこれらの機能を使用できるようにします。

次の図は、サンプルの Contoso 社 Web サイトに埋め込まれた資産の注文アプリを示しています。

![埋め込みアプリが表示された Contoso 社 Web サイト](./media/embed-apps-dev/contoso-website.png)

アプリのユーザーの認証に関して、次の点に注意してください。

* Web サイトが Azure Active Directory (AAD) ベースの認証を使用する場合は、追加のサインインは必要ありません。
* Web サイトが他のサインイン機構を使用する場合や、認証されない場合は、iframe でユーザーに対してサインイン プロンプトが表示されます。 アプリの作成者がアプリをユーザーと共有していれば、ユーザーはサインイン後にアプリを実行できるようになります。

このように、アプリの埋め込みは簡単で有用です。 埋め込みにより、Web サイトや Power BI ダッシュボード、SharePoint ページなどの、担当者やお客様が業務を行う場所にアプリを配置できます。

