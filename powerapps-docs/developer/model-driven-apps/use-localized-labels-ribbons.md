---
title: リボンでのローカライズされたラベルを使用する (モデル駆動型アプリ) | Microsoft Docs
description: リボンでのローカライズされたラベルの使用について説明します。
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: KumarVivek
ms.author: kvivek
manager: shilpas
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="use-localized-labels-with-ribbons"></a>リボンでのローカライズされたラベルの使用

<!-- https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/customize-dev/use-localized-labels-ribbons -->

テキストを表示するリボン要素にはテキストを直接入力できますが、リボンに表示するテキストを定義するには、ローカライズされたラベルを使用することがベスト プラクティスです。 この方法では、多言語を使用でき、共有テキストの管理が向上します。  
  
## <a name="using-localized-labels"></a>ローカライズされたラベルの使用  
 `<RibbonDiffXml>` 要素には、`<LocLabels>` 要素が含まれます。 以下の例に示すように、`<Titles>` 要素を使用して、リボン ラベルとツールチップに表示するテキストを指定できます。  
  
```xml  
<LocLabels>  
 <LocLabel Id="MyISV.account.SendToOtherSystem.LabelText">  
  <Titles>  
   <Title languagecode="1033"  
          description="Send to Other System" />  
  </Titles>  
 </LocLabel>  
 <LocLabel Id="MyISV.account.SendToOtherSystem.ToolTip">  
  <Titles>  
   <Title languagecode="1033"  
          description="Sends this Record to another system" />  
  </Titles>  
 </LocLabel>  
</LocLabels>  
```  
  
 テキストを表示するリボン要素の定義内で、`$LocLabels:` ディレクティブを使用して、ローカライズされたラベルを参照する方法を以下の例に示します。  
  
```xml  
ToolTipTitle="$LocLabels:MyISV.account.SendToOtherSystem.LabelText"  
ToolTipDescription="$LocLabels:MyISV.account.SendToOtherSystem.ToolTip"  
```  
  
## <a name="force-a-line-break-in-a-ribbon-control-label"></a>リボン コントロール ラベル内での改行の強制  
 リボン コントロール ラベルが非常に長い場合、テキストは使用可能なスペースに合わせて折り返されます。 文字 `&#x200b;&#x200b;` を使用して、改行を含める場所を指定できます。  
  
 ラベル テキストが非常に長く、テキストを折り返すだけのスペースがない場合、コントロールの幅が拡張され、ラベル全体が表示されます。  
  
### <a name="see-also"></a>関連項目  
 [コマンド、およびリボンをカスタマイズする](customize-commands-ribbon.md)   
 [エクスポート、編集の準備、およびリボンのインポート](export-prepare-edit-import-ribbon.md)   
 [リボンでのローカライズされたラベルの使用](use-localized-labels-ribbons.md)   
 [リボン コマンドを定義する](define-ribbon-commands.md)
