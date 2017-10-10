---
title: "ApplicationManager (BizTalk Server サンプル) |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 51ebe7a8-a0ca-4d2a-bf40-ec6421ba5a95
caps.latest.revision: "13"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: e352eb3ffb5418d7d109b5c0f574689c67f969f4
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="applicationmanager-biztalk-server-sample"></a>ApplicationManager (BizTalk Server サンプル)
ApplicationManager サンプルでは、管理オブジェクトを使用して BizTalk アプリケーションを開始または停止する方法を示します。  
  
## <a name="prerequisites"></a>前提条件  
  
-   このサンプルの管理オブジェクトを使用するには、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 管理者特権が必要です。  
  
-   Windows PowerShell スクリプトを実行するには、Windows PowerShell 実行ポリシーが必要です。 詳細については、次を参照してください。:[実行ポリシーの確認](http://go.microsoft.com/fwlink/?LinkId=128930)です。  
  
## <a name="what-this-sample-does"></a>このサンプルの処理  
 このサンプルを使用して、 **BtsCatalogExplorer**と**アプリケーション**クラス、 **Microsoft.BizTalk.ExplorerOM**を開始および停止、展開済みの名前空間 BizTalk アプリケーション。 サンプルは Microsoft [!INCLUDE[btsVCSharp](../includes/btsvcsharp-md.md)] で作成されています。 このトピックには、Windows PowerShell のスクリプト例も含まれています。 このサンプルは次の操作を示します。  
  
-   使用して、BizTalk 管理データベースに接続する、 **BtsCatalogExplorer**クラスです。  
  
-   アプリケーション インスタンスを検索する**BtsCatalogExplorer**アプリケーション名に基づいています。  
  
-   アプリケーションの開始コマンドまたは停止コマンドを実行する。  
  
## <a name="where-to-find-this-sample"></a>このサンプルの場所  
 このサンプルは、SDK がある次の場所にあります。  
  
 \<*パスのサンプル*> \Admin\ExplorerOM\ApplicationManager  
  
 次の表は、このサンプルのファイルとその目的を示しています。  
  
|ファイル|Description|  
|---------------|-----------------|  
|Program.cs|このサンプルに示されている操作の [!INCLUDE[btsVCSharp](../includes/btsvcsharp-md.md)] ソース ファイル。|  
|ApplicationManager.sln、ApplicationManager.csproj、ApplicationManager.suo|このサンプルのソリューション ファイルとプロジェクト ファイル。|  
  
## <a name="building-and-running-this-sample"></a>このサンプルのビルドおよび実行  
  
#### <a name="to-build-this-sample"></a>このサンプルをビルドするには  
  
1.  [!INCLUDE[btsVStudioNoVersion](../includes/btsvstudionoversion-md.md)] で、ソリューション ファイル ApplicationManager.sln を開きます。  
  
2.  **[ビルド]** メニューの **[ソリューションのビルド]**をクリックします。  
  
#### <a name="to-run-this-sample"></a>このサンプルを実行するには  
  
1.  コマンド ウィンドウを開き、次のフォルダーに移動します。  
  
     \<*パスのサンプル*> \Admin\ExplorerOM\ApplicationManager\bin\Debug  
  
2.  次の 2 つのコマンドライン引数を順番どおりに指定して、ApplicationManager.exe ファイルを実行します。  
  
    -   **\<開始 (&) #124 です。 停止 >**最初の引数は、展開されたアプリケーションで実行する操作。  
  
    -   **\<ApplicationName >** 2 番目の引数は、展開されたアプリケーションの名前。  
  
     例:  
  
    ```  
    ApplicationManager.exe stop MyBizTalkApp  
    ```  
  
     一部のコマンドライン パラメーターのみを指定してサンプルを実行すると、使用する構文が表示されます。 例:  
  
    ```  
    Usage:  
  
    ApplicationManager <start|stop> <Application Name>  
  
     Where:  
      <Application Name> = The name of the application that needs to be changed  
  
    Example: ApplicationManager start Application1  
    ```  
  
## <a name="windows-powershell-script-example"></a>Windows PowerShell スクリプトの例  
 次の Windows PowerShell スクリプト フラグメントは、の同じ機能を示すために使用できます、 **ExplorerOM**クラス。  
  
```  
#=== Make sure the ExplorerOM assembly is loaded ===#  
  
[void] [System.reflection.Assembly]::LoadWithPartialName("Microsoft.BizTalk.ExplorerOM")  
  
#=== Connect the BizTalk Management database ===#  
  
$Catalog = New-Object Microsoft.BizTalk.ExplorerOM.BtsCatalogExplorer  
$Catalog.ConnectionString = "SERVER=.;DATABASE=BizTalkMgmtDb;Integrated Security=SSPI"  
  
#=== Loop through applications in the catalog trying to find a name match ===#  
  
foreach($app in $Catalog.Applications)  
{  
    if ($($app.Name) -ieq $args[1])  
    {  
  
        #=== The first command-line argument should be "start" or "stop" ===#  
  
        if ($args[0] -ieq "start")  
        {  
            Write-Host `r`nIssuing start command to $app.Name...`r`n  
            $app.Start([Microsoft.BizTalk.ExplorerOM.ApplicationStartOption] "StartAll")  
            $Catalog.SaveChanges()  
        }  
  
        if ($args[0] -ieq "stop")  
        {  
            Write-Host `r`nIssuing stop command to $app.Name...`r`n  
            $app.Stop([Microsoft.BizTalk.ExplorerOM.ApplicationStopOption] "StopAll")  
            $Catalog.SaveChanges()  
        }  
  
    }  
}  
```  
  
 このスクリプトは、[!INCLUDE[btsVCSharp](../includes/btsvcsharp-md.md)] サンプルと同じコマンドライン引数を受け取ります。 Windows PowerShell スクリプトを実行して、展開されている BizTalk アプリケーションを開始する例を次に示します。  
  
```  
PS C:\> .\ApplicationManager.ps1 start MyBizTalkApp  
  
Issuing start command to MyBizTalkApp ...  
```  
  
## <a name="see-also"></a>参照  
 [Admin ExplorerOM (BizTalk Server Samples フォルダ)](../core/admin-explorerom-biztalk-server-samples-folder.md)