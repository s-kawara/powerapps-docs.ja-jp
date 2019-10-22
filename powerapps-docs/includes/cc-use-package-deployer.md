---
ms.openlocfilehash: a108a9ee6f9033851b2f55beb071a1e7cae254dd
ms.sourcegitcommit: ad203331ee9737e82ef70206ac04eeb72a5f9c7f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/18/2019
ms.locfileid: "67224260"
---
Package Deployer ツールは [NuGet パッケージ](https://go.microsoft.com/fwlink/?linkid=859205)に含まれています。 Package Deployer を使用するには、**nuget.exe.** を使用し、Package Deployer をダウンロードしてローカル コンピューターに抽出する必要があります。<br/><br/>

<https://www.nuget.org/downloads> から **nuget.exe** をダウンロードし、コンピューターの **d:\\** などに保存します。 コマンド プロンプトで次のコマンドを実行し、パッケージの中身をコンピューター上のフォルダー (たとえば、**PD**) に抽出します。<br/>

`d:\nuget install Microsoft.CrmSdk.XrmTooling.PackageDeployment.Wpf -Version [VERSION] -O d:\PD`<br/><br/>
    
Package Deployer ツールを抽出したら、`[ExtractedLocation]\tools` フォルダーに移動し、**PackageDeployer.exe** ファイルを見つけます。 
