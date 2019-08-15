---
title: アクセス可能な Web リソースの作成 (モデル駆動型アプリ) | MicrosoftDocs
description: このトピックでは、障碍のある方がアクセス可能な Web リソース ユーザー インターフェイス要素の設計に役立つ一般的なガイダンスや多くのリソースへのリンクを紹介します。
keywords: ''
ms.date: 10/31/2018
ms.service: powerapps
ms.custom:
  - ''
ms.topic: article
ms.assetid: 307269ac-674c-5b8a-fee7-767f060af15f
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

# <a name="create-accessible-web-resources"></a>アクセス可能な Web リソースの作成

<!-- https://docs.microsoft.com/dynamics365/customer-engagement/developer/create-accessible-web-resources -->


ソリューションにユーザー インターフェイス要素を提供する Web リソースを含める場合、障碍のある方でも Web リソースを使用できるようにするための要件が満たされていることを確認します。  
  
 アプリケーションのユーザー インターフェイス要素は、すべてのユーザーが同等の機能を使えるようにするための標準およびベスト プラクティスに従っています。 障碍のある方がアプリケーションを操作する場合、スクリーン リーダーやさまざま代替入力デバイスなどの支援技術 (AT) を使用することができます。  
  
 このトピックでは、障碍のある方がアクセス可能な Web リソース ユーザー インターフェイス要素の設計に役立つ一般的なガイダンスや多くのリソースへのリンクを紹介します。  
  
<a name="BKMK_AT"></a>   
## <a name="assistive-technology"></a>支援技術  
 スクリーン リーダー、点字ターミナル、音声認識ソフトウェアなどのさまざまな支援技術 (AT) アプリケーションがあります。 これらのアプリケーションは、ユーザー インターフェイス要素を、AT アプリケーションを使用するユーザーがプログラムを使用できるようにするための手段を提供します。  
  
 Windows アプリケーションの場合、Microsoft UI オートメーション (UIA) クラスは、ユーザー インターフェイス要素へのプログラムでのアクセスを可能にします。 これらのクラスは自動化テストと AT の両方をサポートします。 開発者が定義して UIA を通じて公開したプロパティおよび要素を、AT アプリケーションが使用できます。 Windows アプリケーション開発者は、UIA を使用することで、どの程度 UI 要素を公開するかをかなりの割合で制御できます。  
  
 Web アプリケーションでは、特定の HTML 要素は、ドキュメント オブジェクト モデル (DOM) を通じて公開されます。 ブラウザーで、DOM 要素をプロパティおよびイベントと共に UIA オブジェクトに変換します。プロパティとイベントは、AT により使用され、ユーザーが Web アプリケーションを使用することができるようになります。 開発者が、UIA を使用するブラウザーで公開する UI 要素をどの程度制御できるかには制限があります。  
  
<a name="BKMK_HTMLWebResources"></a>   
## <a name="accessible-html-web-resources"></a>アクセス可能な HTML Web リソース  
 Web リソースの HTML は、ブラウザーで処理され、AT アプリケーションで使用できるようになります。  
  
 考慮すべき最初の点は、HTML が所定の使用パターンに従っていることを確認することです。 たとえば、HTML `button` 要素とまったく同じように機能するクリック イベントのある HTML `div` 要素を定義できます。 ただし、ブラウザーは `div` 要素がボタンとして使用されることは想定しておらず、AT アプリケーションに同じプロパティやイベントを公開することはありません。  
  
 ユーザーが Web リソースで行える種類の操作に対して、正しい HTML 要素を使用することが重要です。 これを[セマンティック HTML](https://docs.microsoft.com/microsoft-edge/accessibility) と言います。  
  
 ただし、それ以上のことは、セマンティック HTML では行えません。 近代の Web アプリケーションには、一般に、連携して動作する多くの HTML 要素で構成されているカスタム コントロールが含まれています。 非同期 JavaScript を使用して動的に頻繁に更新されるページ コンテンツは、セマンティック HTML のみに頼った AT アプリケーションにとっては分かりづらいものです。 [Accessible Rich Internet Applications (ARIA)](https://docs.microsoft.com/microsoft-edge/accessibility) テクノロジは HTML を独自のセマンティックなやり取りを行う属性の追加により拡張することでソリューションを実現します。  
  
 ARIA は、コントロールまたはウィジェットで使用する、HTML 要素に適用できる拡張属性の標準セットを提供します。 これらの属性は、HTML 要素がコントロールで果たす役割を表します。 ARIA はまた、ナビゲーション操作を改善する機能を備えており、ユーザーが動的に更新可能な要素に対応できるようにします。 推奨される方法は、ARIA をセマンティック HTML 上のレイヤーにすることです。  
  
 AT のサポートのほかに、検討する必要のある他の要件があります。 たとえば、ユーザーがテキスト サイズを大きくしたときの UI の調整方法などです。 UI で、作業を行う際にユーザーは色を区別する必要がありますか。 すべての操作は、キーボードを使用して実行できますか。 詳細については、「[Web アクセシビリティの概要](https://docs.microsoft.com/previous-versions/windows/apps/hh452681(v=win.10))」を参照してください。
  
<a name="BKMK_SilverlightWebResources"></a>   
## <a name="accessible-silverlight-web-resources"></a>アクセス可能な Silverlight Web リソースの作成  
 Silverlight Web リソースが フォームでホストされているか、HTML Web リソースおよび UI が Silverlight ブラウザーのプラグインで表示されます。 Silverlight は、Windows Presentation Framework (WPF) のサブセットです。このため、WPF ウィンドウズ アプリケーションに似た UIA を使用することで、プログラム的なアクセスおよび AT が公開されています。 詳細については、「[Silverlight Accessibility for Developers](https://docs.microsoft.com/previous-versions/windows/)」を参照してください。  
  
<a name="BKMK_AccessiblityTestingTools"></a>   
## <a name="accessibility-testing-tools"></a>アクセシビリティのテスト用ツール  
 次の一覧は、一般に公開されているアクセシビリティのテスト用ツールの一部です。  
  
 [Visual Studio アクセシビリティ チェッカー](https://msdn.microsoft.com/library/ms228004)  <!--TODO No relevant microsoft docs link-->
 HTML Web リソース ファイルを編集するために Visual Studio を使用している場合、アクセシビリティに関する問題をチェックするための組み込みツールがあります。 **ツール**メニューで、**アクセシビリティのテスト**を選択し、アクセシビリティ関連の問題に関するガイダンスを提供するレポートを表示します。  
  
 [UI Accessibility Checker](http://acccheck.codeplex.com/)  
 UI Accessibility Checker (AccChecker) は、テスターが簡単に Microsoft Active Accessibility (MSAA) や他のユーザー インターフェイス (UI) の Windows への実装に関するアクセシビリティの問題を発見できます。 AccChecker は、既存の実装についての詳細を提供する Windows API ツール (Inspect など) の実現から生まれましたが、実装が正しいかどうかについての情報はありません。  
  
 [Inspect (Inspect.exe)](https://docs.microsoft.com/windows/desktop/WinAuto/inspect-objects)  
 Inspect (Inspect.exe) は Windows ベースのツールで、任意の UI 要素を選択してその要素のユーザー補助データを表示できます。 Microsoft UI オートメーションのプロパティおよびコントロール パターンに加え、Microsoft Active Accessibility プロパティも表示できます。 Inspect はまた、UI オートメーション ツリーのオートメーション要素のナビゲーション構造、および Microsoft Active Accessibility 階層のアクセス可能オブジェクトをテストできます。  
  
 [Accessible Event Watcher (AccEvent.exe)](https://docs.microsoft.com/windows/desktop/WinAuto/accessible-event-watcher)  
 Accessible Event Watcher (AccEvent) ツールは、開発者やテスターが、UI の変更が起こったときにアプリケーションの UI 要素が適切な Microsoft UI オートメーションおよび Microsoft Active Accessibility イベントを発生させるかを検証することができます。 UI の変更は、フォーカスが変更したときや、UI 要素の呼び出し、選択、状態またはプロパティの変更が行われたときに発生する可能性があります。
  
<a name="BKMK_AdditionalResources"></a>   
## <a name="additional-resources"></a>その他のリソース  
 次の Web リソースは、リソースをアクセシブルにするための条件を定義するための開始点を提供します。  
  
-   [CRM、アクセシビリティ、および 508](http://blogs.msdn.com/b/devkeydet/archive/2013/01/29/crm-accessibility-and-508.aspx)  
  
-   [Web アクセシビリティの概要](https://docs.microsoft.com/previous-versions/windows/apps/hh452681(v=win.10))  
  
-   [ Visual Studio および ASP.NETにおけるアクセシビリティ](https://msdn.microsoft.com/library/ms228004)  <!--TODO No relevant microsoft docs link-->
  
-   [開発者向けの Silverlight のアクセシビリティ](https://docs.microsoft.com/previous-versions/windows/)  
  
-   [アクセシビリティの概要](https://developer.microsoft.com/en-us/windows/accessible-apps)  
  
-   [ユーザー補助 - W3C](http://www.w3.org/standards/webdesign/accessibility)  
  
-   [Web コンテンツのアクセシビリティに関するガイドライン (WCAG) 2.0](http://www.w3.org/TR/WCAG20/)  
  
### <a name="see-also"></a>関連項目  
 [Web ページ (HTML) の Web リソース](webpage-html-web-resources.md)   
 [Silverlight (XAP) の Web リソース](/dynamics365/customer-engagement/developer/silverlight-xap-web-resources)<br/>   <!--TODO No relevant topic in powerapps repo-->
 [Web リソース](web-resources.md)
