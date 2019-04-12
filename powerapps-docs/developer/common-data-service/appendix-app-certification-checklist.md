---
title: '付録: アプリの認証チェックリスト (PowerApps) | Microsoft Docs'
description: アプリ認定チェックリストはモデル駆動型の確認に関する情報を提供し、キャンバス アプリとフローは AppSource に公開する前に通過する必要があります。
ms.custom: ''
ms.date: 03/20/2019
ms.reviewer: kvivek
ms.service: powerapps
ms.topic: article
author: omarcdoc
ms.author: omarc
manager: AnnBe
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="appendix-app-certification-checklist"></a>付録: アプリの認証チェックリスト

次のチェックリストは、アプリを [送信](next-steps-submit-app-cloud-partner-portal.md) した後の認定プロセスで Microsoft によって実行される検証の一覧です。 

<table>
<tbody>
<tr>
<th>アプリ</th>
<th>検証の種類</th>
<th>認定チェックリスト</th>
</tr>
<tr>
<td rowspan=5>Common Data Service に接続する <a href="https://docs.microsoft.com/powerapps/maker/model-driven-apps/model-driven-app-overview">モデル駆動型アプリ</a>、<a href="https://docs.microsoft.com/powerapps/maker/canvas-apps/getting-started">キャンバス アプリ</a>、そして <a href="https://docs.microsoft.com/flow/getting-started">フロー</a><br/><br/><strong>注意</strong>: Dynamics 365 for Customer Engagement アプリはモデル駆動型アプリです。</td>
<td>正常性確認</td>
<td><ul>
<li>アプリ登録の種類を確認: 無料、試用版またはお問い合わせ お問い合わせに登録されている場合、発行者はテスト ドライブを有効にする必要があります。</li>
<li>送信済みの <a href="https://docs.microsoft.com/powerapps/developer/common-data-service/create-package-app-appsource">パッケージ</a> が AppSource での公開に必要なすべてのアーティファクトを含んでいることを確認してください。</li>
<li>クラウド パートナー ポータルからエンド ツー エンド (E2E) 機能ドキュメントをダウンロードし、ドキュメントが機能シナリオとユーザー / 管理者の体験で更新されていることを検証します。</li>
</ul>
</td>
</tr>
<tr>
<td>コード検証</td>
<td>
<ul>
<li>キャンバス アプリのコード検証は PowerApps の <a href="https://docs.microsoft.com/en-us/powerapps/maker/canvas-apps/accessibility-checker">アクセシビリティ チェッカー ツール</a> によって行われ、以下を確認します:
<ul>
<li>静的計算式エラーと警告: なにか問題が見つかった場合は、認証チームがフィードバックを共有して解決し AppSource に再送信します。</li>
<li>実行時エラー: アプリを実行モードで開いて表示する時に発生する可能性があります。 問題が見つかったらすべて電子メールで報告されます。</li>
<li>ユーザー補助のエラーと警告: ユーザー補助のエラーはすべてソリューション チェッカーのガイドラインに従って解決する必要があります。</li>
</ul></li>
<li>Common Data Service ソリューションのコード検証は <a href="https://experienceisv.microsoftcrmportals.com/precertification/#/">オンデマンド コード分析 (ODCA)</a> ツールを通じて行われます。</li>
<li>ODCA から報告された問題は手動で正確さが検証され、誤検知した問題は重大度が低く抑えられます。</li>
<li>生成されたレポートは電子メールで発行者と共有されます。</li>
</ul>
</td>
</tr>
<tr>
<td>展開の検証</td>
<td>
<ul>
<li>ソリューションは <a href="https://docs.microsoft.com/powerapps/developer/common-data-service/package-deployer/create-packages-package-deployer">Package Deployer</a> を使用して PowerApps Studioにインストールされます。 インストールされたキャンバス アプリは、ソリューションおよびアプリ セクションにインストール後に手動で配置されます。そしてアプリが編集モードおよび実行モードで開かれていることを確認します。 キャンバス アプリが PowerApps Studio から手動で削除され、アンインストールが成功したことを確認します。</li>
<li>キャンバス アプリが発行者から提供されたコネクタを介して正しく接続していることを確認します。 たとえば、Common Data Service やその他の接続です。</li>
<li>すべての Common Data Service コンポーネント (エンティティ、Web リソース、プラグイン、およびその他のコンポーネント) がソリューションで利用可能なことを確認してください。</li>
<li>ソリューションを手動でアンインストールし、管理ソリューションに関連付けられたすべてのコンポーネントが削除されたかを確認します。</li>
</ul>
</td>
</tr>
<tr>
<td>機能の検証</td>
<td>
<ul>
<li>発行者が共有する機能ドキュメントに基づいてアプリの機能を検証します。 アプリに実装されたすべての機能が通過する必要があります。</li>
<li>発行者はクラウド パートナー ポータルを通じて E2E 機能ドキュメントを送信するか、電子メールを通じてビデオ リンクを共有することができます。</li>
<li>アプリがライセンス構成を必要とする場合、認証チームは必要なライセンスを更新するために発行者にインスタンス詳細を共有します。</li>
</ul></td>
</tr>
<tr>
<td>セキュリティの検証</td>
<td>
<ul>
<li>外部データ ソースまたはアクセスを必要とする接続にキャンバス アプリが接続しているかどうか、また適切な接続の詳細を E2E ドキュメントで共有する必要があるかどうかを確認します。</li>
<li>キャンバス アプリが PowerApps コネクタ以外の任意の外部接続に接続することを確認します。</li>
<li>Package Deployer 内で提供されているすべてのカスタム コードを確認してください。 AppSource にアプリを承認する前にコードを検証してください。</li>
<li>カスタム コードが対象の環境から顧客データを取得しているかを確認するにはコードを手動で検証します。</li>
</ul>
</td>
</tr>
<tr>
<td rowspan=5>Common Data Service の<i>他</i> にもデータ ソースに接続する <a href="https://docs.microsoft.com/powerapps/maker/canvas-apps/getting-started">キャンバス アプリ</a> および <a href="https://docs.microsoft.com/flow/getting-started">フロー</a>
</td>
<td>正常性確認</td>
<td><ul>
<li>キャンバス アプリが有効な .msapp ファイルを含んでいることを確認します。</li>
<li>パッケージ フォルダが、マニフェスト、Jason、その他の画像コンポーネントなど、必要なコンポーネントをすべて含んでいることを確認します。</li>
</ul>
</td>
</tr>
<tr>
<td>コード検証</td>
<td><ul>
<li>先に説明したのと同じ Common Data Service に接続する モデル駆動型アプリ、キャンバス アプリ、そして フロー</li></ul>
</td>
</tr>
<tr>
<td>展開の検証</td>
<td>
<ul>
<li>キャンバス アプリはアプリ インポート機能を使用して PowerApps Studio に手動でインストールされます。 インストールされたキャンバス アプリは、アプリ セクションにインストール後に手動で配置されます。そしてアプリが編集モードおよび実行モードで開かれていることを確認します。 キャンバス アプリが PowerApps Studio から手動で削除され、アンインストールが成功したことを確認します。</li>
<li>キャンバス アプリが発行者から提供されたコネクタに正しく接続していることを確認します。</li>
</ul>
</td>
</tr>
<tr>
<td>機能の検証</td>
<td>
<ul>
<li>先に説明したのと同じ Common Data Service に接続する モデル駆動型アプリ、キャンバス アプリ、そして フロー</li></ul></td>
</tr>
<tr>
<td>セキュリティの検証</td>
<td>
<ul>
<li>先に説明したのと同じ Common Data Service に接続する モデル駆動型アプリ、キャンバス アプリ、そして フロー</li></ul>
</td>
</tr>
</tbody>
</table>

作成のベスト プラクティスの詳細:
- キャンバス アプリは [キャンバス アプリのコード標準とガイドライン](https://aka.ms/powerappscanvasguidelines) を参照してください。
- モデル駆動型アプリは [モデル駆動型アプリのコンポーネントについて](https://docs.microsoft.com/powerapps/maker/model-driven-apps/model-driven-app-components) を参照してください。

  




  

