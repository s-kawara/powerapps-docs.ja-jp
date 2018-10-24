---
title: PowerApps でモデル駆動型アプリの Web リソースを作成または編集する | MicrosoftDocs
description: Web リソースを作成または編集する方法について説明します
ms.custom: ''
ms.date: 06/02/2018
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
ms.assetid: ef4ba8df-9ba9-4066-b40d-def9761c7de2
caps.latest.revision: 21
ms.author: matp
manager: kvivek
ms.openlocfilehash: 8d9414ba4c900f98ac26010e4e6d7240b336e2d7
ms.sourcegitcommit: aba996b1773ecdf62758e06b34eaf57bede29e08
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/08/2018
ms.locfileid: "39696064"
---
# <a name="create-or-edit-model-driven-app-web-resources-to-extend-an-app"></a>モデル駆動型アプリの Web リソースを作成または編集してアプリを拡張する

通常、Web リソースが使用されるのは、Web 開発で使用されるファイルを使って開発者がアプリを拡張する場合です。 アプリのユーザーは、開発者やデザイナーによって提供される Web リソースを管理することが必要になる場合があります。  

> [!TIP]
> Web リソースについて詳しくは、開発者ドキュメントの「[Customer Engagement の Web リソース](/dynamics365/customer-engagement/developer/web-resources)」をご覧ください。<br /> PowerApps に追加される Web リソースの依存関係については、開発者ドキュメントの [Web リソースの依存関係](/dynamics365/customer-engagement/developer/web-resources)に関する記事をご覧ください。
   
<a name="BKMK_WhatAreWebResources"></a>

## <a name="what-are-web-resources"></a>Web リソースとは  

Web リソースは、システムに格納されている仮想ファイルです。 各 Web リソースには一意の名前があり、そのファイルを取得するために URL で使用できます。 次のように考えてみてください。Web アプリを実行している実際の Web サーバーにアクセスできたとしたら、その Web サイトにファイルをコピーできます。 しかし、ほとんどのオンライン サービスではこれを実行できません。  代わりに、Web リソースを使用してシステムにファイルをアップロードし、ファイルとして Web サーバーにコピーした場合とまったく同じように、それを名前で参照することができます。  
  
たとえば、"new_myWebResource.htm" という名前の HTML ページを Web リソースとして作成した場合、次のような URL を使用してブラウザーでそのページを開くことができます。  
 
`<base URL>/WebResources/new_myWebResource.htm   `
  
ここで、*\<base URL>* の部分は、`dynamics.com` で終わるアプリを表示するために使用する URL に含まれます。 Web リソースはシステム内のデータであるため、このように Web リソースにアクセスできるのは、組織のライセンスされているユーザーのみです。 通常、Web リソースは直接参照されるのではなく、フォームに含まれています。 最も一般的な使用方法は、フォーム スクリプトに JavaScript ライブラリを提供することです。  
    
Web リソースは、システム内のデータでありソリューション対応であるため、ソリューションの一部としてエクスポートし、別の組織にソリューションをインポートすることで、別の組織に移動させることができます。 Web リソースを操作するにはソリューション エクスプローラーを使う必要があります。
  
## <a name="open-solution-explorer"></a>ソリューション エクスプローラーを開く

作成する Web リソースの名前には、カスタマイズ接頭辞が含まれます。 これは、使用中のソリューションのソリューション発行元に基づいて設定されます。 カスタマイズ接頭辞が重要であれば、作業しているアンマネージド ソリューションのカスタマイズ接頭辞が、この Web リソースに必要なものであることを確認します。 詳細: [既定の発行者のソリューション発行者の接頭辞を変更する](../common-data-service/change-solution-publisher-prefix.md) 

[!INCLUDE [cc_navigate-solution-from-powerapps-portal](../../includes/cc_navigate-solution-from-powerapps-portal.md)]

## <a name="view-web-resources"></a>Web リソースの表示

ソリューション エクスプローラーを開き、**[コンポーネント]** で **[Web リソース]** を選択します。

![Web リソースの表示](media/view-web-resources-solution-explorer.png)

<a name="BKMK_CreateAndEditWebResources"></a>

## <a name="create-or-edit-web-resources"></a>Web リソースの作成または編集  

[Web リソースの表示](#view-web-resources)中に、**[新規]** を選択して新しい Web リソースを作成するか、既存の Web リソースをダブルクリックしてこれを編集することができます。

![新しい Web リソースのフォーム](media/new-web-resource-form.png)

フォームを完成させて、Web リソースを作成または編集します。
  
|フィールド|説明|  
|-----------|-----------------|  
|**Name**|*必須*。 この Web リソースの一意の名前です。 Web リソースの保存後にこれを変更することはできません。<br />&bull; この名前に使用できるのは、文字、数字、ピリオド、連続しないスラッシュ (“/”) のみです。<br /> &bull; ソリューション発行者のカスタマイズ接頭辞が Web リソースの名前の先頭に付加されます。|  
|**表示名**|Web リソースの一覧を表示する場合に表示される名前です。|  
|**Description**|Web リソースの説明です。|  
|**種類**|*必須*。 Web リソースの種類です。 Web リソースの保存後にこれを変更することはできません。|  
|**テキスト エディター**|Web リソースの種類がテキスト ファイルの一種である場合は、このボタンを選択してページを開き、テキスト エディターを使用してコンテンツを編集します。<br />詳細: [テキスト エディターを適切に使用する](#use-the-text-editor-appropriately)| 
|**言語**|言語を選択できます。 このオプションでは、Web リソースのデータを格納するレコードがタグ付けされるだけです。 Web リソースの動作は変更されません。|  
|**ファイルのアップロード**|**[参照...]** ボタン を選択して、Web リソースとしてアップロードするファイルを選択します。<br />&bull; 新しい Web リソースを作成する場合、または既存の Web リソースを上書きする場合にファイルをアップロードすることができます。<br />&bull; ファイルのファイル名拡張子が許可されている拡張子と一致する必要があります。<br />&bull; 既定では、Web リソースとしてアップロードできるファイルの最大サイズは、5 MB です。 この値を変更するには、Dynamics 365 Customer Engagement で **[システム設定]** > **[電子メール]** タブ > **[添付ファイルのサイズ制限の設定]** 設定を使用します。 詳細: [[システムの設定] ダイアログ ボックス - [電子メール] タブ](https://docs.microsoft.com/dynamics365/customer-engagement/admin/system-settings-dialog-box-email-tab) |  
|**URL**|Web リソースを保存した後、ここに Web リソースへの URL が表示されます。 このリンクを選択して、ブラウザーで Web リソースを表示します。|  
  
変更内容を追加した後、**[保存]** を選択して、**[発行]** を選択します。  

> [!NOTE]
> Web リソースへの変更は、発行するまではアプリケーションに表示されません。
  
<a name="BKMK_UsingTextEditor"></a>
   
### <a name="use-the-text-editor-appropriately"></a>テキスト エディターを適切に使用する

Web リソース用のアプリケーションに用意されているテキスト エディターは、テキスト ファイルの簡単な編集にのみ使用する必要があります。 これを使用して HTML Web リソースの作成と編集を行うことができますが、テキスト エディターを使って作成した HTML Web リソースのみを編集する必要があります。 このテキスト エディターは、非常に単純な HTML コンテンツ向けに設計されています。 

> [!IMPORTANT]
> テキスト エディターを使って内容を作成した HTML Web リソースではない場合は、テキスト エディターを使って編集しないでください。  
> テキスト エディターでは、HTML ソースを変更するコントロールが使用され、そこでは編集が許可されています。 これらの変更によって、ブラウザーでのページの動作が変わったり、より高度なコードの場合は動作が停止したりする可能性があります。 テキスト エディターを使用して HTML Web リソースを開き、変更を加えずに保存しただけでも、一部の HTML Web リソースは破損する場合があります。  詳細: [開発者ドキュメント: HTML Web リソースでテキスト エディターを使用する](/dynamics365/customer-engagement/developer/webpage-html-web-resources#use-the-text-editor-for-html-web-resources)
  
**[ファイルのアップロード]** ボタンを使用してアップロードする前に、外部エディターを使用してテキスト ファイルを編集し、ローカルに保存することをお勧めします。 こうすることで、Web リソースのコピーを保持し、必要に応じて以前のバージョンに戻すことができます。 メモ帳などの単純なエディターを使用することも可能ですが、より高度な機能を備えたテキスト エディターを使用することを強くお勧めします。 [Visual Studio Community](https://www.visualstudio.com/vs/community/) および [Visual Studio Code](https://code.visualstudio.com/) は無料で使用でき、Web リソースによって使用されるテキスト ベースのファイルを編集するための強力な機能を備えています。  

<a name="BKMK_CreateAndEditFormWebResources"></a>
 
## <a name="create-and-edit-a-web-resource-on-a-form"></a>フォーム上の Web リソースを作成および編集する

ユーザーにとってさらに魅力的で便利になるように、フォーム上の Web リソースを追加または編集することができます。 

> [!NOTE]
> フォーム ヘッダーまたはフッターに Web リソースを含めることはできません。  

[!INCLUDE [cc_navigate-solution-from-powerapps-portal](../../includes/cc_navigate-solution-from-powerapps-portal.md)]

### <a name="navigate-to-a-form"></a>フォームに移動する
ソリューション エクスプローラーを開き、**[コンポーネント]** の下で **[エンティティ]** を展開して、操作するエンティティを展開します。

**[フォーム]** を選択し、一覧から種類がメインのフォームを見つけたら、エントリをダブルクリックまたはタップしてフォームを開き、編集します。

### <a name="add-or-edit-web-resource-in-a-form"></a>フォーム内の Web リソースを追加または編集する

設定できるフォーム内の Web リソースのプロパティについては、[Web リソースのプロパティ](web-resource-properties-legacy.md)に関する記事をご覧ください。

### <a name="preview"></a>プレビュー

メイン フォームの表示とイベントの動作をプレビューするには、次の操作を実行します。
- **[ホーム]** タブで **[プレビュー]** を選択し、**[フォームの作成]**、**[フォームの更新]**、または **[読み取り専用]** を選択します。
- フォームのプレビューを終了するには、**[ファイル]** メニューで **[閉じる]** を選択します。

### <a name="save"></a>保存

フォームの編集が完了したら、**[ホーム]** タブで **[保存して閉じる]** を選択し、フォームを閉じます。 

### <a name="publish"></a>発行

カスタマイズが完了したら、それらを発行します。
- 現在編集しているコンポーネントのカスタマイズのみを発行する場合は、ナビゲーション ウィンドウで作業していたエンティティを選択し、**[発行]** を選択します。
- 発行していないコンポーネントすべてのカスタマイズを一度に発行する場合は、ナビゲーション ウィンドウで **[エンティティ]** を選択し、**[アクション]** ツール バーで **[すべてのカスタマイズの発行]** を選択します。
   
  
### <a name="see-also"></a>関連項目  

[Web リソースのプロパティ](web-resource-properties-legacy.md) <br /> 
[フォームの作成および設計](create-design-forms.md) <br />
[カスタマイズの概要](getting-started-customization.md) <br /> 
[開発者ドキュメント: Customer Engagement の Web リソース](/dynamics365/customer-engagement/developer/web-resources)
