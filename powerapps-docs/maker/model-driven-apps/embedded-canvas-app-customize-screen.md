---
title: モデル駆動フォームに埋め込まれたキャンバス アプリケーションの画面サイズと表示方向をカスタマイズする | MicrosoftDocs
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

# <a name="customize-the-screen-size-and-orientation-of-a-canvas-app-embedded-on-a-model-driven-form"></a>モデル駆動フォームに埋め込まれたキャンバス アプリケーションの画面サイズと表示方向をカスタマイズする
本トピックではモデル駆動フォームに埋め込まれたキャンバス アプリケーションの画面サイズと表示方向をカスタマイズ方法を説明します。

1.  以下の手順に従って、モデル駆動フォームに埋め込まれたキャンバス アプリケーションを追加または編集します。
    - [埋め込み型キャンバス アプリケーションをモデル駆動フォームに追加する](embedded-canvas-app-add-classic-designer.md)
    - [モデル駆動型フォームの埋め込み型キャンバス アプリケーションを編集する](embedded-canvas-app-edit-classic-designer.md)
2. キャンバス アプリケーションを PowerApps Studioで開き、**ファイル** タブを選択して **アプリの設定** を選択します。
3. **画面サイズ+向き** タブを選択します。既定では、 **サイズ** が **カスタム** に設定されています。
4. 使用可能な **サイズ** および **方向** オプションのリストから選択するか、 **カスタム** を選択して **幅** および **高さ** に設定する値を指定します。
    > [!NOTE]
    > **サイズ** が **カスタム** に設定されている場合、 **方向** は指定した **幅** と **高さ** に基づいて決定されるため、無効となります。
5. 変更が完了したら、 **ファイル** タブを選択し、 **保存**を選択します。
6. 変更した内容をエンドユーザーが利用できるようにするには、 **公開** を選択し、 **このバージョンを公開する**を選択します。

## <a name="see-also"></a>関連項目
[モデル駆動型フォーム上にキャンバス アプリを埋め込む](embed-canvas-app-in-form.md) <br />
[埋め込み型キャンバス アプリケーションをモデル駆動フォームに追加する](embedded-canvas-app-add-classic-designer.md) <br />
[モデル駆動型フォームの埋め込み型キャンバス アプリケーションを編集する](embedded-canvas-app-edit-classic-designer.md) <br />
[組み込みキャンバス アプリ内からホスト フォームで事前定義済みの操作を実行する](embedded-canvas-app-actions.md) <br />
[ModelDrivenFormIntegrationコントロールのプロパティとアクション](embedded-canvas-app-properties-actions.md) <br />
[埋め込みキャンバス アプリの共有](share-embedded-canvas-app.md)。 <br />
[埋め込みキャンバス アプリの作業のガイドライン](embedded-canvas-app-guidelines.md) <br />
[パブリック プレビュー リリースを使用して作成された、モデル駆動型フォームの埋込み型キャンバスアプリケーションを最新版へと移行する](embedded-canvas-app-migrate-from-preview.md) <br />
