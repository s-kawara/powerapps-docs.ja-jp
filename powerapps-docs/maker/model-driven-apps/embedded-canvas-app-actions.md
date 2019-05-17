---
title: 埋め込みキャンバス アプリ内からホスト フォームでアクションを実行する | MicrosoftDocs
ms.custom: ''
ms.date: 03/29/2019
ms.reviewer: ''
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: get-started-article
applies_to:
  - Dynamics 365 (online)
  - Dynamics 365 Version 9.x
  - PowerApps
ms.assetid: 00e62904-2ce9-4730-a113-02b1fedbf22e
author: Aneesmsft
ms.author: matp
manager: kvivek
tags:
  - PowerApps maker portal impact
search.audienceType:
  - maker
search.app:
  - PowerApps
  - D365CE
---
# <a name="perform-predefined-actions-on-the-host-form-from-within-an-embedded-canvas-app"></a>組み込みキャンバス アプリ内からホスト フォームで事前定義済みの操作を実行する
埋め込みキャンバス アプリ はホスト フォーム上で事前定義されたアクションを実行する機能を提供します。 これらのアクションで作成者はホストフォームに移動して、更新、および保存できます。 これらのアクションを使用して、埋め込みキャンバス アプリはフォームとモデル駆動型アプリケーションのより不可欠な部分として振る舞います。  

> [!NOTE]
> この機能は現在はプレビュー中です。 <br />
> [!INCLUDE [cc-preview-features-definition](../../includes/cc-preview-features-definition.md)] 

**ModelDrivenFormIntegration** オブジェクトに、作成者がホスト フォーム上でアクションを実行可能にする次の新しいメソッドが追加されました。  
  
### <a name="navigatetomainformentityname-mainformname-recordid"></a>NavigateToMainForm(entityName, mainFormName, recordId)
ホスト フォームをメイン フォームに移動して、指定されたレコードを表示します。  
* **entityName** - メイン フォームの親エンティティを指定する必須の文字列パラメーター。  
* **formName** - 移動する先のメイン フォーム名を指定する必須の文字列パラメーター。  
* **recordId** - 必須の文字列パラメータで、メイン フォームに表示するレコードの ID を指定します。  
 
NavigateToMainForm メソッドを呼び出すと、次のエラー メッセージが表示されることがあります。
  
| エラー メッセージ | トラブルシューティングのガイダンス |
|:--------------|:-------------------------|
|**エンティティが見つかりません: *[EntityName]*** | *entityName* パラメーターの値を調べて、それが有効なエンティティー名でありユーザーがアクセスできることを確認してください。 |
|**フォームが見つかりません: *[FormName]*** | *mainFormName* パラメーターの値を調べて、それが有効なメイン フォーム名でありユーザーがアクセスできることを確認してください。 |
|**レコードを読み込み中に問題が発生しました。** | *recordId* パラメーターの値を調べて、それが有効なレコード ID でありユーザーがアクセスできることを確認してください。 |
  
  
### <a name="navigatetoviewentityname-viewname"></a>NavigateToView(entityName, viewName)
ホスト フォームをビューに移動します。  
* **entityName** - ビューの親エンティティを指定する必須の文字列パラメーター。  
* **viewName** - 移動する先のメイン フォーム名を指定する必須の文字列パラメーター。  
 
NavigateToView メソッドを呼び出すと、次のエラー メッセージが表示されることがあります。
  
| エラー メッセージ | トラブルシューティングのガイダンス |
|:--------------|:-------------------------|
|**エンティティが見つかりません: *[EntityName]*** | *entityName* パラメーターの値を調べて、それが有効なエンティティー名でありユーザーがアクセスできることを確認してください。 |
|**ビューが見つかりません: *[ViewName]*** | *viewName* パラメーターの値を調べて、それが有効なビュー名でありユーザーがアクセスできることを確認してください。 |
  
  
### <a name="openquickcreateformentityname"></a>OpenQuickCreateForm(entityName)  
エンティティの既定のクイック作成フォームを開きます。  
* **entityName** - 簡易作成フォームの親エンティティを指定する必須の文字列パラメーター。  
 
OpenQuickCreateForm メソッドを呼び出すと、次のエラー メッセージが表示されることがあります。
  
| エラー メッセージ | トラブルシューティングのガイダンス |
|:--------------|:-------------------------|
|**エンティティが見つかりません: *[EntityName]*** | *entityName* パラメーターの値を調べて、それが有効なエンティティー名でありユーザーがアクセスできることを確認してください。 |
  
  
### <a name="refreshformshowprompt"></a>RefreshForm(showPrompt)  
ホスト フォーム上のデータを更新します。  
* **showPrompt** - ホスト フォームで保存されていないデータを保存する前に、確認プロンプトをユーザーに表示するかを示す必須のブール値パラメーター。 値は true または false である必要があります。
 
RefreshForm メソッドを呼び出すと、次のエラー メッセージが表示されることがあります。
  
| エラー メッセージ | トラブルシューティングのガイダンス |
|:--------------|:-------------------------|
|**"true" または "false" をパラメーター値として使用してください。** | *showPrompt* パラメーターの値を確認し、それが "true" または "false" であることを確認してください。 |
  
  
### <a name="saveform"></a>SaveForm()  
ホスト フォーム上のデータを保存します。  


> [!NOTE]
> 機能が使用可能になる前に作成された組み込みキャンバス アプリで、事前定義された操作を実行するメソッドの IntelliSense が表示されない場合、アプリを保存して閉じ、再度開きます。 

## <a name="see-also"></a>関連項目
[モデル駆動型フォーム上にキャンバス アプリを埋め込む](embed-canvas-app-in-form.md) <br />
[埋め込みキャンバス アプリに現在のレコードをデータ コンテキストとして渡す](pass-current-embedded-canvas-app.md) <br />
[関連付けられたレコードのリストをデータ コンテキストとして埋め込みキャンバス アプリに渡す](pass-related-embedded-canvas-app.md) <br />
[埋め込みキャンバス アプリの共有](share-embedded-canvas-app.md)。 <br />
[埋め込みキャンバス アプリの作業のガイドライン](embedded-canvas-app-guidelines.md)
