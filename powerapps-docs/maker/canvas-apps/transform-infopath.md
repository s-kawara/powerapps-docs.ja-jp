---
title: InfoPath フォームを PowerApps に作り替える | Microsoft Docs
description: InfoPath フォームを InfoPath の一般的なシナリオより多くの情報を含む PowerApps に変更する方法、および PowerApps でこれらの項目を作成する方法について説明します。
author: richardriley99
manager: kvivek
ms.service: powerapps
ms.topic: article
ms.custom: canvas
ms.reviewer: anneta
ms.date: 04/05/2018
ms.author: rriley
ms.openlocfilehash: b57d62d3e64ea08905ddcc8627cf6921d421fb18
ms.sourcegitcommit: b9fa569153924af9815db45d52c04e764ddb7fa2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/17/2018
ms.locfileid: "39094727"
---
# <a name="transform-your-infopath-forms-to-powerapps"></a>InfoPath フォームを PowerApps に作り替える

InfoPath で作成したものをさらに堅牢なプラットフォームで提供する方法について説明します。

## <a name="key-advantages-of-powerapps-over-infopath"></a>PowerApps が InfoPath より優れている点

InfoPath のほとんどのパワー ユーザーは、独特なスキル セットを使って優れたフォームを作成しています。 このようなユーザーは自分が作成するフォームに満足していますが、制限がないわけではありません。&quot;古くさい&quot; 感じ、モバイル デバイスの最適なエクスペリエンスとはいえないこと、将来の見通しの不確実さ、そしてコードを記述せずに他のサービスに接続しようとするといつでも引っ掛かってしまうこと、などです。

PowerApps チームには、これらをはじめとする多くの課題が報告されてきます。 チームは、よりよいエクスペリエンスを PowerApps に組み込もうと努力しています。 目標は、ユーザーがビジネス スキルと既存の技術スキルを利用してアプリを作成できるようにすることです。 PowerApps を使って、コードを記述することなく、適切なビジネス ソリューションを速やかに構築して展開できるようにすることです。

**PowerApps が可能にするパワフルな未来**  
PowerApps はサービスとしてのソフトウェア (SaaS) プラットフォームであり、高機能のアプリを短期間で開発し、追加作業なしで Web、SharePoint、Dynamics 365、Teams、Power BI、モバイル デバイスに展開できるように設計されています。 そして、簡単に展開できるので (公開されているアプリへの URL を伝えるだけです)、更新も簡単に行うことができます。

**アプリの共有**  
アプリを構築して、Google や Apple のアプリ ストアに公開しようとしたことがあればわかるはずですが、 面倒です。 さらなる課題として、第 2 のアプリを展開したり、既存のアプリを更新したりする場合、ユーザーははるかに多くの手順を実行する必要があります。 PowerApps ではそのようなことはありません。 ユーザーは、アプリ ストアから Microsoft PowerApps アプリをインストールした後、Microsoft アカウントのユーザー名とパスワードを使ってログインすれば、共有されているすべての高機能アプリを利用できるようになります。 その後は、アプリが更新されたり新しいアプリが追加されたりすると、ユーザーのデバイスに表示されます。 デバイス管理の苦労がないモバイル アプリは、ビジネスにとって大きなメリットです。

**モバイルについて**  
PowerApps では、ユーザーのモバイル デバイスの機能を活用することができます。 アクセラレータ、カメラ、コンパス、接続情報、位置信号などのすべてにアプリ内からアクセスできます。 これにより、アプリ構築のあらゆる可能性を活用できます。 もちろん、PowerApps ではタッチ機能が自動的に有効になり、アプリ構築時に余分なコーディングは必要ありません。

**既成の枠を破る**  
InfoPath の原則は、1 つのデータ ソースからのデータを使うことでした。 ただし、別の場所 (別のサイト コレクションの SharePoint リストなど) から更新したり、外部サービスに接続しようとすると、分離コードのような概念のために面倒になります。 PowerApps ではそのようなことはありません。 PowerApps は、複数のデータ ソースとサービス接続を 1 つのアプリで使用できるように設計されています。 現在、[150 を超えるコネクタ](https://docs.microsoft.com/powerapps/connections-list#all-connectors)が提供されており、オンプレミスとクラウドのデータ、Microsoft Office 365 および Flow や Dynamics 365 などの Azure サービス、Dropbox、Google、Salesforce、Slack などの人気のあるターゲットを含む多数のサード パーティ サービスの組み合わせがサポートされています。 元のデータがあった場所だけでなく、ユーザーが必要とする場所を含むようにソリューションを拡張できます。

## <a name="powerapps-and-sharepoint-even-better-together"></a>PowerApps と SharePoint: 相乗効果

PowerApps は、SharePoint のエクスペリエンスを 2 つの方法で向上させる優れたツールです。 SharePoint リスト用のフォームをカスタマイズしたり、SharePoint データを操作するためのスタンドアロン アプリを作成したりできます。

**[Customizing a SharePoint form]\(SharePoint フォームのカスタマイズ\)** は、ユーザーが日常の作業に使っている SharePoint リストの項目を追加/表示/編集する方法をカスタマイズしたい場合に最適です。 **[Customize Forms]\(フォームのカスタマイズ\)** をクリックすると、コンテキストに基づいてモード (新規/編集/表示) を変更する単一画面の &quot;フォーム アプリ&quot; が作成されます。 これらのアプリは SharePoint によって管理されます。そのアクセス許可は、編集/表示のためのリストのアクセス許可と同じです。

**SharePoint から PowerApps キャンバス アプリを作成する**と、モバイル デバイスでアプリを単独で実行することができます。 SharePoint ページにアプリを埋め込むこともできます。 クリックすると 3 画面のアプリ (リスト ビュー、新規/編集フォーム、表示フォーム) が作成されます。  これらのアプリのアクセス許可/共有モデルは、SharePoint には関連付けられておらず、PowerApps から管理されます。

2 つのオプションの違いを理解したので、次のセクションではそれぞれの使い方の概要を説明します。

## <a name="sharepoint-forms"></a>SharePoint フォーム

PowerApps チームと SharePoint チームは協力して、SharePoint で使用するための新しいカスタマイズ ストーリーを作成しています。  ほとんどの InfoPath 開発者は、SharePoint と対話するために InfoPath を学習します。 SharePoint はすばらしいものですが、既定のフォームは少し平凡であり、InfoPath なしではカスタマイズやビジネス ロジックに対応していません。 しかし、それももう昔の話です。

PowerApps を使えば、ネイティブ機能としてリスト フォームをカスタマイズできます。 それにより、PowerApps のすべての機能を利用できます。 次のスクリーンショットは、Power BI レポートが埋め込まれた PowerApps フォームの例です。  ソリューション全体は、15 分もかからずに作成できました。

![SharePoint の統合](./media/transform-infopath/sharepoint-integration.png)

PowerApps のもう 1 つの重要な機能は、同じフォームから別の SharePoint サイト コレクションまたは別の環境に簡単に接続できることです。 たとえば、SharePoint Online のデータと SharePoint オンプレミス環境のデータを同時に表示して更新する 1 つのフォームを作成したいことはありませんか。 問題はありません。 [オンプレミス データ ゲートウェイ](https://docs.microsoft.com/powerapps/gateway-management)をインストールすれば数分のうちには、接続している PowerApps、Power BI、Microsoft Flow、Azure Logic Apps をオンプレミスのデータで実行できます。 ファイアウォール ルールを変更する必要はありません。 このアプリを Microsoft Flow と接続することで、新しいレベルの機能を利用できます。

## <a name="a-standalone-sharepoint-app"></a>スタンドアロン SharePoint アプリ

リスト フォームのエクスペリエンスを更新するだけではなく、完全に構築したい場合は、SharePoint データに基づくスタンドアロン アプリでこの手法を使います。 これは初めて作るものとしても適しており、PowerApps キャンバスを学習し、さまざまなデータ ソースから将来のアプリの開発を始めることができます。

始めるには、使用する SharePoint リストに移動して次のようにします。

1. メニュー バーの [PowerApps] をクリックします
2. [アプリの作成] を選択します
3. 名前を指定します。
4. [作成] をクリックします

PowerApps が既定のアプリを作成するので、それをカスタマイズできます。

最初は簡単にします。 最初のアプリ用に、異なる型のフィールドを 2 つだけ含む簡単なカスタム リストを使います。 これにより、苦労することなく強固な基盤を築くことができます。 心配しないでください。すぐに習熟して複雑なアプリを作成できるようになります。  この最初のアプリを作成する手順については、こちらの[ドキュメント](https://docs.microsoft.com/powerapps/generate-app-from-sharepoint-list-interface)またはコミュニティのこちらの[ビデオ](https://youtu.be/BnYe_7fpZRM)をご覧ください。 次の例では、InfoPath の一般的なタスクと PowerApps でのその方法を示します。 これらの各タスクでは簡単な SharePoint リスト アプリを作成します。

# <a name="how-do-you-do-that-with-powerapps"></a>PowerApps での方法

基本的な概念を理解したので、次に進みます。 最初のアプリが身についたら、次のセクションでは InfoPath の一般的な概念を PowerApps に適用します。

**値に基づいてフィールドを非表示/表示/ロックする**  
よいフォームを作る最も一般的な方法の 1 つは、強力なビジネス ロジックを用意し、そのロジックを適用できるようにすることです。 そのための 1 つの方法は、値またはアクションに基づいてフィールドの状態を変更することです。 PowerApps では、コントロールを選択し、DisplayMode を Edit または View に設定して、ユーザーがフィールドを変更できるかどうかを指定します。 使用できる 2 番目の方法は、条件付きでそれを行う簡単な If 式です。 最初に、編集するラベルを選び、ロック アイコンをクリックしてロックを解除し、値を変更できるようにします。

![データ カードの非表示/表示/ロック](./media/transform-infopath/hide-show-lock.png)

次に、右側でカードの一番下までスクロールし、DefaultMode プロパティを編集します。

![If-Else ステートメント式](./media/transform-infopath/if-else-statement.png)

この例では If ステートメントを使います。 If(ThisItem.Color = &quot;Blue&quot;, DisplayMode.View, DisplayMode.Edit) このステートメントは、現在の項目の Color フィールドが Blue の場合は Animal フィールドを読み取り専用にし、そうではない場合はフィールドを編集可能にします。

カードをまったく表示しないようにする場合は、同様の関数を DisplayMode のすぐ上の Visible フィールドに挿入します。

ここで他に行うことは、承認ボタンを非表示にして、ユーザーのメール アドレスが承認者のメール アドレスと一致する場合にのみ表示されるようにします。 ヒント: User().Email は現在のユーザーのメール アドレスにアクセスする方法です。 したがって、ボタン Visible 値を If(YourDataCard.Text = User().Email, true, false) にします。YourDataCard は承認者のメール アドレスを格納しているカードです。

**条件付き書式**  
上でフィールドを非表示にしたのと同様の方法で、ユーザーへのフィードバックを表示できます。 入力された値が有効範囲外の場合はテキストを赤で強調表示したり、ファイルをアップロードした後はアップロード ボタンのテキストと色を削除に変更します。 これはすべて、Color や Visible などのプロパティ フィールドで If などの関数を使って行います。

たとえば、If 関数と [IsMatch](https://docs.microsoft.com/powerapps/functions/function-ismatch) 関数を組み合わせて使って、ユーザーが入力ボックスに正しい書式のメール アドレスを入力しなかった場合、メール アドレス フィールドのテキストの色を赤に変更できます。 これを行うには、TextInput1 の Color の値を If(IsMatch(TextInput1.Text, Email), Black, Red) に設定します。TextInput1 はユーザーがメール アドレスを入力するフィールドです。 IsMatch は、メールなどの多種多様な定義済みパターンや、ユーザー独自のパターン作成機能をサポートしています。 条件付き書式については、こちらの[コミュニティ ビデオ](https://powerusers.microsoft.com/t5/Video-Webinar-Gallery/PowerApps-Conditional-Formatting-and-Popups/m-p/84962)をご覧ください。

**ロール ベースのセキュリティの実装**  
最初に検討する関数は [DataSourceInfo](https://docs.microsoft.com/powerapps/functions/function-datasourceinfo) です。 データ ソースから戻る情報はデータ ソースによって異なりますが、多くの場合、DataSourceInfo(YourDataSource, DataSourceInfo.EditPermission) を使って、ユーザーにデータを編集するアクセス権があるかどうかをチェックできます。 YourDataSource をデータ ソースの名前に置き換えます。 これにより、ユーザーが編集アクセス権限を持っている場合にのみ、フォームやボタンを表示できます。 関数で照会できる情報の完全な一覧については、DataSourceInfo のドキュメントをご覧ください。

代わりに Active Directory グループを使ってアプリ内のボタンやフォームへのアクセスを管理する場合は、さらに詳しく知る必要があります。 これを行うには、PowerApps の柔軟性を利用し、Microsoft Graph API を使って独自のコネクタを作成します。 手順については、[ドキュメント](https://powerapps.microsoft.com/blog/implementing-role-based-permission/)をご覧ください。

**アプリからのメールの送信**  
PowerApps からメールを送信する方法はたくさんあります。 最も簡単な方法は、Office 365 Outlook コネクタを使うことです。 このコネクタでは、アプリからユーザーとしてメールを送信できます。 メール メッセージを受け取ったり、メールボックスの他のタスクを実行したりすることもできます。 メールの送信については、[ドキュメント](https://docs.microsoft.com/powerapps/connections/connection-office365-outlook)またはこちらのコミュニティ [ビデオ](https://powerusers.microsoft.com/t5/Video-Webinar-Gallery/Send-an-email-from-PowerApps/m-p/74349)をご覧ください。

たとえば SharePoint 承認ワークフローの承認チェーンを作成するなどして、さらに複雑なメールを送信する必要がある場合は、Microsoft Flow を作成してそれにアプリを接続します。 Microsoft Flow にアプリを接続すると、ワークフロー エンジンで PowerApps などを外部のデータやサービスに接続できます。 PowerApps と Microsoft Flow の接続については、こちらの[ドキュメント](https://docs.microsoft.com/powerapps/using-logic-flows)をご覧ください。

まだ探しているメール オプションが見つからない場合は、Benchmark Email、Gmail、MailChimp、Outlook.com、SendGrid、SMTP などに対する PowerApps コネクタも利用できます。 これが PowerApps の優れた接続性です。

**ワークフロー**  
ワークフロー エンジンに触れずにビジネス アプリやビジネス ロジックについて説明するのは容易ではありません。 よいニュースは、PowerApps チームは別のワークフロー エンジンを提供するようなことはしていません。 代わりに、Microsoft Flow サービスへの堅牢なコネクタを提供します。 これにより、使いやすいワークフロー エンジンを通して [200 以上のさまざまなサービス](https://flow.microsoft.com/connectors/)を使ってプロセスとタスクを自動化できます。 PowerApps と Microsoft Flow の接続については、こちらの[ドキュメント](https://docs.microsoft.com/powerapps/using-logic-flows)をご覧ください。

**PowerApps での変数**  
ソリューションを作成するときは、変数を含める必要があると考えるのが自然です。 PowerApps には 3 種類の変数が用意されていますが、必要があるときにだけ使います。 データを取得し、変数に格納して、その変数を参照することを考えるのではなく、データを直接参照することを考えてください。 Excel について考えるとよくわかります。 Excel では、Total は変数ではなく他のフィールドの合計です。 したがって、シートの他の場所でその値を使う場合は、合計を計算したフィールドを指定します。 これらすべてについては[ドキュメント](https://docs.microsoft.com/powerapps/working-with-variables)をご覧ください。 別の思考プロセスを受け入れてください。

それでも変数が必要な場合 (いろいろなケースがあります)、これは異なるオプションを理解する役に立ちます。 PowerApps では変数を定義する必要がないことに留意してください。 いずれかの関数を使って名前と格納する値を指定するだけで、変数が作成されます。 メニュー バーの [表示] をクリックして [変数] を選択することで、作成した変数を見ることができます。 変数はメモリに保持されているので、アプリを閉じると、その値は失われます。 変数は次の 3 種類です。

- グローバル変数は最も一般的なものです。 [Set](https://docs.microsoft.com/powerapps/functions/function-set) 関数を使って変数の値を指定すると、アプリ全体で使用できるようになります。 関数を使う方法の例は、Set(YourVariable, YourValue) です。 アプリ全体で、名前を使って YourVariable を参照できます。
- コンテキスト変数は、それが定義されている画面でのみ使用できる変数です。 画面を終了するとリセットされます。 たとえば、前の画面から渡された情報を格納したり、フォームが送信されたかどうかを追跡したりするためによく使われます。 [UpdatedContext](https://docs.microsoft.com/powerapps/functions/function-updatecontext) の一般的な使い方は、UpdateContext( { Submitted: "true" } ) です。これは Submitted 変数を true に設定します。 情報が送信されたことを追跡し、すべてのフィールドを読み取り専用に変更するには、ページに送信ボタンのこの部分を作成します。 ":" を使用していることに注意してください。個別に更新可能な情報のテーブルを格納するにはコレクションを使います。 詳細については、[Collect](https://docs.microsoft.com/powerapps/functions/function-clear-collect-clearcollect) に関するページをご覧ください。 使用例は、ユーザーが送信するさまざまな SharePoint 項目にタグを付けるショッピング カートの作成です。 概念の仕組みについては、コミュニティの[ビデオ](https://powerusers.microsoft.com/t5/Video-Webinar-Gallery/Learn-about-PowerApps-Collections/m-p/89180)をご覧ください。

**カスケード ドロップダウン**  
カスケード ドロップダウンは非常に便利です。 前のドロップダウンで選択された値に基づいて、次のドロップダウンに表示される項目をフィルター処理できます。 PowerApps では、アプリで 2 つのデータ ソースを使って作成されることがよくあります。 最初のデータ ソースのデータを使用または更新し、2 番目のデータ ソースを使ってカスケード効果を作成するための値を格納します。 2 番目のデータ ソースと選択オプションの例を次に示します。

![カスケード ドロップダウン](./media/transform-infopath/cascading-dropdowns.png)

最初のドロップダウン コントロールを作成し、Items プロパティについて、式 Distinct(Impacts, Title) を使って、Cost、Program Impact、Schedule だけをドロップダウンに表示します。 次に、2 番目のドロップダウンを追加し、Items プロパティを Filter(Impacts,ddSelectType.Selected.Value in SCategory) に設定します。ddSelectType は 1 番目のドロップダウン ボックスの名前です。 このようにしてカスケード ドロップダウンを作成できます。 詳細については、PowerApps チームの投稿「[SharePoint: Cascading Dropdowns in 4 Easy Steps!](https://powerusers.microsoft.com/t5/PowerApps-Community-Blog/SharePoint-Cascading-Dropdowns-in-4-Easy-Steps/ba-p/16248)」(SharePoint: 4 つの簡単な手順でドロップダウン カスケードを作成する) またはこの[コミュニティ ビデオ](https://powerusers.microsoft.com/t5/Video-Webinar-Gallery/PowerApps-Cascading-Dropdown/m-p/92813)をご覧ください。心配しなくても SharePoint なしで簡単に行うことができます。

**1 つのスーパー アプリを作成しない**  
PowerApps では、アプリから別のアプリを呼び出すことができるので、大規模な InfoPath フォームを 1 つ作成する代わりに、相互に呼び出すアプリのグループを作成したり、データを受け渡すことで、開発を単純にできます。

## <a name="next-steps"></a>次の手順

以上で PowerApps アプリを作成する準備ができました。 続けて以下の役に立つリンクをご覧ください。 1 つは、PowerApps コミュニティ サイトへのリンクです。 コミュニティを利用すれば、自分だけで行うよりスキルを速く高めることができます。

[**数式のリファレンス**](https://docs.microsoft.com/powerapps/formula-reference) - 既定の関数をいくつか見るだけでも、刺激を受けるのによい方法です。

[**PowerApps コミュニティ**](https://powerusers.microsoft.com/t5/PowerApps-Community/ct-p/PowerApps1) - 例を参照し、他のユーザーと情報交換し、質問して回答を受け取り、PowerApps コミュニティの拡大に手を貸してください。