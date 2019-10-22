---
title: SaveData および LoadData 関数 | Microsoft Docs
description: 構文を含む PowerApps の SaveData および LoadData 関数の参照情報
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: tapanm
ms.date: 01/31/2019
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: e716de7a3551e2195d3f3459540a6f68acb4fd51
ms.sourcegitcommit: 7dae19a44247ef6aad4c718fdc7c68d298b0a1f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2019
ms.locfileid: "71992289"
---
# <a name="savedata-and-loaddata-functions-in-powerapps"></a>PowerApps の SaveData および LoadData 関数
[コレクション](../working-with-data-sources.md#collections)を保存および再読み込みします。

## <a name="description"></a>説明
**SaveData** 関数は、後で名前から使用できるようにコレクションを格納します。  

**LoadData** 関数は、既に **SaveData** で保存されている名前でコレクションを再読み込みします。 別のソースからコレクションを読み込む場合、この関数は使用できません。  

これらの関数を使用すると、アプリの起動時のパフォーマンスを向上させることができ **[ます。](../controls/control-screen.md#additional-properties)** そのためには、最初の実行時にアプリケーションの OnStart 式にデータをキャッシュしてから、以降の実行でローカルキャッシュを再読み込みします。 これらの機能を使用して、[単純なオフライン機能](../offline-apps.md)をアプリに追加することもできます。

PowerApps Studio でアプリを作成する場合、または web プレーヤーでアプリを実行する場合は、ブラウザー内でこれらの関数を使用することはできません。 アプリをテストするには、iPhone または Android デバイスで PowerApps Mobile を実行します。

これらの関数は、メモリ内コレクションで動作するため、使用可能なアプリメモリの量によって制限されます。 使用可能なメモリは、デバイスとオペレーティングシステム、PowerApps プレーヤーが使用するメモリ、および画面とコントロールの観点からアプリの複雑さによって異なります。 数 mb を超えるデータを格納する場合は、アプリを実行するデバイスで、想定されるシナリオでアプリをテストします。 一般に、30 ~ 70 mb の使用可能なメモリが必要です。  

**LoadData** はコレクションを作成しません。この関数は、既存のコレクションの格納しか行いません。 最初に **[Collect](function-clear-collect-clearcollect.md)** を使用して、適切な[列](../working-with-tables.md#columns)でコレクションを作成する必要があります。 読み込まれたデータは、コレクションに追加されます。空のコレクションから開始する場合は、 **[Clear](function-clear-collect-clearcollect.md)** 関数を最初に使用します。

ストレージは暗号化され、他のユーザーとアプリからは分離された、ローカル デバイス上のプライベートな場所にあります。

## <a name="syntax"></a>構文
**SaveData**( *Collection*, *Name* )<br>**LoadData**( *Collection*, *Name* [, *IgnoreNonexistentFile* ])

* *Collection* - 必須。  格納または読み込みの対象となるコレクション。
* *Name* - 必須。  ストレージの名前。 同じデータ セットを保存し、読み込むには、同じ名前を使用する必要があります。 名前空間は、他のアプリまたはユーザーとは共有されません。
* *IgnoreNonexistentFile* - 省略可能。 一致するファイルが見つからないときに **LoadData** 関数でエラーを表示するか無視するかを示すブール値 (**true**/**false**)。 **false** を指定した場合、エラーが表示されます。 **true** を指定した場合、エラーは無視されます。これは、オフラインのシナリオで役立ちます。 **SaveData** は、デバイスがオフライン (つまり、**Connection.Connected** の状態が **false**) の場合に、ファイルを作成します。

## <a name="examples"></a>例

| 数式 | 説明 | 結果 |
| --- | --- | --- |
| **If (接続されている、ClearCollect (LocalTweets、SearchTweet ("PowerApps"、{maxResults:100})、LoadData (LocalTweets, "ツイート", true))** |デバイスが接続されている場合、Twitter サービスから LocalTweets コレクションを読み込みます。それ以外の場合は、ローカル ファイル キャッシュからコレクションを読み込みます。 |デバイスがオンラインであるかオフラインであるかによって、コンテンツがレンダリングされます。 |
| **SaveData(LocalTweets, "Tweets")** |LocalTweets コレクションをデバイスにローカル ファイル キャッシュとして保存します。 |**LoadData** がコレクションに読み込むことができるように、データはローカルに保存されます。 |

