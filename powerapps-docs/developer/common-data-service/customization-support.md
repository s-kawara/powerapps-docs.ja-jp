---
title: Common Data Service for Apps アプリの開発練習 | MicrosoftDocs
ms.custom: ''
ms.date: 06/18/2018
ms.reviewer: ''
ms.service: crm-online
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Dynamics 365 (online)
- Dynamics 365 Version 9.x
- powerapps
ms.assetid: e9810433-224b-4bde-851a-e581cf5fb8a4
caps.latest.revision: 21
author: Mattp123
ms.author: matp
manager: kvivek
search.audienceType:
- developer
search.app:
- PowerApps
- D365CE
ms.openlocfilehash: 1eda4b591a3296001ffa62b16e185b421a197e75
ms.sourcegitcommit: 429b83aaa5a91d5868e1fbc169bed1bac0c709ea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/24/2018
ms.locfileid: "42865043"
---
# <a name="common-data-service-for-apps-supported-and-unsupported-app-building-practices"></a>Common Data Service for Apps でサポートされている/サポートされていないアプリの開発練習

<!--
The way your organization works is unique. Some organizations have well-defined business processes that they apply using PowerApps apps. Others aren’t happy with their current business processes and use PowerApps to apply new data and processes to their business. Whatever situation you find yourself in, you’ll find a lot of customization capabilities in PowerApps so that it can work for your organization.  
  
 Of course you’re eager to get started, but please take a few minutes to read the content in this section. This will introduce you to important terms, give you some background about why things are done a certain way, and help you avoid potential problems in the future.  

## What is metadata and why should you care?  
 In the past, you may have customized business applications by editing the source code. This created complications because each organization had unique changes and it was very difficult, or extremely expensive, to upgrade. Then application developers started exposing application programming interfaces (APIs) so that other developers could interact with the application and add their own logic without touching the source code. This was moderately better because it means developers can extend the application without changing it. But it still requires a developer to write code.  -->
  
 現代のビジネス アプリケーションには、コードを記述せずにアプリを作成できるように、メタデータ駆動型アーキテクチャが使用されます。 メタデータは "データに関するデータ" という意味であり、Common Data Service for Apps に格納されているデータの構造を定義します。 このメタデータにより、データ構造の変更がアプリケーションで認識され、その変更に合わせてアプリケーションを調整することが可能になります。 メタデータが認識されているため、メタデータに関連付けられている追加機能を含めることができます。  

エンティティ、ビュー、フィールド、グラフ、ダッシュボードなどの Common Data Service for Apps コンポーネントを変更し、自分の望みどおりに動作するアプリを作ることは、*カスタマイズ*と呼ばれています。  
 
PowerApps にあるツールを使用し、アプリをビルドし、カスタマイズするとき、メタデータに依存する機能によって使用されるメタデータまたはデータを追加または更新します。 アプリの作成に使用される種類のデータがわかっているため、このデータを考慮し、アプリを壊すことなく、Common Data Service for Apps 環境に新しい機能を追加できます。 <!-- This way you should always be able to apply an update rollup or upgrade to the latest version and enjoy the best new features.  -->

<!--  
> **Customize or Configure?**   
> Most people say they want to customize the application, so we use the word “customize” to describe changing the system to make it work the way you want. Some people prefer to use the word “configure” because it suggests that no code was required to make changes. Call it whatever you like, we just want to make it clear that you don’t need to be a developer to customize or create PowerApps apps.  -->
  
開発者でなくても PowerApps アプリを作成したり、カスタマイズしたりできます。 しかしながら、PowerApps には、開発者がコードを記述するための一連の Web サービスと API が用意されています。 サポートされている手法でコードを記述すると、Common Data Service for Apps 環境が更新されてもコードは引き続き動作します。  
  
<a name="BKMK_SupportedCust"></a>   
## <a name="what-kinds-of-customizations-are-supported"></a>どのような種類のカスタマイズがサポートされていますか。  
 ほとんどのアプリは利用できる PowerApps アプリで作成され、カスタマイズされるものと Microsoft は想定しています。 カスタマイズ ツールでニーズが満たされない場合、サード パーティが提供するソリューションをインストールするか、開発者を雇用してアプリのコードを記述させることができます。 コードが必須のソリューションに投資する必要がある場合、サポートされている API でのみコードを記述するようにしてください。 それにより、アプリとソリューションの両方で投資が保護されます。  
  
 PowerApps アプリを拡張する開発者は、SDK で文書化されている規則とベスト プラクティス (「[Dynamics 365 Customer Engagement での開発におけるベスト プラクティス](https://docs.microsoft.com/dynamics365/customer-engagement/developer/best-practices-sdk)」) に従う義務を負います。 SDK には開発者が利用できる API が記録されており、API を最も効果的に利用する方法が指示されています。 Microsoft は SDK で文書化されている API とプラクティスのみをサポートします。 問題の解決方法に関する説明がインターネット上で見つかることがありますが、それが SDK で文書化されている API を活用するものでなければ、Microsoft はサポートしません。 開発者が変更を適用する前に、サポートされている手法が利用されているかどうかを確認してください。  
  
 開発者が SDK で文書化されている API とベスト プラクティスを利用している場合、Microsoft が Common Data Service for Apps に行った変更が既存のカスタマイズを壊す可能性があるかどうかをテストできます。 Microsoft の目標は、Common Data Service for Apps の新しいバージョンやアップデートがリリースされても、サポートされている手法で記述されたコード カスタマイズが引き続き動作することです。 開発者に毎回コードを変更させることなく、機能が改善された新しいバージョンにアップグレードできるという利点があります。  
  
 サポートされているカスタマイズが新しいバージョンの Common Data Service for Apps における変更によって壊れることがわかった場合、Microsoft は影響を受ける箇所とコードを変更して修正する方法を文書にまとめます。  
  
<a name="BKMK_Unsupported"></a>   
## <a name="what-kinds-of-customizations-arent-supported"></a>どのような種類のカスタマイズがサポートされていませんか。  
 特定の API やプログラミング プラクティスを Microsoft がサポートしていないとしても、それが動作しないということにはなりません。 <!--  “Unsupported by Microsoft” means exactly what it says: you can’t get support about these APIs or programming practices from Microsoft. We don’t test them and we don’t know if something we change will break them. We can’t predict what will happen if someone changes code in our application.  --> サポートされていない API やプログラミング プラクティスを利用する場合、開発者は自分のコードをサポートする責任を負います。 自分のコードをテストして動作することを確認する必要があります。  
  
 サポートされていないカスタマイズを Common Data Service for Apps 環境で利用する場合、Microsoft Technical Support にお問い合わせいただく前に、カスタマイズした内容を文書にまとめ、行ったカスタマイズを削除するための方針を用意してください。 サポートされていないカスタマイズのことで支援が必要な場合、そのカスタマイズを用意した開発者か組織にお問い合わせください。  
  
<a name="BKMK_CommonUnsupportedCustomizations"></a>   
### <a name="common-unsupported-customization-practices"></a>サポートされていないカスタマイズの一般的なプラクティス  
 次は、サポートされていない一般的なカスタマイズ プラクティスの一覧です。 これは完全な一覧ではありません。 詳細情報: [Dynamics 365 でサポートされている拡張子: サポートされていないカスタマイズ](https://docs.microsoft.com/dynamics365/customer-engagement/developer/supported-extensions#Unsupported)。 
 
**JavaScript を利用し、Web アプリケーションの Document Object Model (DOM) 要素を操作する**  
 アプリケーション内のどこかで使用されている JavaScript ライブラリが対話する API は、文書化されている API に限定する必要があります。 JavaScript 開発者がアプリケーションを作成するとき、頻繁に特定の名前で DOM 要素にアクセスします。 PowerApps アプリは Web アプリケーションであるため、このような手法でうまくいきますが、アプリが参照する要素の名前は突然変更されることがあり、更新中に壊れる可能性があります。 Microsoft はアプリケーションに必要な変更を行う権利を保有しており、そのことはしばしば、ページの構築方法が変更されることを意味します。 ページの現在の構造に依存する変更を追加することは、アプリケーションに更新プログラムを適用するたびに、それらのスクリプトのカスタム コードのテストとおそらくは変更にお金を使わなければならないことを意味します。  
  
 jQuery は JavaScript 開発者に使用されている非常に一般的なライブラリです。 jQuery を使用することの利点の多くは、開発者が DOM 要素にアクセスしたり、DOM 要素を作成したりする機能を簡素化することにあります。そこは Common Data Service for Apps アプリケーション ページにおいて Microsoft がサポートしない部分です。 開発者が HTML Web リソースでカスタム ユーザー インターフェイスを作成するときは jQuery が推奨されますが、PowerApps アプリケーション ページ内では、サポートされている API で jQuery の使用が要求されることはありません。  
  
 **JavaScript を使用し、文書化されていない内部オブジェクトまたはメソッドを使用する**  
Common Data Service for Apps では、ページ内でさまざまな JavaScript オブジェクトが使用されます。 JavaScript 開発者は、ページをデバッグすることでこれらのオブジェクトを発見し、アクセスして再利用できます。 Microsoft はこれらのオブジェクトに必要な変更を行う権利を保有しています。たとえば、オブジェクトを削除したり、メソッドの名前を変更したりできます。 スクリプトによってこれらのオブジェクトが参照される場合、オブジェクトが見つからなければ、スクリプトは中断されます。  <a name="BKMK_Metadata"></a>   
 
<a name="BKMK_CombineCustomizations"></a>   
## <a name="combine-customization-capabilities"></a>カスタマイズ機能を組み合わせる  
 これらのセクションにあるトピックでは、個々のカスタマイズ機能について詳しく取り上げています。 しかしながら、ビジネス要件を満たすことは、多くの場合、ある機能を 1 つまたは複数の他の機能と共に使用することで達成されます。  
  
<a name="BKMK_ChooseTheRightCustomization"></a>   
### <a name="choose-the-right-customization-capability-for-the-job"></a>ジョブに最適なカスタマイズ機能を選択する  
 PowerApps ではさまざまなカスタマイズ機能を利用できます。その 1 つを熟知し、それを利用してあらゆる問題の解決方法を探ることは難しくありません。 解決するビジネス問題を評価するときは、達成を望む最終的な結果について考え、そこにたどり着く方法を求めます。  
 
<a name="BKMK_changesinperformance"></a>   
## <a name="changes-that-affect-common-data-service-for-apps-environment-performance"></a>Common Data Service for Apps 環境のパフォーマンスに影響を与える変更  
 ソリューションをインポートしたり、メタデータを変更するカスタマイズを適用したりすると、Common Data Service for Apps 環境のパフォーマンスに影響が出ることがあります。 システムの通常の動作に干渉する可能性があるアクション:  
  
-   エンティティ、代替キー、属性、関係の追加、削除、変更。   
-   ソリューションのインポート
  
-   カスタマイズの公開 
  
このような変更を本稼働システムに適用する場合、ユーザーに対する影響が最小限に抑えられる時間帯に適用日程を計画することをお勧めします。   
  
  
## <a name="next-steps"></a>次のステップ  
[PowerApps でのモデル駆動型アプリとは](../../maker/model-driven-apps/model-driven-app-overview.md)

