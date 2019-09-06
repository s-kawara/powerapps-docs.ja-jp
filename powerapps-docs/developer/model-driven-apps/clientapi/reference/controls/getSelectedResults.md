---
title: getSelectedResults (クライアント API 参照)| MicrosoftDocs
ms.date: 10/31/2018
ms.service: powerapps
ms.topic: reference
ms.assetid: 4d025f92-db16-440c-9f82-e40d71e09862
author: KumarVivek
ms.author: kvivek
manager: annbe
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getselectedresults-client-api-reference"></a>getSelectedResults (クライアント API 参照)


このメソッドを使用して、検索コントロールの現在選択した結果を取得します。 現在選択した結果も、現在開かれている結果を表します。 

## <a name="control-types-supported"></a>サポートされているコントロールの種類

サポート情報検索コントロール

## <a name="syntax"></a>構文

```
var kbSearchControl = formContext.getControl("<name>");
var kbSearchResult = kbSearchControl.getSelectedResults();
```

## <a name="return-value"></a>戻り値 

**KBSearchResult** 現在選択されている結果。

## <a name="kbsearchresult-properties"></a>KBSearchResult プロパティ

| **プロパティ**        | **型** | **説明**  |
|---------------------|----------|------------------|
| **回答**          | String   | 記事のコンテンツを含む HTML マークアップ。 このコンテンツは、顧客に送信する電子メールにそのコンテンツを組み込むことができるユーザー定義アクションに渡すことができます。 |
| **articleId**       | String   | 代替キーとして使用される記事IDです。 この値を使用して、この記事が Common Data Service 内に既に存在するかどうかを確認できます。|
| **articleUid**      | String   | 一意の記事IDです。 この値は、代替キーとして使用されます。 この ID は、記事がまだ存在しない場合に、記事の関連付けの間に新しい サポート情報レコードを作成するために必要です。 |
| **attachmentCount** | 番号   | 記事の添付ファイルの数です。 |
| **createdOn**       | Date     | 記事が作成された日付。 この値では、ユーザーの現在のタイム ゾーンと形式が使用されます。 記事の経過年数をビジネス ロジックで使用する場合は、使用することもできます。 |
| **expiredDate**     | Date     | 記事の期限が切れた日付、また切れる日付。 この日付と現在の日付を比較して、記事が期限切れになったかどうかを比較できます。 この値では、ユーザーの現在のタイム ゾーンと形式が使用されます。|
| **folderHref**      | String   | 記事のフォルダーパスへのリンクです。|
| **href**            | String   | 記事へのダイレクトリンクです。|
| **isAssociated**    | Boolean  | 記事が親レコードに関連付けられているかどうかを示します。 フォーム スクリプトを使用して、またはフォーム スクリプトによって起動された別のプロセスで、記事を現在のレコードに関連付ける前に、この値を確認できます。 |
| **lastModifiedOn**  | Date     | 記事が最後に修正された日付。 この値では、ユーザーの現在のタイム ゾーンと形式が使用されます。 |
| **publicUrl**       | String   | 記事のポータル URL をサポートします。 [ポータル URL] オプションをオフにすると、空白になります。 ユーザー定義アクションを使用して、これを、顧客に送信する電子メールのコンテンツ内のリンクに組み込みます。 |
| **published**       | Boolean  | 記事が公開済みの状態にあるかどうかを示します。 公開されている場合は **True** 、それ以外は **False** です。 記事に関する情報を顧客に送信する前に、記事が公開されているかどうかを確認する必要があります。 |
| **質問**        | String   | 記事のタイトル。 どのビジネス プロセスにおいても記事を参照する場合に、この値を使用して名前で記事を参照できます。  |
| **rating**          | 番号   | 記事の評価。  |
| **searchBlurb**     | String   | 検索クエリで見つかった領域を含む、記事のコンテンツの短い断片。 これを使用して、検索リスト内でユーザーに記事を少しだけ見せて、これが探している記事であるかどうかの判断を助けます。 |
| **serviceDeskUri**  | String   | 記事へのリンクです。 このリンクを使用して記事を開きます。   |
| **timesViewed**     | 番号   | 顧客によってポータルで記事が閲覧された回数。  |