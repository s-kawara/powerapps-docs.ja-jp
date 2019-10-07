---
title: Microsoft Translator 接続の概要 | Microsoft Docs
description: いくつかの例を通して段階的に Microsoft Translator への接続方法を確認し、すべての機能を見る
author: lancedMicrosoft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.date: 07/12/2017
ms.author: lanced
ms.reviewer: tapanm
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 4eab4585a2abd8633704c76b57cde52702982e97
ms.sourcegitcommit: 7dae19a44247ef6aad4c718fdc7c68d298b0a1f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2019
ms.locfileid: "71994031"
---
# <a name="connect-to-microsoft-translator-from-powerapps"></a>PowerApps から Microsoft Translator に接続する
![Microsoft Translator](./media/connection-microsoft-translator/translatoricon.png)

Microsoft Translator コネクタを追加すると、アプリの**ラベル** コントロールに翻訳されたテキストを表示できます。 たとえば、ユーザーに翻訳するテキストの入力を求める入力用のテキスト ボックスを作成できます。 また、別のラベルには翻訳されたテキストを表示できます。

このトピックでは、Microsoft Translator 接続の作成方法とアプリでの Microsoft Translator 接続の使用方法を説明し、使用可能な関数の一覧を示します。

> [!NOTE]
> このコネクタの呼び出し数は、ユーザーあたり 1 日 150 件に制限されています。

[!INCLUDE [connection-requirements](../../../includes/connection-requirements.md)]

## <a name="connect-to-microsoft-translator"></a>Microsoft Translator に接続する
1. PowerApps を開き、 **[新規]** を選択して **[空のアプリ]** を作成します。 携帯電話またはタブレットのレイアウトを選択します。 タブレットのレイアウトの方がワークスペースが広くなります。  

   ![空のアプリを開く](./media/connection-microsoft-translator/blank-app.png)
2. 右側のウィンドウで、 **[データ]** タブをクリックまたはタップし、 **[データソースの追加]** をクリックまたはタップします。
3. **[新しい接続]** 、 **[Microsoft Translator]** の順に選択します。  

    ![Microsoft Translator に接続する](./media/connection-microsoft-translator/addconnection.png)

    ![Microsoft Translator に接続する](./media/connection-microsoft-translator/add-translator.png)
4. **[接続]** を選択します。 **[データ ソース]** の下に接続が表示されます。  

    ![Microsoft Translator に接続する](./media/connection-microsoft-translator/translatordatasource.png)

## <a name="use-the-microsoft-translator-connection-in-your-app"></a>アプリで Microsoft Translator 接続を使用する
### <a name="translate-text"></a>テキストの翻訳
1. **[挿入]** メニューで、 **[テキスト]** 、 **[Text input]** (テキスト入力) の順に選択します。 テキスト入力コントロールの名前を **Source** に変更します。  

    ![名前の変更](./media/connection-microsoft-translator/renametosource.png)
2. **[挿入]** メニューの **[コントロール]** から **[ドロップ ダウン]** を追加し、名前を **TargetLang** に変更して **Source** の下に移動します。
3. **TargetLang** の **[Items](../controls/properties-core.md)** プロパティに次の式を設定します。  

    `MicrosoftTranslator.Languages()`
4. ラベルを追加して **TargetLang** の下に移動させ、 **[Text](../controls/properties-core.md)** プロパティに次の式を設定します。  

    `MicrosoftTranslator.Translate(Source.Text, TargetLang.Selected.Value)`
5. **Source** にテキストを入力し、**TargetLang** で言語を選択します。 ラベルに、入力したテキストが選択した言語で表示されます。  

    ![英語からスペイン語へのテキスト翻訳](./media/connection-microsoft-translator/translate-text.png)

### <a name="speak-translated-text"></a>翻訳されたテキストの読み上げ
まだ翻訳していない場合は、前のセクションの手順に従ってテキストを翻訳します。 以下の手順では、前のセクションと同じコントロールを使用します。

1. **TargetLang** のドロップダウン リストの **[Items](../controls/properties-core.md)** プロパティに次の式を設定します。  

    `MicrosoftTranslator.SpeechLanguages()`
2. 2 つ目のラベル (**Source** ボックスではない方) の名前を **Target** に変更します。
3. **[挿入]** メニューの **[メディア]** から**オーディオ** コントロールを追加し、**Media** プロパティに次の式を設定します。  

    `MicrosoftTranslator.TextToSpeech(Target.Text, TargetLang.Selected.Value)`
4. F5 キーを押すか、[プレビュー] ボタン (![](./media/connection-microsoft-translator/preview.png)) を選択します。 **Source** にテキストを入力して **TargetLang** で言語を選択してから、オーディオ コントロールの再生ボタンを選択します。

    入力した言語が選択した言語の音声で読み上げられます。
5. Esc キーを押して既定のワークスペースに戻ります。

### <a name="detect-the-source-language"></a>ソース言語の検出
次の手順では、前のセクションと同じ **Source** のテキスト入力コントロールと **Target** のテキスト コントロールを使用します。 必要であれば新しいコントロールを作成し、式の名前をその名前に更新してください。

1. **Target** のテキスト コントロールを選択し、 **[Text](../controls/properties-core.md)** プロパティに次の式を設定します。  

    `MicrosoftTranslator.Detect(Source.Text).Name`
2. **Source** にテキストを入力します。

    ラベルに、入力したテキストの言語が表示されます。 たとえば、ラベルには、「**bonjour**」と入力すると「**French**」(フランス語) と表示され、「**ciao**」と入力すると「**Italian**」(イタリア語) と表示されます。

## <a name="view-the-available-functions"></a>使用可能な関数の確認
この接続には、次の関数が含まれています。

| 関数名 | 説明 |
| --- | --- |
| [Languages](connection-microsoft-translator.md#languages) |Microsoft Translator でサポートされるすべての言語を取得します。 |
| [Translate](connection-microsoft-translator.md#translate) |Microsoft Translator を使用してテキストを指定された言語に翻訳します。 |
| [Detect](connection-microsoft-translator.md#detect) |入力したテキストのソース言語を検出します。 |
| [SpeechLanguages](connection-microsoft-translator.md#speechlanguages) |音声合成に使用できる言語を取得します。 |
| [TextToSpeech](connection-microsoft-translator.md#texttospeech) |入力したテキストを、WAVE 形式の音声ストリームの音声に変換します。 |

### <a name="languages"></a>言語:
言語の取得:Microsoft Translator でサポートされるすべての言語を取得します。

#### <a name="input-properties"></a>入力プロパティ
なし。

#### <a name="output-properties"></a>出力プロパティ

| プロパティ名 | データ型 | 必須 | 説明 |
| --- | --- | --- | --- |
| コード |string |いいえ | |
| 名前 |string |いいえ | |

### <a name="translate"></a>Translate
テキストの翻訳：Microsoft Translator を使用してテキストを指定された言語に翻訳します。

#### <a name="input-properties"></a>入力プロパティ

| 名前 | データ型 | 必須 | 説明 |
| --- | --- | --- | --- |
| query |string |はい |翻訳するテキスト |
| languageTo |string |はい |翻訳先言語のコード (例: fr (フランス語)) |
| languageFrom |string |いいえ |ソース言語 (指定しない場合、自動検出が行われます) (例: en (英語)) |
| category |string |いいえ |翻訳のカテゴリ (既定値: general (一般)) |

#### <a name="output-properties"></a>出力プロパティ
なし。

### <a name="detect"></a>Detect
言語の検出:入力したテキストのソース言語を検出します。

#### <a name="input-properties"></a>入力プロパティ

| 名前 | データ型 | 必須 | 説明 |
| --- | --- | --- | --- |
| query |string |はい |言語を特定するテキスト |

#### <a name="output-properties"></a>出力プロパティ

| プロパティ名 | データ型 | 必須 | 説明 |
| --- | --- | --- | --- |
| コード |string |いいえ | |
| 名前 |string |いいえ | |

### <a name="speechlanguages"></a>SpeechLanguages
音声の言語を取得します。音声合成に使用できる言語を取得します。

#### <a name="input-properties"></a>入力プロパティ
なし。

#### <a name="output-properties"></a>出力プロパティ

| プロパティ名 | データ型 | 必須 | 説明 |
| --- | --- | --- | --- |
| コード |string |いいえ | |
| 名前 |string |いいえ | |

### <a name="texttospeech"></a>TextToSpeech
テキスト読み上げ:入力したテキストを、WAVE 形式の音声ストリームの音声に変換します。

#### <a name="input-properties"></a>入力プロパティ

| 名前 | データ型 | 必須 | 説明 |
| --- | --- | --- | --- |
| query |string |はい |変換するテキスト |
| language |string |はい |音声を生成する言語コード (例: en-us (米国英語)) |

#### <a name="output-properties"></a>出力プロパティ
なし。

## <a name="helpful-links"></a>便利なリンク
[利用可能な接続](../connections-list.md)をすべて表示する。  
アプリに[接続を追加する](../add-manage-connections.md)方法を確認する。

