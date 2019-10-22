---
title: リボン コマンドを定義する (モデル駆動型アプリ) | MicrosoftDocs
description: リボン コマンドは、リボン コントロール要素から参照できる再使用可能な定義を作成します。
keywords: ''
ms.date: 10/31/2018
ms.service: powerapps
ms.custom:
  - ''
ms.topic: article
ms.assetid: 60933770-8c7c-499c-12b4-8b64f6eedb35
author: JimDaly
ms.author: jdaly
manager: shilpas
ms.reviewer: null
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---

# <a name="define-ribbon-commands"></a>リボン コマンドを定義する

<!-- https://docs.microsoft.com/dynamics365/customer-engagement/developer/customize-dev/define-ribbon-commands -->

*リボン* コマンドは、リボン コントロール要素から参照できる再使用可能な定義を作成します。  
  
## <a name="ribbon-command-elements"></a>リボン コマンド要素  
 `<CommandDefinition>` 要素は、リボンのコマンドを定義します。 `Id` 属性は、`Command` パラメーターを使用してリボン コントロール要素から参照可能なコマンドの一意の ID を指定します。  
  
 リボン コマンドは次の 3 つを定義します。  
  
- **有効化ルール**: 特定のリボン コントロールを有効にするタイミングを指定します。  
  
- **表示ルール**: 特定のリボン要素を表示するタイミングを指定します。  
  
- **操作**: リボン コントロールの使用中に実行するコードを指定します。  
  
> [!IMPORTANT]
>  コマンドの定義はすべて、ユーザーのコンピューターにダウンロードされるので、コマンドの定義を実行時に評価できます。 つまり、リボンの特定のコントロールを表示する特権を持っていなくても、ユーザーは、ブラウザーの**ソースの表示**コマンドを使用して、コードを確認し、表示されないコントロールが存在しないかどうかを調べることができます。  
  
### <a name="see-also"></a>関連項目  
 [コマンド、およびリボンをカスタマイズする](customize-commands-ribbon.md)   
 [リボンでのローカライズされたラベルの使用](use-localized-labels-ribbons.md)   
 [リボンの有効化ルールの定義](define-ribbon-enable-rules.md)
