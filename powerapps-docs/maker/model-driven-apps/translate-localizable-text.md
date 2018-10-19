---
title: モデル駆動型アプリのローカライズ可能なテキストの変換 | MicrosoftDocs
description: ローカライズ可能なテキストを複数の言語をサポートするように翻訳する方法について説明します
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
search.audienceType:
  - maker
search.app:
  - PowerApps
  - D365CE
---
# <a name="translate-localizable-text-for-model-driven-apps"></a>モデル駆動型アプリのローカライズ可能なテキストの変換

フィールドのラベルやドロップダウン リストの値などのエンティティまたはフィールドのテキストをカスタマイズした場合、自分の環境とは異なる基本言語バージョンを使用している環境内のユーザーに対して、カスタマイズしたテキストをユーザーの希望言語で提供することができます。 

このプロセスでは、次の 4 つの手順を実行します。
1. 環境で別の言語を有効にする
2. ローカライズ可能なテキストをエクスポートする
3. ローカライズ可能なテキストを翻訳する
4. ローカライズ済みテキストをインポートする

## <a name="enable-other-languages-for-your-environment"></a>環境で別の言語を有効にする

環境でその言語をまだ有効にしていない場合は、「[言語を有効にする](https://docs.microsoft.com/dynamics365/customer-engagement/admin/enable-languages)」に記載される手順を使用して有効にします。

> [!IMPORTANT]
> 各言語の有効化には数分かかることがあります。 この間、環境の他のユーザーは、アプリを使用できなくなる場合があります。 ユーザーへの影響が最も少ないタイミングで言語を有効にしてください。

> [!TIP]
> 言語を有効にするときは、各言語に使用される LCID 値をメモします。 この値は、ローカライズ可能なテキストのエクスポートされたデータにおける言語を表します。 言語コードは 4 桁または 5 桁のロケール ID です。 有効なロケール ID 値は、[ロケール ID (LCID) の一覧](http://go.microsoft.com/fwlink/?LinkId=122128)のページで確認できます。

## <a name="export-the-localizable-text"></a>ローカライズ可能なテキストをエクスポートする

エクスポートされるローカライズ可能なテキストのスコープは、ローカライズ可能なテキストを含むアンマネージド ソリューションです。 これは、ソリューション エクスプローラーを使用してのみ行うことができます

[!INCLUDE [cc_navigate-solution-from-powerapps-portal](../../includes/cc_navigate-solution-from-powerapps-portal.md)]

ローカライズ可能なテキストを含むアンマネージド ソリューションを開き、メニュー バーの **翻訳** > **翻訳のエクスポート** を選択します。 

![翻訳のエクスポート](media/export-localizable-text.png)

以下の内容の通知が表示されます。
> 翻訳用にカスタマイズされたラベルをエクスポートするには、数分かかる場合があります。 最初のエクスポートが終了するまで、エクスポート リンクをもう一度クリックしないでください。 今すぐエクスポートしますか? 

続行する場合は **OK** をクリックしてください。

エクスポートが完了すると、ダウンロード フォルダーに `CrmTranslations_{0}_{1}.zip` という名前のファイルが存在します。ここで、`{0}` は、ソリューションの一意の名前で、`{1}` はソリューションのバージョン番号です。

## <a name="get-the-localizable-text-translated"></a>ローカライズ可能なテキストを翻訳する

翻訳担当者、翻訳会社、およびローカリゼーション会社にはこのファイルを送信できます。

テキストを翻訳する知識がある場合や、フォームを表示するだけの場合、エクスポートした zip ファイルを展開します。2 つの XML ファイルが含まれていることがわかります。 
 - `[Content_Types].xml`
 - `CrmTranslations.xml`

Microsoft Office Excel を含む CrmTranslations.xml ファイルを開くことができます。

> [!TIP]
> 通常どおり Excel を使って Excel ファイルを開くのでない限り、Excel を開いた後、展開した CrmTranslations.xml ファイルへのパスを貼り付けることで、ファイルを開くことを選択する方が簡単な可能性があります。

> [!IMPORTANT]
> ファイル形式を変更しないでください。 別の形式でファイルを保存した場合は、インポートして元に戻すことができません。

Excel でデータを表示したら、**ローカライズされたラベル** タブを参照してください。

![ローカライズ用にエクスポートされたテキスト](media/localized-labels-tab-exported-languages.png)

ユーザー定義エンティティまたはフィールドには、ローカライズ可能なテキストの空白セルがあります。 それらのアイテムのローカライズ済みの値を追加します。

> [!NOTE]
> 標準エンティティまたはエンティティ フィールドの表示名または説明を変更した場合、ローカライズされた文字列にはソース値の翻訳が反映されます。 それらは、新しい値を反映するようにローカライズされる必要があります。

**表示文字列** タブには、リボン コマンド、エラー メッセージ、フォーム ラベルなど、そのほかの UI 要素に表示されるテキストが含まれています。

### <a name="updating-localizable-text-in-the-base-language"></a>基本言語でローカライズ可能なテキストを更新する

特殊なメッセージに含まれる標準エンティティ名またはエンティティ フィールドの表示名を変更した場合、カスタマイズした名前を使用するために **表示文字列** タブで情報を更新できます。

> [!TIP]
> システム エンティティ メッセージを編集するために表示される UI には、エンティティ名への多くの参照が含まれていますが、すべてが含まれているわけではありません。 この手法を使用してさらに多く見つけることができる場合があります。 詳細情報: [システム エンティティ メッセージの編集](../common-data-service/edit-system-entity-messages.md)

たとえば、取引先企業エンティティの表示名を*会社*に変更した場合、**表示文字列**の基本言語を検索して一致 `account`、`accounts`、`Account`、`Accounts` を見つけ、それぞれ該当する `company`、`companies`、`Company`、`Companies` に置き換えます。

> [!IMPORTANT]
> このためにファイルで一般的な検索/置換を使用しないでください。 一致するテキストが、変更した名前を実際に参照していることに注意してください。


## <a name="import-the-localized-text"></a>ローカライズ済みテキストをインポートする
テキストをインポートするには、ファイルを圧縮し、それらをシステムにインポートする必要があります。

### <a name="compress-the-files"></a>ファイルを圧縮する

`CrmTranslations.xml` ファイルの変更後、このファイルを `[Content_Types].xml` ファイルとまとめて zip 形式に圧縮する必要があります。 *両方のファイル* を選択し、右クリックしてコンテキスト メニューを開くだけです。 コンテキスト メニューで、**送る** > **圧縮 (zip 形式) フォルダー** を選択します。

### <a name="import-the-files"></a>ファイルをインポートする

翻訳のエクスポート元の同じアンマネージド ソリューションから、メニューで **翻訳** > **翻訳のインポート** を選択します。 

![翻訳のインポート](media/import-translations.png)

圧縮された翻訳済みのテキストが含まれているファイルを選択し、**インポート** を選択します。

![選択したファイルのインポート](media/import-translated-text-dialog.png)

翻訳済みテキストをインポートすると、アプリでの変更を確認するためにすべてのカスタマイズをする必要があります。

## <a name="community-tools"></a>コミュニティ ツール

[Easy Translator](https://www.xrmtoolbox.com/plugins/MsCrmTools.Translator/) は、XrmToolbox コミュニティが開発したツールです。 Easy Translator を使用して、翻訳をコンテキスト情報と共にエクスポートおよびインポートします。 

> [!NOTE]
> このコミュニティ ツールは Microsoft ではサポートされていません。
> このツールに関するご質問は、その発行元にお問い合わせください。 詳細: [XrmToolBox](https://www.xrmtoolbox.com)。


## <a name="next-steps"></a>次のステップ
[組織の地域と言語のオプション](https://docs.microsoft.com/dynamics365/customer-engagement/admin/enable-languages)<br />
[システム エンティティ メッセージの編集](../common-data-service/edit-system-entity-messages.md)

