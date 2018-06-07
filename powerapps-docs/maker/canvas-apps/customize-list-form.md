---
title: PowerApps を使用した SharePoint リスト フォームのカスタマイズ |Microsoft Docs
description: PowerApps を使用して、SharePoint のリスト フォームをカスタマイズします。
documentationcenter: na
author: aftowen
manager: kfile
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: conceptual
ms.component: canvas
ms.date: 02/05/2018
ms.author: anneta
ms.openlocfilehash: 34c4e4126015f9a5f53ef6f07c9c66e4a4141db0
ms.sourcegitcommit: 68fc13fdc2c991c499ad6fe9ae1e0f8dab597139
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2018
ms.locfileid: "32330401"
---
# <a name="customize-a-sharepoint-list-form-using-powerapps"></a>PowerApps を使用した SharePoint リスト フォームのカスタマイズ

PowerApps であらゆる SharePoint リスト フォームを簡単にカスタマイズできるようになりました。 SharePoint リスト フォームをカスタマイズするのに InfoPath で行っていた多くのことが、PowerApps を使ってブラウザーのインラインで行えるようになりました。 その上、PowerApps を使うともっと多くのことができるのです!

PowerApps は SharePoint と直接統合されます。別のアプリをコンピューターにダウンロードする必要はありません。 PowerApps があれば、コードを記述しなくても表現力豊かなカスタマイズ フォームを作成できます。 フォームは、発行されると SharePoint リスト内に埋め込まれて、リストのすべてのユーザーが利用できるようになります。

PowerApps は SharePoint にシームレスに統合されるので、2 つの場所からフォームを管理する必要はありません。アクセス許可は SharePoint から継承され、SharePoint を通じて管理されます。 何よりも、PowerApps を SharePoint に統合すると、分析レポート、条件付き書式の簡単なポイント アンド クリック ルール、他のデータ ソースへの接続などの多くの強力な機能にアクセスできるようになります。

カスタマイズを始める準備はできましたか? それでは、始めましょう。

## <a name="create-a-custom-list-form-app-in-powerapps"></a>PowerApps でカスタム リスト フォーム アプリを作成する

> [!NOTE]
> SharePoint リストに PowerApps がサポートしないデータ型が含まれる場合は、**[フォームのカスタマイズ]** オプションを使用できない、または正常に動作しない可能性があります。

SharePoint リスト内で、コマンド バーの **[PowerApps]**、**[アプリの作成]** の順にクリックまたはタップします。 すると、PowerApps Studio がブラウザーで開き、そこで PowerApps によって次の例のような 1 画面のフォーム アプリが生成されます。

![1 画面のフォーム アプリ](./media/customize-list-form/list-form-app.png)

任意のタイミングで SharePoint リストに戻るには、PowerApps Studio の左上隅にある **[SharePoint に戻る]** をクリックまたはタップします。

## <a name="customize-the-list-form"></a>リスト フォームをカスタマイズする

PowerApps には、フォームをカスタマイズする多くの方法が用意されています。 次に例をいくつか示します。

* [サイズと向きを変更する](set-aspect-ratio-portrait-landscape.md)
* [テキストの書式を設定する](controls/properties-text.md)
* [イメージ](add-images-pictures-audio-video.md)または[グラフを追加する](use-line-pie-bar-chart.md)
* [カスタムのデータ検証を追加する](functions/function-validate.md)
* [ルールを追加する](working-with-rules.md)
* [追加のビューを作成する](https://powerapps.microsoft.com/blog/separate-custom-forms/)

例を挙げて説明します。お使いのフォームに **[AccountID]** というフィールドがあり、表示させたくないと思っているとします。

![[AccountID] フィールドを選択](./media/customize-list-form/select-card.png)

PowerApps でフィールドを非表示にするのは簡単です。フォームのカスタマイズ オプションで **[AccountID]** のチェックボックスをオフにするだけです。

![[AccountID] のチェックボックスをオフ](./media/customize-list-form/checkbox.png)

フィールドを非表示にし、他のフォーム変更を行う詳しい手順については、「[PowerApps でのフォームのカスタマイズ](customize-forms-sharepoint.md)」をご覧ください。 全リソースの一覧については、「[Microsoft PowerApps docs (Microsoft PowerApps のドキュメント)](https://docs.microsoft.com/powerapps/)」をご覧ください。

## <a name="save-and-publish-the-list-form-back-to-sharepoint"></a>リスト フォームを保存して SharePoint に発行しなおす

1. カスタマイズしたら、**[ファイル]**、**[保存]** の順にクリックまたはタップします。 すると、PowerApps フォーム アプリの変更内容が保存されます。

1. 他のユーザーが使用できるようにフォームを SharePoint に発行しなおすには、**[SharePoint に発行]** をクリックまたはタップします。 フォームの共有について心配する必要はありません。フォームは、SharePoint リストからアクセス許可を継承します。

    ![SharePoint に発行](./media/customize-list-form/publish-to-sharepoint.png)  

## <a name="view-your-list-form-in-sharepoint"></a>SharePoint でリスト フォームを表示する

1. カスタマイズしたフォームを表示するには、**[SharePoint に戻る]** をクリックまたはタップして、SharePoint リストのいずれかのアイテムをクリックまたはタップします。 フォームが、ブラウザー ウィンドウの右側にインラインで開きます。

    ![SharePoint でフォームをインラインで開く](./media/customize-list-form/list-form-open.png)

1. [フォームをさらにカスタマイズ](sharepoint-form-integration.md)する場合は、**[カスタマイズ]** をクリックまたはタップして、変更を行います。 変更が完了したら、かならず変更を保存します。

    ![[カスタマイズ] ボタン](./media/customize-list-form/customize-button.png)

    カスタマイズと保存は何度でもできますが、変更内容は **[SharePoint に発行]** をクリックまたはタップするまで SharePoint に表示されません。

## <a name="toggle-between-using-the-default-sharepoint-form-and-the-custom-form"></a>既定の SharePoint フォームとカスタム フォームの使用を切り替える

1. SharePoint のリストから **[設定]**、**[リストの設定]**、**[フォームの設定]** の順にクリックまたはタップします。

1. **[フォームの設定]** ページで、次のいずれかをクリックまたはタップしてから、**[OK]** をクリックまたはタップします。

    * **既定の SharePoint フォームを使用する** - SharePoint は、リストの既定の SharePoint フォームを使用します。

    * **Use a custom form created in PowerApps (PowerApps で作成されたカスタム フォームを使用する)** - SharePoint は、PowerApps でカスタマイズされたフォームを使用します。 (PowerApps Studio の **[保存]** ページからフォームを再発行することもできます)。

    これらのオプションは、必要に応じて切り替えることができます。

    ![[フォームの設定] オプション](./media/customize-list-form/form-settings.png)

## <a name="delete-the-custom-list-form"></a>カスタム リスト フォームを削除する

1. SharePoint のリストから **[設定]**、**[リストの設定]**、**[フォームの設定]** の順にクリックまたはタップします。

1. **[フォームの設定]** ページで、**[既定の SharePoint フォームを使用する]** をクリックまたはタップてから、**[Use a custom form created in PowerApps (PowerApps で作成されたカスタム フォームを使用する)]** の下にある **[Delete custom form (カスタム フォームの削除)]** をクリックまたはタップします。 これにより、PowerApps で作成したカスタム フォームが 削除され、フォームは SharePoint の既定のフォームに戻ります。

    ![カスタム フォームの削除](./media/customize-list-form/use-default-sharepoint.png)

## <a name="top-questions-about-list-form-customization"></a>リスト フォームのカスタマイズに関するよくある質問

### <a name="customizing-forms-versus-creating-apps"></a>フォームのカスタマイズとアプリの作成

**Q:** カスタマイズしたリスト フォームは、SharePoint または PowerApps から作成したスタンドアロンのアプリとどう違うのですか?

**A:** SharePoint から作成したリスト フォーム アプリは、SharePoint リスト内でのみ使用できる特別な種類の PowerApps アプリです。 これらのリスト フォーム アプリは、PowerApps Studio や PowerApps Mobile のアプリ リストには表示されず、SharePoint リストの外部で実行することはできません。

**Q:** カスタマイズしたリスト フォームとスタンドアロンのアプリは、それぞれどういうときに作成すべきですか?

**A:** ユーザーに SharePoint を使用してフォームにアクセスさせる場合や、ユーザーがリスト アイテムを作成、表示、または編集する方法をカスタマイズする場合は、SharePoint 内からカスタマイズしたリスト フォームを作成することをお勧めします。 SharePoint サイトの影響を受けずにユーザーが使用できるユーザー向けの完全にカスタマイズされたエクスペリエンスを作成する場合は、スタンドアロンのアプリを作成することをお勧めします。

**Q:** リスト フォームをカスタマイズし、同じリストのスタンドアロンのアプリを作成できますか?

**A:** はい。 スタンドアロンのアプリとカスタマイズされたリスト フォームは、互いの影響を受けません。個別にカスタマイズして管理することができます。

**Q:** リスト フォームをカスタマイズするためのカスタマイズ機能は、スタンドアロンのアプリをカスタマイズするためのカスタマイズ機能と同じですか?

**A:** はい。 スタンドアロンのアプリを使用した場合と同じように、[コントロールを追加および構成したり](add-configure-controls.md)、[使用できるデータ ソースに接続したり](add-data-connection.md)、[独自のデータ ソースを追加したり](../canvas-apps/register-custom-api.md)できます。

**Q:** カスタマイズしたリスト フォームは、所属組織の既定の環境以外の環境で作成できますか?

**A:** いいえ。 現在、カスタマイズしたリスト フォームは組織の既定の PowerApps 環境のみで作成できます。カスタマイズしたリスト フォームを別の環境で作成したり、別の環境に移行することはできません。

### <a name="managing-your-custom-list-form"></a>カスタム リスト フォームの管理

**Q:** 他のユーザーと共有できるリスト フォームの直接リンクを取得する方法を教えてください。

**A:** SharePoint リストを開いて、**[リンクのコピー]** をクリックまたはタップします。

**Q:** 他のユーザーに変更を見せずに、リスト フォームを更新できますか?

**A:** はい。 フォームの変更と保存は何度でもできますが、変更内容は **[[SharePoint に発行]](customize-list-form.md#save-and-publish-the-list-form-back-to-sharepoint)** をクリックまたはタップするまで他のユーザーには表示されません。

**Q:** リスト フォームをカスタマイズしたけれど間違えた場合は、以前のバージョンに戻すことができますか?

**A:** はい。 フォームに変更を加えてその変更を保存した後に、間違いに気付いた場合は、PowerApps を使用して以前のバージョンのフォームに戻すことができます。

1. SharePoint リスト内で、コマンド バーの **[PowerApps]**、**[アプリの作成]** の順にクリックまたはタップします。

1. PowerApps Studio で **[ファイル]** をクリックまたはタップします。次に、**[保存]** ページで **[すべてのバージョンの表示]** をクリックまたはタップします。 **[バージョン]** ページが新しいブラウザー タブに表示されます。

    > [!NOTE]
    > **[すべてのバージョンの表示]** ボタンが表示されていない場合は、**[保存]** をクリックまたはタップしてください。 ボタンが表示されるはずです。

1. **[バージョン]** ページ (つまり、ブラウザー タブ) を閉じずに、元のブラウザー タブの **[保存]** ページに戻って、左側のナビゲーション ウィンドウの上部にある矢印をクリックまたはタップします。次に、**[SharePoint に戻る]** をクリックまたはタップしてフォームのロックを解除し、PowerApps Studio を終了します。

1. さきほどのブラウザー タブの **[バージョン]** ページに戻り、復元するバージョンを見つけて、**[復元]** をクリックします。

    > [!NOTE]
    > フォームが別のユーザーによってロックされているために復元が失敗したというエラー メッセージが表示された場合は、そのユーザーがフォームのロックを解除するまで待機してからやり直してください。

**Q:** カスタム リスト フォーム間を移動できますか?

**A:** いいえ。 この機能は現在サポートされていません。

### <a name="administering-custom-list-forms"></a>カスタム リスト フォームの管理

**Q:** 他のユーザーとカスタム リスト フォームを共有する方法を教えてください。

**A:** フォームを共有する必要はありません。フォームは、SharePoint リストからアクセス許可を継承します。 フォームのカスタマイズが完了したら、他のユーザーが使用できるように[そのフォームを SharePoint に発行しなおす](customize-list-form.md#save-and-publish-the-list-form-back-to-sharepoint)だけです。

**Q:** 誰がリスト フォームをカスタマイズできるのですか?

**A:** 関連リストを管理、設計、または編集する SharePoint アクセス許可を持つ任意のユーザーです。

**Q:** カスタム リスト フォームの作成や使用に、PowerApps のライセンスは必要ですか?

**A:** [PowerApps が含まれている Office 365 プラン](../../administrator/pricing-billing-skus.md#licenses)をご利用の場合は、カスタム リスト フォームの作成および使用が可能です。

**Q:** ゲスト ユーザーがカスタム フォームを含むリストにアクセスするとどうなりますか?

**A:** ゲスト ユーザーが PowerApps を使用してカスタマイズされているリスト フォームにアクセスしようとすると、エラー メッセージが表示されます。

**Q:** 管理者が所属組織のすべてのカスタマイズされたフォームのリストを取得する方法を教えてください。

**A:** PowerApps のテナント管理者であるか、組織の既定の PowerApps 環境に対する環境管理者アクセス許可を持っている場合は、次のように操作します。

1. [PowerApps 管理センター](https://admin.powerapps.com)に移動して、環境のリストから、組織の既定の環境を選択します。

1. 既定の環境のページ上部の **[リソース]** をクリックまたはタップします。

1. アプリのリストから、アプリの種類が **SharePoint Form** のアプリを探します。これらは、カスタマイズされたフォームです。

    ![カスタマイズされたフォームのリスト](./media/customize-list-form/all-customized-forms.png)
