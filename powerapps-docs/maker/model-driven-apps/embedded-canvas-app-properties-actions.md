---
title: ModelDrivenFormIntegrationコントロールのプロパティと操作 | MicrosoftDocs
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
# <a name="modeldrivenformintegration-control-properties-and-actions"></a>ModelDrivenFormIntegrationコントロールのプロパティと操作
モデル駆動型フォームに埋め込まれたキャンバス アプリケーションには、 **ModelDrivenFormIntegration** という名前の特別なコントロールが含まれています。 このコントロールは、ホストのモデル駆動型フォームから埋め込みキャンバス アプリにコンテキスト データを取り込みます。  

このトピックでは、ModelDrivenFormIntegrationコントロールで使用可能なプロパティと操作について説明します。

| プロパティまたは操作 | 説明 |
|:--------------|:-------------------------|
|**DataSource** | ホスト モデル駆動型フォームの上位エンティティに接続されたデータ ソースに設定する必要があります。 <br />[新しいのキャンバス アプリを埋め込む](embedded-canvas-app-add-classic-designer.md) ときに自動的に設定されます 。 |
|**項目** | 埋め込みキャンバス アプリがホスト モデル駆動型フォームからレコードにアクセスできるようにする読み取り専用プロパティ。 <br />たとえば、名前 accountnumber と 表示名 Account Number のフィールドの値を取得するには、 ModelDrivenFormIntegration.Item.accountnumber または ModelDrivenFormIntegration.Item.'Account Number' が使用できます。 |
|**OnDataRefresh** | このプロパティの計算式は、ホスト モデル駆動型フォームがデータを保存する際に評価されます。 <br />これを使用して、ホストのモデル駆動型フォームの上位エンティティに接続されているデータ ソースを更新したり、変数の設定や更新などのほかの操作を実行します。 <br /> たとえば、これを以下の計算式に設定すると、アカウントのデータ ソースが更新され、CurrentAccountNumber という変数に現在のレコードの取引先企業番号フィールドの値が設定されます。 <br /> 更新 (アカウント) ; 設定 (CurrentAccountNumber, ModelDrivenFormIntegration.Item.'Account Number') |
|**RefreshForm** | ホストのモデル駆動型フォームのデータを更新します。 <br />詳細については [ホスト フォームでの定義済みのアクションの実行](embedded-canvas-app-actions.md#refreshformshowprompt) を参照してください。 |
|**SaveForm** | ホストモデル駆動型フォームにデータを保存します。 <br />詳細については [ホスト フォームでの定義済みアクションの実行](embedded-canvas-app-actions.md#saveform) を参照してください。  |
|**NavigateToMainForm** | ホストモデル駆動型フォームからメインフォームに移動し、指定したレコードを表示します。 <br />詳細については [ホスト フォームでの定義済みアクションの実行](embedded-canvas-app-actions.md#navigatetomainformentityname-mainformname-recordid) を参照してください。 |
|**NavigateToView** | ホストモデル駆動型フォームをビューに移動します。 <br />詳細については [ホスト フォームでの定義済みアクションの実行](embedded-canvas-app-actions.md#navigatetoviewentityname-viewname) を参照してください。  |
|**OpenQuickCreateForm** | エンティティの既定のクイック作成フォームを開きます。  <br />詳細については [ホスト フォームでの定義済みアクションの実行](embedded-canvas-app-actions.md#openquickcreateformentityname) を参照してください。  |
|**Data** | ホスト のモデル駆動型フォームから埋め込みキャンバス アプリに重要なデータを送信するためにフレームワークによって使用される読み取り専用使用するプロパティ。  <br /> このプロパティは使用しないでください。 ホストのモデル駆動型フォームからレコードにアクセスできるアイテムを使用します。  |

## <a name="see-also"></a>関連項目
[モデル駆動型フォーム上にキャンバス アプリを埋め込む](embed-canvas-app-in-form.md) <br />
[埋め込み型キャンバス アプリケーションをモデル駆動フォームに追加する](embedded-canvas-app-add-classic-designer.md) <br />
[モデル駆動型フォームの埋め込み型キャンバス アプリケーションを編集する](embedded-canvas-app-edit-classic-designer.md) <br />
[モデル駆動フォームに埋め込まれたキャンバス アプリケーションの画面サイズと表示方向をカスタマイズする](embedded-canvas-app-customize-screen.md) <br />
[組み込みキャンバス アプリ内からホスト フォームで事前定義済みの操作を実行する](embedded-canvas-app-actions.md) <br />
[埋め込みキャンバス アプリの共有](share-embedded-canvas-app.md)。 <br />
[埋め込みキャンバス アプリの作業のガイドライン](embedded-canvas-app-guidelines.md) <br />
[パブリック プレビュー リリースを使用して作成された、モデル駆動型フォームの埋込み型キャンバスアプリケーションを最新版へと移行する](embedded-canvas-app-migrate-from-preview.md) <br />
