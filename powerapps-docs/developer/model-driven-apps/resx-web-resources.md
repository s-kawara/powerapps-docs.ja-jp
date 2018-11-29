---
title: 文字列 (RESX) Web リソース (モデル駆動型アプリ) | MicrosoftDocs
description: 文字列 Web リソースを使用して、ローカライズされた文字列を使用できるようにする方法について説明します。
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
# <a name="resx-web-resources"></a>RESX Web リソース

<!-- https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/resx-web-resources -->

これらの Web リソースを使用して、任意のユーザー インターフェイスで、定義するまたはエラー メッセージと共に表示するローカライズされた文字列を管理します。 

# <a name="using-resx-web-resources"></a>RESX Web リソースの使用

RESX Web リソースには、RESX XML 形式を使用して定義された単一言語のキーおよびローカライズされた文字列値が含まれます。 RESX XML 形式は Windows アプリケーション用のローカライズされるリソースを定義する一般的な形式で、この種類のファイルを操作するためのツールがあります。ローカライズ ベンダーはこれらの操作に慣れています。 ファイルが CRM で Web リソースとして公開される場合、必要であればアプリケーションにダウンロードされる JSON 形式に変換されます。

RESX Web リソースを作成するときには、言語値を明示的に設定して、Web リソースの名前に適切な言語のロケール ID (LCID) を含める必要があります。 たとえば、`new_/strings/MyAppResources.1033.resx` には英語のリソースが含まれます。 LCID 値のリストについては、「[Microsoft ロケール ID 値](https://msdn.microsoft.com/library/ms912047(WinEmbedded.10).aspx)」を参照してください。

ローカライズ値を抽出するには、[Xrm.Utility.getResourceString](clientapi/reference/Xrm-Utility/getResourceString.md) 関数を使用します。 この関数は、`WebResourceName` と `keyValue` の 2 つのパラメーターを受け入れます。 

たとえば、`Xrm.Utility.getResourceString("new_/strings/MyAppResources","hello")` は、ユーザーの優先言語が英語である場合には、`new_/strings/MyAppResources.1033.resx` Web リソース内でリソース キーのローカライズされた文字列値 hello を返します。 関数は特定の言語または RESX Web リソースのフル ネームを参照しないことに注意してください。 この機能は、依存関係として呼び出し JavaScript Web リソースに関連付けられている RESX Web リソースに依存します。 詳細情報: [Web リソースの依存関係](web-resource-dependencies.md)

適切な文字列値は、各ユーザーの言語設定と組織で使用可能な言語によって決まります。 ローカライズされた文字列がユーザーの言語設定と一致しない場合、ローカライズされた文字列が組織の基本言語に自動的にフォールバックします。 組織の基本言語に一致するローカライズされた文字列が見つからない場合、null 値が返されます。

### <a name="see-also"></a>関連項目
[Web リソース](web-resources.md)<br />
[アクセス可能な Web リソースの作成](create-accessible-web-resources.md)<br />
[モバイル クライアント用 Dynamics 365 で使用する Web リソースと IFrame の内容を作成する](/dynamics365/customer-engagement/developer/create-web-resources-iframe-mobile)<br />
[Web リソースの依存関係](web-resource-dependencies.md)<br />
[Webpage (HTML) の Web リソース](webpage-html-web-resources.md)<br />
[Silverlight (XAP) の Web リソース](/dynamics365/customer-engagement/developer/silverlight-xap-web-resources)<br />
[スクリプト (JScript) Web リソース](script-jscript-web-resources.md)<br />
[画像 (JPG、PNG、GIF、ICO) の Web リソース](image-web-resources.md)<br />
[スタイルシート (XSL) Web リソース](stylesheet-xsl-web-resources.md)<br />
[データ (XML) Web リソース](data-xml-web-resources.md)<br />
[CSS Web リソース](css-web-resources.md)<br />
[Web リソース (WebResource) エンティティのメッセージおよびメソッド](/dynamics365/customer-engagement/developer/webresource-entity-messages-methods)<br />
[サンプル: データ パラメーターを使用した Web リソースへの複数の値の引き渡し](sample-pass-multiple-values-web-resource-through-data-parameter.md)<br />
[サンプル: Web リソースとしてファイルをインポート](sample-import-files-web-resources.md)<br />