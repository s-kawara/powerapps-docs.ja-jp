---
title: 要求ログ サイトで webhook 登録をテストする (Common Data Service for Apps) | Microsoft Docs
description: webhook で渡されるコンテキスト データを把握するには、要求ログ サイトを使用してデータを調べると便利です。 このトピックでは、この方法について説明します。
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: brandonsimons
ms.author: jdaly
manager: ryjones
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="test-webhook-registration-with-request-logging-site"></a>要求ログ サイトで webhook 登録をテストする 

webhook を使用するサービスを作成または構成する前に、処理する必要のあるデータを把握するために、サービスが受け取るデータの種類をテストする必要があります。 そのために、幾つかある要求ログ サイトのいずれかを使用できます。 この例では、[webhook テスター](https://webhook.site)を使用して webhook 要求のターゲットを構成します。 次の手順を実行します。

1. [https://webhook.site](https://webhook.site) に移動します。 右上隅に、緑色の **コピー** ボタンが表示されます。
    ![webhook テスター コピー ボタン](media/webhook-tester-copy-button.png)
1. **コピー** ボタンを使用して URL をコピーします。 このページを開いたままにしてください。
1. [webhook の登録](register-web-hook.md)で説明されているように、プラグイン登録ツールを使用して新しい webhook を登録します。 
    1. ステップ 2 でコピーした URL を**エンドポイント URL** として使用します。 
    1. 名前と希望する認証プロパティを設定します。 webhook テスターは、データを処理する実際のサイトのようにこれらの値を評価しませんが、どのように受け渡されるかを確認することはできます。
1. 「[webhook のステップの登録](register-web-hook.md#register-a-step-for-a-webhook)」で説明されているように、ステップ 4 で作成した webhook を使用してプラグイン登録ツールを活用しながらステップを登録します。 
    1. 取引先担当者エンティティの更新など、CDS for Apps アプリケーションのデータを編集して簡単に実行できるイベントを使用します。
1. CDS for Apps アプリケーションを使用して、イベントをトリガーする操作を実行します。
1. イベントをトリガーした後、ステップ 2 から CDS for Apps テスター ページに戻り、ページを更新します。 ページが更新され、要求で渡されるデータが表示されたことがわかります。

    ![Webhook テスター Web サイトでログされた要求の例](media/webhook-tester-example.png)

    > [!TIP]
    > **形式 JSON** オプションを使用すると、要求の本文で返される JSON を読みやすくします。

## <a name="next-steps"></a>次のステップ

[ｗebhook を使用してサーバー イベント用に外部ハンドラーを作成する](use-webhooks.md)

### <a name="see-also"></a>関連項目
[webhook の登録](register-web-hook.md)