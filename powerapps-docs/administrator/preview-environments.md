---
title: プレビュー環境 | Microsoft Docs
description: PowerApps プレビュー プログラムで機能を先行試用する
author: manasmams
manager: kvivek
ms.service: powerapps
ms.component: pa-admin
ms.topic: conceptual
ms.date: 08/29/2018
ms.author: manasma
search.audienceType:
- admin
search.app:
- D365CE
- PowerApps
- Powerplatform
ms.openlocfilehash: e2c4c735827941b32ce5e019eb8d71e4328e4a7a
ms.sourcegitcommit: b8eee36e680036accb0e7d9fc7a434906af1c4d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/30/2018
ms.locfileid: "43297910"
---
# <a name="powerapps-preview-program"></a>PowerApps プレビュー プログラム
PowerApps では、数日または数週間おきにプラットフォームとその機能が更新されます。 PowerApps プレビュー プログラムでは、(お客様の実稼働アプリがデプロイされている) 他のリージョンで利用可能になる前に、新しい機能や更新をいち早くお試しいただけます。 

PowerApps プレビュー プログラムでは、次のことができます。
- **新しい機能を試し、理解します**。フィードバックを得る目的で、多くの機能が最初に数週間、プレビューとして公開されます。 プレビュー プログラムに参加することで、新機能について一足先に知り、フィードバックを提供できます。 また、実稼働アプリが作成されるリージョンに届いたとき、新機能をすぐに活用できます。
- PowerApps の最新アップデート (vNext) で**現行のアプリが引き続き動作するように手配し、事業を継続します**。

## <a name="what-in-powerapps-is-available-for-preview"></a>PowerApps の何がプレビューされますか。
PowerApps のプレビュー機能にアクセスするには、プレビュー環境に入る必要があります。 プレビュー環境の詳細は次のセクションにあります。
現在のところ、PowerApps には次のシナリオでプレビューを展開する予定です。
1. **アプリを作成する**: 次のバージョンの PowerApps を使用してキャンバス ベースのアプリを作成できます。 プレビュー環境でアプリを作成することでこれを実行できます。 現在のところ、モデル駆動型アプリをプレビュー プログラムに組み込めないという制限があり、Microsoft はそれについて取り組んでいます。
2. **アプリを管理する**: [PowerApps Web ポータル][2]を使用し、アプリを管理し、共有できます。 プレビュー機能にアクセスするために必要なことは、プレビュー環境に入ることです。[PowerApps Web ポータル][3]のプレビュー版が自動的に表示されます。
3. **アプリを再生する**: Web プレーヤーを使用し、プレビュー環境でアプリを再生する必要があります。 それを行うと、[Web プレーヤーのプレビュー版][4]が自動的に表示されます。 アプリは PowerApps Web プレーヤーの vNext 版で再生されます。 現在、iOS、Android、Windows 向けの PowerApps Mobile はプレビューできないという制限があります。 初回リリース環境で作成されたアプリを再生するとうまく動作しない場合があり、Microsoft はそれについて取り組んでいます。
4. **PowerApps を管理する**: [PowerApps 管理センターのプレビュー版][1]を使用することで管理体験をプレビューできます。

## <a name="how-to-get-early-access-to-the-upcoming-updates"></a>どうすれば今後のアップデートに早期アクセスできますか。
PowerApps の場合、すべてのアプリと関連リソースが 1 つの環境に格納されます。 すべてのプレビュー機能への早期アクセスは、vNext (プレビュー) がデプロイされているリージョンで作成された環境でも利用できます。 現在のところ、下の画像にあるように、リージョンは 1 つだけです。**プレビュー (米国)** です。

![](./media/preview-environment/env3-preview.png)

環境のリージョンとして **[プレビュー (米国)]** を選択し、プレビュー プログラム参加に同意し、PowerApps の次のバージョン (vNext) にアクセスするための環境を作成します。
この環境で作成されたすべてのアプリとその他のリソースは、プラットフォームの vNext バージョンに置かれます (SAAS)。

## <a name="how-to-learn-about-the-latest-updates"></a>最新のアップデートについて知る方法はありますか。
プレビューできる新しい機能に関する情報は、[PowerApps の新機能][5]で入手できます。 プレビューできる機能には "プレビュー" タグが与えられます。

## <a name="key-scenarios-to-test-with-the-preview-program"></a>プレビュー プログラムでテストする主なシナリオ
1. **近日公開の PowerApps アップデート (vNext) で実稼働アプリを検証する**

   近日公開される PowerApps のアップデートで実稼働アプリが正常に動作するか確認することが推奨されます。 初回リリースの環境に運用環境からアプリを[コピー][6]し、アプリを再生してシナリオをテストできます。 CustomAPI や Flow など、その他の必要なリソースもすべて、コピーしたアプリと共に移動する必要があります。 それにより、アプリと必要なリソースのコピーが 1 つ作成されるはずです。 アプリを再生するためだけでなく、アプリを編集しているときや管理しているときも最新アップデートのテストを開始できます。
   
2. **プレビューで利用できる新しい機能を試す**

   Microsoft はさまざまな新機能を最初に**プレビュー (米国)** リージョンで公開する予定です。 残りのリージョンで公開される前に新機能を試すことができます (運用環境に影響を与えることがあります)。

## <a name="how-to-provide-feedback-to-the-product-team"></a>製品チームにフィードバックを提供する方法は?
フィードバックは [PowerApps フォーラム][8]に投稿するか、[サポート][9]にご連絡ください。

## <a name="what-are-the-known-issues-and-limitations"></a>既知の問題と制限事項はありますか。
1. **PowerApps のポータルとクライアントはプレビューできない** 

   特定の機能、サービス、ポータルはプレビューできません。
   
   ![](./media/preview-environment/table.png)

2. **初回リリース環境で作成されたアプリに Windows の Desktop Studio からアクセスする**

   前述のように、Windows の Desktop Studio はプレビューできません。 そのため、プレビュー環境でアプリを作成したり、編集したりすることは Desktop Studio と互換性のないことであり、次のエラー メッセージが表示されます。
   
   ![](./media/preview-environment/error2.jpg)

   その場合、プレビュー環境でアプリを作成または編集するときは、Web Studio を使用することをお勧めします。

3. **プレビュー リージョンではデータベースを作成できない**

   現在のところ、プレビュー (米国) リージョンの環境では Common Data Service for Apps でデータベースを作成できません。Microsoft はこれについて取り組んでいます。


<!--Reference links in article-->
[1]: https://preview.admin.powerapps.com
[2]: https://web.powerapps.com
[3]: https://preview.web.powerapps.com
[4]: https://preview.web.powerapps.com/webplayer
[5]: https://docs.microsoft.com/powerapps/maker/canvas-apps/release-notes
[6]: https://docs.microsoft.com/powerapps/administrator/environment-and-tenant-migration
[7]: https://preview.create.powerapps.com
[8]: https://powerusers.microsoft.com/t5/PowerApps-Community/ct-p/PowerApps1
[9]: https://powerapps.microsoft.com/support/

