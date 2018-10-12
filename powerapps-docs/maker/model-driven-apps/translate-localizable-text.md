---
title: モデル駆動型アプリのローカライズ可能なテキストを翻訳する |MicrosoftDocs
description: 複数の言語をサポートするためにローカライズ可能なテキストを翻訳する方法について説明します
ms.custom: ''
ms.date: 06/03/2018
ms.reviewer: ''
ms.service: crm-online
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Dynamics 365 (online)
- Dynamics 365 Version 9.x
- powerapps
author: Mattp123
ms.assetid: 3d77d149-819b-45e6-8e70-1fbe54d5c153
caps.latest.revision: 19
ms.author: matp
manager: kvivek
ms.openlocfilehash: e2e305313f3b86be2ea410f6668676b56aa79d95
ms.sourcegitcommit: aba996b1773ecdf62758e06b34eaf57bede29e08
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/08/2018
ms.locfileid: "39690798"
---
# <a name="translate-localizable-text-for-model-driven-apps"></a>モデル駆動型アプリのローカライズ可能なテキストを翻訳する

フィールド ラベルやドロップダウン リスト値などのエンティティまたはフィールド テキストをカスタマイズした場合は、その環境の基本言語バージョンを使用していない、環境内のユーザーに対して、ユーザーの優先言語でこのカスタマイズされたテキストを提供できます。 

このプロセスの手順は次のとおりです。
1. 環境に対して他の言語を有効にする
2. ローカライズ可能なテキストをエクスポートする
3. ローカライズ可能なテキストを翻訳する
4. ローカライズされたテキストをインポートする

## <a name="enable-other-languages-for-your-environment"></a>環境に対して他の言語を有効にする

環境に対して言語をまだ有効にしていない場合は、「[言語を有効にする](https://docs.microsoft.com/dynamics365/customer-engagement/admin/enable-languages)」で説明されている手順を使用して有効にします。

> [!IMPORTANT]
> 各言語を有効にするには数分かかる場合があります。 その間、環境内の他のユーザーはそのアプリを使用できません。 言語の有効化は、ユーザーへの影響が最小限に留まる時間に行う必要があります。

> [!TIP]
> 言語を有効にしている間、各言語に使用される LCID 値に注意してください。 この値は、ローカライズ可能なテキストのエクスポートされたデータの言語を表します。 言語コードは、4 桁または 5 桁のロケール ID です。 有効なロケール ID 値は[ロケール ID (LCID) チャート](http://go.microsoft.com/fwlink/?LinkId=122128) に示されています。

## <a name="export-the-localizable-text"></a>ローカライズ可能なテキストをエクスポートする

エクスポートされるローカライズ可能なテキストの範囲は、ローカライズ可能なテキストを含むアンマネージド ソリューションです。 この処理には必ずソリューション エクスプ ローラーを使用します。

[!INCLUDE [cc_navigate-solution-from-powerapps-portal](../../includes/cc_navigate-solution-from-powerapps-portal.md)]

ローカライズ可能なテキストを含むアンマネージド ソリューションを開き、メニュー バーで **[翻訳]** > **[翻訳のエクスポート]** を選択します。 

![翻訳のエクスポート](media/export-localizable-text.png)

次のアラートが表示されます。
> 翻訳用にカスタマイズされたラベルをエクスポートするには、数分間かかることがあります。 最初のエクスポートが完了するまで、エクスポート リンクを再度クリックしないでください。 今すぐエクスポートしますか? 

続行するには、**[OK]** をクリックします。

エクスポートが完了すると、ダウンロード フォルダー内に `CrmTranslations_{0}_{1}.zip` のような名前のファイルが生成されます。ここで、`{0}` はソリューションの一意名、`{1}` はソリューションのバージョン番号です。

## <a name="get-the-localizable-text-translated"></a>ローカライズ可能なテキストを翻訳する

このファイルを言語の専門家、翻訳会社、およびローカリゼーション会社に送信できます。

テキストを翻訳する知識を持っているか、または単に形式を確認する場合は、エクスポートした zip ファイルを解凍すると、2 つの XML ファイルが含まれていることがわかります。 
 - `[Content_Types].xml`
 - `CrmTranslations.xml`

Microsoft Office Excel を使用して、CrmTranslations.xml ファイルを開くことができます。

> [!TIP]
> 日常的に Excel で XML ファイルを開く場合を除き、Excel を開いてから、解凍した CrmTranslations.xml ファイルへのパスを貼り付けることで、ファイルを選択して開く方が簡単です。

> [!IMPORTANT]
> ファイル形式を変更しないようにしてください。 ファイルを別の形式で保存した場合、再インポートができなくなります。

Excel でデータを表示したら、**[ローカライズされたラベル]** タブを確認します。

![ローカライズ用にエクスポートされたテキスト](media/localized-labels-tab-exported-languages.png)

任意のカスタム エンティティまたはフィールドには、ローカライズ可能なテキスト用の空のセルがあります。 これらの項目に対してローカライズされた値を追加します。

> [!NOTE]
> 標準のエンティティまたはエンティティ フィールドの表示名または説明を変更しても、ローカライズされた文字列は、元の値に対する翻訳を反映します。 これらの文字列は、新しい値を反映するようにローカライズする必要があります。

**[表示文字列]** タブには、リボン コマンド、エラー メッセージ、フォーム ラベルなどのその他の UI 要素に対して表示されるテキストが含まれています。

### <a name="updating-localizable-text-in-the-base-language"></a>ローカライズ可能なテキストを基本言語で更新する

特殊なメッセージに含まれる標準のエンティティまたはエンティティ フィールドの表示名を変更する場合は、カスタマイズした名前を使用するように **[表示文字列]** タブ内の情報を更新できます。

> [!TIP]
> システム エンティティ メッセージの編集用に公開されている UI には、エンティティ名への多数の参照が含まれますが、それらのすべてが含まれるわけではありません。 この手法を使用すると、さらに多くの名前が表示されます。 詳細情報: [システム エンティティ メッセージの編集](../common-data-service/edit-system-entity-messages.md)

たとえば、Account エンティティの表示名を *Company* に変更する場合、**[表示文字列]** で基本言語列を検索して `account`、`accounts`、`Account`、`Accounts` との一致文字列を見つけてから、それぞれ `company`、`companies`、`Company`、`Companies` に適切に置換します。

> [!IMPORTANT]
> その際に、ファイルで一般的な検索/置換を実行しないでください。 一致したテキストが、変更した名前を実際に参照するようにしてください。


## <a name="import-the-localized-text"></a>ローカライズされたテキストをインポートする
テキストをインポートするには、ファイルを圧縮してからシステムにインポートする必要があります。

### <a name="compress-the-files"></a>ファイルを圧縮する

`CrmTranslations.xml` ファイルを変更した後は、このファイルを `[Content_Types].xml` ファイルと共に zip 形式に圧縮する必要があります。 *両方のファイル*を選択し、マウスの右ボタンをクリックして、コンテキスト メニューを開きます。 コンテキスト メニューで、**[送る]** > **[圧縮 (zip 形式) フォルダー]** を選択します。

### <a name="import-the-files"></a>ファイルをインポートする

翻訳のエクスポート元として使用した同じアンマネージド ソリューションから、メニューで **[翻訳]** > **[翻訳のインポート]** を選択します。 

![翻訳のインポート](media/import-translations.png)

圧縮された翻訳済みテキストを含むファイルを選択し、**[インポート]** を選択します。

![選択したファイルのインポート](media/import-translated-text-dialog.png)

翻訳されたテキストがインポートされたら、すべてのカスタマイズを発行してアプリでの変更を表示する必要があります。

## <a name="community-tools"></a>コミュニティ ツール

[Easy Translator](https://www.xrmtoolbox.com/plugins/MsCrmTools.Translator/) は、XrmToolBox コミュニティによって開発されたツールです。 Easy Translator を使用すると、翻訳をコンテキスト情報と共にエクスポートおよびインポートできます。 

> [!NOTE]
> コミュニティ ツールは、Microsoft ではサポートされません。
> このツールに関してご不明な点がありましたら、発行元にお問い合わせください。 詳細情報: [XrmToolBox](https://www.xrmtoolbox.com)


## <a name="next-steps"></a>次の手順
[組織の地域と言語のオプション](https://docs.microsoft.com/dynamics365/customer-engagement/admin/enable-languages)<br />
[システム エンティティ メッセージの編集](../common-data-service/edit-system-entity-messages.md)

