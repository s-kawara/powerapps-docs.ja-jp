---
title: Web リソースの依存関係 (モデル駆動型アプリ) | MicrosoftDocs
description: Common Data Serviceの Web リソース間の依存関係の定義について説明します。
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
# <a name="web-resource-dependencies"></a>Web リソースの依存関係

<!-- https://docs.microsoft.com/dynamics365/customer-engagement/developer/web-resource-dependencies -->

他の Web リソース間の依存関係を定義できます。 この機能の主な目的は、文字列 (RESX) Web リソースと、それを使用する JavaScript Web リソースとの関連付けを可能にすることです。 また、これにより、オフライン使用のために HTML Web リソースが必要とする Web リソースも、オフラインで利用できるように設定することができます。 

しかし、JavaScript Web リソースを使用する開発者が利用できる他の動作がいくつかあります。

次の画像は、Web リソース フォーム内の [依存関係] タブを示しています。 Web リソース間の依存関係は上のリストで設定します。 属性の依存関係は、下のリストを使用して設定します。 属性の依存関係は、JavaScript Web リソースにのみ利用できます。 詳細情報 [属性の依存関係](#attribute-dependencies)

![[Web リソースの依存関係] タブ](media/web-resource-dependencies.PNG)

ソリューション内では、ソリューション コンポーネント内の依存関係を定義できます。 モデル駆動型アプリまでは、これらの依存関係の主な目的は、別のソリューション コンポーネントの依存先になっているときにソリューション コンポーネントを削除しないようにすることでした。 モデル駆動型アプリでは、JavaScript Web リソースの動作が強化されており、JavaScript Web リソースへの依存としてリストされた他の Web リソースも JavaScript Web リソースと共に読み込まれます。 

> [!NOTE]
> 依存関係が構成されてその Web リソースが公開された後にのみ、依存関係が確立されます。 未公開の Web リソースの依存関係は、その Web リソースが公開されるまで有効になりません。

最も一般的なシナリオは、文字列 (RESX) Web リソースをそれに依存する Javascript Web リソースに関連付けることです。 文字列 (RESX) Web リソースは、それを使用する JavaScript Web リソースに関連付けられる各言語対応のものがあります。 その JavaScript Web リソースが読み込まれると、ローカライズされた値もユーザーの優先する言語と組織の基本言語用に自動的に読み込まれ、使用できるようになります。 いずれにせよこれらのリソース間のソリューション依存関係は作成する必要があるため、必要とするときに依存 RESX リソースが自動的に読み込まれることを知るというさらなる利点があります。

ただし、Web リソースの依存関係は RESX Web リソースだけに限られません。 JavaScript Web リソースを任意の他のタイプの Web リソースに関連付けて、その関連付けられた Web リソースを JavaScript Web リソースと共に読み込ませる依存関係を作成することができます。 これにより、フォーム イベントのスクリプトを登録するときに複数の依存 Web リソースを明示的に読み込む必要がなく、ただプライマリ スクリプトを登録して依存構成に残りを読み込ませるため、時間の節約になります。 プライマリ JavaScript Web リソースのために読み込まれる JavaScript Web リソースにはそれに関連付けられた Web リソースがすべて含まれるため、依存関係のチェーンを作成することもできます。

> [!IMPORTANT]
> Web リソースの依存関係は、Web リソースが読み込まれる順序を制御しません。 すべての Web リソースは非同期にまた並行して読み込まれます。 JavaScript Web リソースが、初期化する前に読み込んで初期化すべき他の JavaScript Web リソースに依存している場合は、別の方法でその依存関係を管理する必要があります。

<a name="attribute-dependencies"></a>

# <a name="attribute-dependencies"></a>属性の依存関係
<!--TODO: Add links to the attribute and attribute.controls collection definitions in the Client API reference -->
 モデル駆動型アプリ以降、JavaScript Web リソースがフォームに表示したくないエンティティ属性の値に依存する場合は、その属性を JavaScript Web リソースの依存関係として設定できます。 つまり、属性をクライアント API の attributes コレクション内で使用できるようになるため、コード内の値を取得または設定できるようになります。 この方法で依存関係を追加すると、フォームにコントロールがないため、属性の controls コレクションが空になります。

この機能の前は、フォームに属性を手動で追加してからコントロールを非表示にするように構成する必要がありました。 今では、この依存関係をより直接的に確立し、誰かがフォームから非表示フィールドを削除する可能性を排除できます。 


## <a name="see-also"></a>関連項目
[Web リソース](web-resources.md)<br />
[アクセス可能な Web リソースの作成](create-accessible-web-resources.md)<br />
[Webpage (HTML) の Web リソース](webpage-html-web-resources.md)<br />
[スクリプト (JScript) Web リソース](script-jscript-web-resources.md)<br />
[画像 (JPG、PNG、GIF、ICO) の Web リソース](image-web-resources.md)<br />
[スタイルシート (XSL) Web リソース](stylesheet-xsl-web-resources.md)<br />
[データ (XML) Web リソース](data-xml-web-resources.md)<br />
[CSS Web リソース](css-web-resources.md)<br />
[RESX Web リソース](resx-web-resources.md)<br />
[Web リソース エンティティの参照](../common-data-service/reference/entities/webresource.md)<br />
[サンプル: データ パラメーターを使用した Web リソースへの複数の値の引き渡し](sample-pass-multiple-values-web-resource-through-data-parameter.md)<br />
[サンプル: Web リソースとしてファイルをインポート](sample-import-files-web-resources.md)<br />
