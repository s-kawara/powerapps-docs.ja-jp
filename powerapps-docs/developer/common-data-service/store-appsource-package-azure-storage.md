---
title: '手順 5: AppSource パッケージを Azure Storage に保存し、SAS キーで URL を生成する (Common Data Service for Apps) | Microsoft Docs'
description: ファイルのセキュリティを維持するには、すべてのアプリ開発者は Microsoft Azure Blob Storage のアカウントに AppSource パッケージ ファイルを保存し、Shared Access Signature (SAS) キーを使用してパッケージ ファイルを共有する必要があります。 パッケージ ファイルは、認証のため、その後 AppSource 試用版のために Azure Storage から取得されます。
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: shmcarth
ms.author: jdaly
manager: ryjones
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="step-5-store-your-appsource-package-on-azure-storage-and-generate-a-url-with-sas-key"></a>手順 5: AppSource パッケージを Azure Storage に保存し、SAS キーで URL を生成する

Microsoft Azure Storage は、いつでも利用でき、セキュリティ保護された、永続的な、拡大縮小可能な、冗長なストレージを提供する Microsoft が管理するクラウド サービスです。 詳細については、「[Microsoft Azure Storage の概要](https://docs.microsoft.com/azure/storage/common/storage-introduction)」を参照してください。

ファイルのセキュリティを維持するには、すべてのアプリ開発者は Microsoft Azure Blob Storage のアカウントに AppSource パッケージ ファイルを保存し、Shared Access Signature (SAS) キーを使用してパッケージ ファイルを共有する必要があります。 パッケージ ファイルは、認証のため、その後 AppSource 試用版のために Azure Storage から取得されます。

## <a name="before-you-upload-your-package"></a>パッケージをアップロードする前に

Microsoft Azure Storage Explorer を [http://storageexplorer.com](http://storageexplorer.com) からダウンロードしてインストールします 。

Azure Storage Explorer を使用すると、ストレージ アカウントの内容を簡単に管理できます。

## <a name="upload-your-package-and-generate-a-url-with-sas-key"></a>パッケージをアップロードして、SAS キーで URL を作成する

パッケージを Azure Blob Storage にアップロードするには、以下の手順に従います。

1. [https://azure.microsoft.com](https://azure.microsoft.com) の Azure アカウントに移動すると、無料の試用版を作成するか、または支払います。
2. [https://portal.azure.com](https://portal.azure.com) で Azure 管理ポータルにサインインします。
3. **ストレージ** > **ストレージ アカウント - BLOB、ファイル、テーブル、キュー**をクリックして新しいストレージ アカウントを作成します。
    
   ![](media/appsource-storageaccount-pic1.png)

4. **ストレージ アカウントの作成**ページで、ストレージ アカウントの**名前**、**リソース グループ**、および**場所**を指定します。 残りのフィールドはデフォルト オプションのままにしておきます。 **作成**をクリックします。 

   ![](media/appsource-storageaccount-pic2.png)
 
  
5. ストレージ アカウントが作成されたら、新しく作成されたリソース グループに移動し、新しい BLOB コンテナーを作成します。 **BLOB サービス**の下で、**コンテナー**を選択してから、 **+ コンテナー**を選択します。

   ![](media/appsource-storageaccount-pic3.png)

6. コンテナーの名前を指定し、**BLOB** として**パブリック アクセス レベル**を選択します。 **OK** をクリックします。

   ![](media/appsource-storageaccount-pic4.png)

7. コンピューターで Azure Storage Explorer を起動し、Azure Storage アカウントを作成したときと同じアカウントを使用してサインインすることで、Azure Storage アカウントに接続します。

8. Azure Storage Explorer で、新しく作成されたコンテナーを選択してから、**アップロード** > **ファイルのアップロード**を選択して、[手順4: アプリの AppSource パッケージを作成する](create-package-app-appsource.md) で作成したアプリ ソース パッケージをアップロードします。 

   ![](media/appsource-storageaccount-pic5.png)

9. コンピューター上の AppSource パッケージ ファイルを参照し、それをアップロードすることを選択します。

10. アップロードされた AppSource パッケージ ファイルを右クリックし、**Shared Access Signature の入手**を選択します。

    ![](media/appsource-storageaccount-pic6.png)

11. **Shared Access Signature** ページで、**有効期限**値を修正して Shared Access Signature (SAS) を**開始時間**から 1 か月間アクティブにします。 **作成**をクリックします。

    ![](media/appsource-storageaccount-pic7.png)

12. 次のページに、生成された SAS 情報に関する情報が表示されます。 **URL** 値をコピーして、後で使用するために保存します。 クラウド パートナー ポータルでプランの作成中にこの URL を指定する必要があります。

    ![](media/appsource-storageaccount-pic8.png)


> [!div class="nextstepaction"]
> [次の手順: クラウド パートナー ポータル上のアプリの送信](next-steps-submit-app-cloud-partner-portal.md)