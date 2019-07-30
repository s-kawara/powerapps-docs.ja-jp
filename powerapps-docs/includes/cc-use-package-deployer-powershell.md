---
ms.openlocfilehash: 215a6d9fb0890bd6d93843b0b649ada4203e5600
ms.sourcegitcommit: ad203331ee9737e82ef70206ac04eeb72a5f9c7f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/18/2019
ms.locfileid: "67224200"
---
Package Deployer ツールの PowerShell ファイルは [NuGet パッケージ](https://go.microsoft.com/fwlink/?linkid=859211)に含まれています。 これを使用するには、**nuget.exe.** を使用し、Package Deployer をダウンロードしてローカル コンピューターに抽出する必要があります。<br/><br/>

<https://www.nuget.org/downloads> から **nuget.exe** をダウンロードし、コンピューターの **d:\\** などに保存します。 コマンド プロンプトで次のコマンドを実行し、パッケージの中身をコンピューター上のフォルダー (たとえば、**PD-PowerShell**) に抽出します。<br/>

`d:\nuget install Microsoft.CrmSdk.XrmTooling.PackageDeployment.PowerShell -Version [VERSION] -O d:\PD-PowerShell`<br/><br/>
    
Package Deployer ツールの PowerShell ファイルを抽出したら、`[ExtractedLocation]\tools` フォルダーに移動し、必要なファイルを見つけます。 
