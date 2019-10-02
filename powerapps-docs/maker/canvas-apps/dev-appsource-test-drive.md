---
title: AppSource でのお客様によるキャンバス アプリ体験版の使用 | Microsoft Docs
description: AppSource を使用してお客様とキャンバス アプリを共有し、ビジネスの潜在顧客を生成します。
author: tapanm-msft
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: anneta
ms.date: 05/08/2017
ms.author: litran
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 1e9ac3428a9621da360fd1cc5f1c376d52352d1b
ms.sourcegitcommit: 60fd1792430b9f3da08ec161cb2277506d795e3a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2019
ms.locfileid: "71705335"
---
# <a name="let-customers-test-drive-your-canvas-app-on-appsource"></a>AppSource でのお客様によるキャンバス アプリ体験版の使用

PowerApps でのキャンバス アプリの作成に関心がありますか。 キャンバス アプリをお客様と共有したいですか。 アプリをお客様と共有し、ビジネスの潜在顧客を開拓する方法として、[AppSource.com](https://appsource.microsoft.com) では PowerApps 体験版ソリューションをサポートしています。

## <a name="what-is-a-test-drive-solution"></a>体験版ソリューションとは

体験版ソリューションを使用すると、お客様は、PowerApps プランにサインアップしたり、アプリケーションをインストールしたりせずに、実際のアプリを試すことができます。 お客様は、Azure Active Directory (AAD) アカウントを使用して AppSource.com にサインインして、Web ブラウザーでアプリを実行するだけです。 体験版がなければ、お客様はアプリに関する説明を読んだり、ビデオを見たりするしかありません。 体験版を使用すると、ソリューションの内容やアプリの機能についてよく理解することができます。 アプリを実際に使用する経験を持つことができます。 お客様がアプリの内部の構築方法を見ることはできないため、知的財産は保護されます。 体験版アプリを起動するユーザーについて、潜在顧客の情報を収集して共有し、ビジネスの成長に役立てます。

AppSource.com で[公開されているアプリ](https://go.microsoft.com/fwlink/?linkid=848867)の例を次に示します。

![サンプル AppSource 一覧 ](./media/dev-appsource-test-drive/sample-app-source-listing.png)

**[無料試用版]** リンクを上のアプリ一覧から選択すると、関連付けられた PowerApps 体験版アプリがユーザーのブラウザーで直接起動されます。

![サンプル アプリ Web プレーヤー](./media/dev-appsource-test-drive/sample-app-web-player.png)

## <a name="how-do-i-build-a-test-drive-solution"></a>体験版ソリューションを構築する方法
体験版ソリューション用のアプリの構築は、PowerApps でアプリを構築する方法と同じですが、外部データ接続の代わりに埋め込みデータを使用します。 埋め込みデータを使用することで、アプリをお客様にデプロイする障壁が低くなり、体験版に対する抵抗がなくなります。通常、最終的にお客様に配布する完成したソリューションにはデータ接続が含まれますが、埋め込みデータは体験版ソリューションでは十分に機能します。

PowerApps では、埋め込みデータによるアプリの構築がネイティブにサポートされるため、アプリで使用するサンプル データが必要になるだけです。 このデータは Excel ファイルに 1 つ以上のテーブルとしてキャプチャする必要があります。 PowerApps は、外部接続を介する代わりに、Excel テーブルのデータをアプリに取得して処理します。 この後の 3 つの手順のプロセスで、アプリにデータを取得して使用する方法を説明します。

### <a name="step-1-import-data-into-the-app"></a>手順 1:アプリへのデータのインポート
2つのテーブルを含む Excel ファイルがあるとします。**Siteinspector**と**siteinspector**。

![インポートする Excel テーブル](./media/dev-appsource-test-drive/excel-file.png)

オプション **[静的データをアプリに追加します]** を使用して、これら 2 つのテーブルを PowerApps にインポートします。

![[静的データをアプリに追加します]](./media/dev-appsource-test-drive/static-data.png)

これでアプリのデータ ソースとしてテーブルが追加されました。

![データ ソースとしてインポートされた Excel テーブル](./media/dev-appsource-test-drive/data-sources.png)

### <a name="step-2-handling-read-only-and-read-write-scenarios"></a>手順 2:読み取り専用シナリオと読み取り/書き込みシナリオの処理
インポートしたデータは、*静的*つまり読み取り専用です。 アプリが読み取り専用の場合 (ユーザーへのデータの表示のみを行うアプリなど)、アプリ内でテーブルを直接参照します。 たとえば、**SiteInspector**テーブルの **Title** フィールドにアクセスする場合、式で **SiteInspector.Title** を使用します。

アプリが読み取り/書き込みの場合は、最初に各テーブルのデータを*コレクション*に取得します。これは PowerApps の表形式データ構造です。 その後、テーブルではなくコレクションを処理します。 **SiteInspector** テーブルと **SitePhotos** テーブルから **SiteInspectorCollect** コレクションと **SitePhotosCollect** コレクションにデータを取得するには、次のようにします。

```powerapps-dot
ClearCollect( SiteInspectorCollect, SiteInspector ); 
ClearCollect( SitePhotosCollect, SitePhotos )
```

この式では、両方のコレクションがクリアされてから、各テーブルのデータが対応するコレクションに収集されます。

* アプリのどこかでこの式を呼び出して、データを読み込みます。
* アプリのすべてのコレクションを表示するには、 **[ファイル]**  >  **[コレクション]** に移動します。
* 詳しくは、「[アプリのコレクションの作成と更新](../canvas-apps/create-update-collection.md)」をご覧ください。

ここで、**Title** フィールドにアクセスする場合は、式で **SiteInspectorCollect.Title** を使用します。

### <a name="step-3-add-update-and-delete-data-in-your-app"></a>手順 3:アプリでのデータの追加、更新、および削除
これまで、データを直接読み取る方法とコレクションから読み取る方法を説明しました。次は、コレクションのデータの追加、更新、削除を行う方法について説明します。

**行をコレクションに追加する**には、[Collect( DataSource, Item, ... )](../canvas-apps/functions/function-clear-collect-clearcollect.md) を使用します。

```powerapps-dot
Collect( SiteInspectorCollect,
    {
        ID: Value( Max( SiteInspectorCollect, ID ) + 1 ),
        Title: TitleText.Text,
        SubTitle: SubTitleText.Text,
        Description: DescriptionText.Text
    }
)
```

**コレクションの行を更新する**には、[UpdateIf( DataSource, Condition1, ChangeRecord1 [, Condition2, ChangeRecord2, ...] )](../canvas-apps/functions/function-update-updateif.md) を使用します。

```powerapps-dot
UpdateIf( SiteInspectorCollect,
    ID = record.ID,
    {
        Title: TitleEditText.Text,
        SubTitle: SubTitleEditText.Text,
        Description: DescriptionEditText.Text
    }
)
```

**コレクションから行を削除する**には、[RemoveIf( DataSource, Condition [, ...] )](../canvas-apps/functions/function-remove-removeif.md) を使用します。

```powerapps-dot
RemoveIf( SiteInspectorCollect, ID = record.ID )
```

> [!NOTE]
> コレクションにデータが保持されるのはアプリが実行している間だけです。アプリが終了すると、すべての変更は破棄されます。

要約すると、埋め込みデータを使用するアプリのアプリのバージョンを作成できます。これを使用して、外部データに接続するアプリのエクスペリエンスをシミュレーションします。 データを埋め込んだら、そのアプリを体験版ソリューションとして AppSource.com に公開する準備が整いました。

## <a name="how-do-i-list-my-test-drive-solution-on-appsourcecom"></a>体験版ソリューションを AppSource.com に登録する方法
アプリの準備ができたので、AppSource.com に公開します。 このプロセスを開始するには、PowerApps.com の[申し込みフォーム](https://powerapps.microsoft.com/partners/get-listed/)に必要事項を入力してください。

申し込みが完了すると、AppSource.com でアプリを公開するために送信する手順が記載された電子メールが届きます。 また、エンドツーエンドのプロセスを詳しく説明している利用開始のドキュメントを[こちらから](https://go.microsoft.com/fwlink/?linkid=851031)ダウンロードできます。

