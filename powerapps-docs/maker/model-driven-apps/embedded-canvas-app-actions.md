---
title: 埋め込み型キャンバス アプリケーション内からホストモデル駆動型フォームで処理を実行する | MicrosoftDocs
ms.custom: ''
ms.date: 06/25/2019
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
# <a name="perform-predefined-actions-on-the-host-model-driven-form-from-within-an-embedded-canvas-app"></a>埋め込み型キャンバス アプリケーション内からホストモデル駆動型フォームで定義された処理を実行する
埋め込み型キャンバス アプリケーションはホストモデル駆動型フォームに定義済みの処理を実行することができます。 これらのアクションにより、作成者はホストモデル駆動型フォームをナビゲート、更新、保存することができます。 これらのアクションを使用すると、梅込み型キャンバス アプリケーションは、モデル駆動型フォームとモデル駆動型アプリケーションのより不可欠な要素として動作します  

**ModelDrivenFormIntegration** オブジェクトには、次の新しいメソッドが含まれており、これによって開発者がホストモデル駆動型フォームにて処理を実行できるようになります。  
  
### <a name="navigatetomainformentityname-mainformname-recordid"></a>NavigateToMainForm(entityName, mainFormName, recordId)
ホストモデル駆動型フォームからメインフォームに移動し、指定したレコードを表示します。  
* **entityName** - メイン フォームの親エンティティを指定する必須の文字列パラメーター。  
* **formName** - 移動する先のメイン フォーム名を指定する必須の文字列パラメーター。  
* **recordId** - 必須の文字列パラメータで、メイン フォームに表示するレコードの ID を指定します。  
 
NavigateToMainForm メソッドを呼び出すと、次のエラー メッセージが表示されることがあります。
  
| エラー メッセージ | トラブルシューティングのガイダンス |
|:--------------|:-------------------------|
|**エンティティが見つかりません: *[EntityName]*** | *entityName* パラメーターの値を調べて、それが有効なエンティティー名でありユーザーがアクセスできることを確認してください。 |
|**フォーム が見つかりません: *[FormName]*** | *mainFormName* パラメーターの値を調べて、それが有効なメイン フォーム名でありユーザーがアクセスできることを確認してください。 |
|**レコードを読み込み中に問題が発生しました。** | *recordId* パラメーターの値を調べて、それが有効なレコード ID でありユーザーがアクセスできることを確認してください。 |
  
  
### <a name="navigatetoviewentityname-viewname"></a>NavigateToView(entityName, viewName)
ホストモデル駆動型フォームをビューに移動します。  
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
ホストのモデル駆動型フォームのデータを更新します。  
* **showPrompt** - 必須のブール型パラメータです。ホストのモデル駆動型フォームに未保存のデータを保存する前に、ユーザーに確認メッセージを表示するかどうかを表します。 値は true または false である必要があります。
 
RefreshForm メソッドを呼び出すと、次のエラー メッセージが表示されることがあります。
  
| エラー メッセージ | トラブルシューティングのガイダンス |
|:--------------|:-------------------------|
|**"true" または "false" をパラメーター値として使用してください。** | *showPrompt* パラメーターの値を確認し、それが "true" または "false" であることを確認してください。 |
  
  
### <a name="saveform"></a>SaveForm()  
ホストモデル駆動型フォームにデータを保存します。  


> [!NOTE]
> 機能が使用可能になる前に作成された組み込みキャンバス アプリで、事前定義された操作を実行するメソッドの IntelliSense が表示されない場合、アプリを保存して閉じ、再度開きます。 

## <a name="see-also"></a>関連項目
[モデル駆動型フォーム上にキャンバス アプリを埋め込む](embed-canvas-app-in-form.md) <br />
[埋め込み型キャンバス アプリケーションをモデル駆動フォームに追加する](embedded-canvas-app-add-classic-designer.md) <br />
[モデル駆動型フォームの埋め込み型キャンバス アプリケーションを編集する](embedded-canvas-app-edit-classic-designer.md) <br />
[モデル駆動フォームに埋め込まれたキャンバス アプリケーションの画面サイズと表示方向をカスタマイズする](embedded-canvas-app-customize-screen.md) <br />
[ModelDrivenFormIntegrationコントロールのプロパティとアクション](embedded-canvas-app-properties-actions.md) <br />
[埋め込みキャンバス アプリの共有](share-embedded-canvas-app.md)。 <br />
[埋め込みキャンバス アプリの作業のガイドライン](embedded-canvas-app-guidelines.md) <br />
[パブリック プレビュー リリースを使用して作成された、モデル駆動型フォームの埋込み型キャンバスアプリケーションを最新版へと移行する](embedded-canvas-app-migrate-from-preview.md) <br />
