---
title: SaveData および LoadData 関数 | Microsoft Docs
description: 構文を含む PowerApps の SaveData および LoadData 関数の参照情報
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: anneta
ms.date: 01/31/2019
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 3fb23fec6f6885a55b054889b90fed0c5efafd5e
ms.sourcegitcommit: bdee274ce4ae622f7af5f208041902e66e03d1b3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "57800355"
---
# <a name="savedata-and-loaddata-functions-in-powerapps"></a>PowerApps の SaveData および LoadData 関数
[コレクション](../working-with-data-sources.md#collections)を保存および再読み込みします。

## <a name="description"></a>説明
**SaveData** 関数は、後で名前から使用できるようにコレクションを格納します。  

**LoadData** 関数は、既に **SaveData** で保存されている名前でコレクションを再読み込みします。 別のソースからコレクションを読み込む場合、この関数は使用できません。  

内のデータをキャッシュすることによって、アプリ起動時のパフォーマンスを向上させるためにこれらの関数を使用して、 **[App.OnStart](../controls/control-screen.md#additional-properties)** 数式の最初の実行と後続の実行にローカル キャッシュを再読み込みします。 追加する、これらの関数を使用することもできます。[単純なオフライン機能](../offline-apps.md)をアプリにします。

PowerApps Studio でアプリを作成するとき、または web player アプリを実行するときに、ブラウザー内でこれらの関数を使うことはできません。 アプリをテストするには、PowerApps Mobile で iPhone または Android デバイスで実行します。

これらの関数は、メモリ内コレクションで動作するために、利用可能なアプリのメモリの量によって制限されます。 使用可能なメモリは、デバイスとオペレーティング システム、PowerApps プレーヤーを使用して、メモリ、および画面とコントロールの観点から、アプリの複雑さによって異なります。 メガバイト単位を複数のデータを格納する場合は、アプリケーションの実行を予定されているデバイスで想定されるシナリオを使用してアプリをテストします。 一般に、使用可能なメモリの 30 日と 70 のメガバイト数の間にあるはずです。  

**LoadData** はコレクションを作成しません。この関数は、既存のコレクションの格納しか行いません。 最初に **[Collect](function-clear-collect-clearcollect.md)** を使用して、適切な[列](../working-with-tables.md#columns)でコレクションを作成する必要があります。 読み込まれたデータがコレクションに追加されます。使用して、 **[クリア](function-clear-collect-clearcollect.md)** 関数の最初に空のコレクションを開始する場合。

ストレージは暗号化され、他のユーザーとアプリからは分離された、ローカル デバイス上のプライベートな場所にあります。

## <a name="syntax"></a>構文
**SaveData**( *Collection*, *Name* )<br>**LoadData**( *Collection*, *Name* [, *IgnoreNonexistentFile* ])

* *Collection* - 必須。  格納または読み込みの対象となるコレクション。
* *Name* - 必須。  ストレージの名前。 同じデータ セットを保存し、読み込むには、同じ名前を使用する必要があります。 名前空間は、他のアプリまたはユーザーとは共有されません。
* *IgnoreNonexistentFile* - 省略可能。 一致するファイルが見つからないときに **LoadData** 関数でエラーを表示するか無視するかを示すブール値 (**true**/**false**)。 **false** を指定した場合、エラーが表示されます。 **true** を指定した場合、エラーは無視されます。これは、オフラインのシナリオで役立ちます。 **SaveData** は、デバイスがオフライン (つまり、**Connection.Connected** の状態が **false**) の場合に、ファイルを作成します。

## <a name="examples"></a>例

| 数式 | 説明 | 結果 |
| --- | --- | --- |
| **If(Connection.Connected, ClearCollect(LocalTweets, Twitter.SearchTweet("PowerApps", {maxResults:100})),LoadData(LocalTweets, "Tweets", true))** |デバイスが接続されている場合、Twitter サービスから LocalTweets コレクションを読み込みます。それ以外の場合は、ローカル ファイル キャッシュからコレクションを読み込みます。 |デバイスがオンラインであるかオフラインであるかによって、コンテンツがレンダリングされます。 |
| **SaveData(LocalTweets, "Tweets")** |LocalTweets コレクションをデバイスにローカル ファイル キャッシュとして保存します。 |**LoadData** がコレクションに読み込むことができるように、データはローカルに保存されます。 |

