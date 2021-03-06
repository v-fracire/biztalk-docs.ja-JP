---
title: Visual Studio からアセンブリを展開するときの動作 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 421df529-1ddb-4f49-a40a-c06f2a434ffc
caps.latest.revision: 10
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: c74336e90e1ac58088de0d528695dbfed617d9b5
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36985267"
---
# <a name="what-happens-when-you-deploy-an-assembly-from-visual-studio"></a>Visual Studio からアセンブリを展開する場合の動作
このトピックでは、[!INCLUDE[btsVStudioNoVersion](../includes/btsvstudionoversion-md.md)] から [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 上の BizTalk アプリケーションにアセンブリを展開する場合の動作について説明します。  
  
 プロジェクトは個別に展開したり、ソリューション内のすべてのプロジェクトを同時に展開したりできます。 プロジェクトを展開する前に、個別にまたは、ソリューションの一部として指定するプロジェクトのプロパティでアセンブリの展開先アプリケーション」の説明に従って[Visual Studio の配置プロパティを設定する方法](../core/how-to-set-deployment-properties-in-visual-studio.md)します。 [!INCLUDE[btsVStudioNoVersion](../includes/btsvstudionoversion-md.md)] でプロジェクトまたはソリューションを展開すると、アセンブリは自動的にビルドされ、指定したアプリケーションに展開されます。 ローカルの BizTalk グループにプロジェクト プロパティで指定したアプリケーションと同じ名前の既存のアプリケーションがある場合、アセンブリはその既存のアプリケーションに展開されます。それ以外の場合、指定した名前のアプリケーションが新しく作成され、作成されたアプリケーションにアセンブリが展開されます。 このプロセスの一部として、アセンブリは、アセンブリに含まれるオーケストレーション、パイプライン、スキーマ、およびマップ (これらは "アイテム" と呼ばれます) と共にローカルの BizTalk 管理データベースにインポートされ、データベース内で指定したアプリケーションに関連付けられます。  
  
 プロジェクトをソリューションに含めて同時に展開する場合でも、ソリューション内のプロジェクトは同じ BizTalk アプリケーションまたは異なる BizTalk アプリケーションに展開できます。 次の図は、[!INCLUDE[btsVStudioNoVersion](../includes/btsvstudionoversion-md.md)] の BizTalk ソリューションに含まれる 3 つのアセンブリを、2 つの異なる BizTalk アプリケーションに展開する場合を示しています。  
  
 ![BizTalk アセンブリを展開](../core/media/visualstudiodeploy.gif "VisualStudioDeploy")  
  
 プロジェクトまたはソリューションを展開したら、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 管理コンソールや BTSTask コマンド ライン ツールを使用して、アセンブリおよびそのアイテムを表示したり管理したりすることができます。  
  
## <a name="destination-locations"></a>展開先  
 [!INCLUDE[btsVStudioNoVersion](../includes/btsvstudionoversion-md.md)] からアセンブリを展開する場合、既定では、アセンブリの展開先はアセンブリの展開元です。 [!INCLUDE[btsVStudioNoVersion](../includes/btsvstudionoversion-md.md)] からアセンブリをインストールまたはエクスポートするときに、"インストール元" と "インストール先" の環境が同じでない場合、インストールは失敗します。 たとえば、インストール元が D:[path]/[filename] であり、ターゲット コンピューター、つまりインストール先のコンピューターに "D" ドライブがない場合、このインストールは失敗します。  
  
 この動作は、BizTalk 管理者を使用してリソースを追加する動作とは対照的です。リソースを追加するときの既定のインストール先は %BTAD_InstallDir% です。 この環境変数は、インストールで指定したインストール ディレクトリに展開されます。  
  
 この問題を解決するには、以下の手順に従います。  
  
1. [!INCLUDE[btsVStudioNoVersion](../includes/btsvstudionoversion-md.md)] で、アセンブリを展開します。  
  
2. アセンブリが展開されたら、BizTalk 管理者を開きます。  
  
3. 必要に応じて、展開先を変更します。 たとえば、展開先を %BTAD_InstallDir% などに変更します。  
  
   展開先を変更したら、以後同じアセンブリを再展開する場合は、この新しい場所が既定値として使用されます。  
  
   詳細については、次を参照してください。 [Visual Studio から BizTalk アセンブリを展開する方法](../core/how-to-deploy-a-biztalk-assembly-from-visual-studio.md)します。  
  
## <a name="deploying-solutions-vs-projects"></a>Vs のソリューションを展開します。プロジェクト  
 展開する場合は、個別のプロジェクトではなく、常にソリューションを展開することを強くお勧めします。 個別のプロジェクトの展開では、展開するアセンブリと別のアセンブリとの間に依存関係がある場合、展開を完了するまでにいくつかの手順を実行しなければなりません。 しかし、ソリューションを展開すると、アセンブリ間の依存関係を管理するための手順はすべて [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] が自動的に実行します。 詳細については、次を参照してください。 [Visual Studio から BizTalk アセンブリを再デプロイする方法](../core/how-to-redeploy-a-biztalk-assembly-from-visual-studio.md)します。  
  
 次の図は、ソリューションを展開した場合に、依存関係のあるアセンブリを再展開するために [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] によって実行される手順を示しています。  
  
 ![ソリューションのアセンブリを展開する](../core/media/deployassemblies.gif "DeployAssemblies")  
  
## <a name="see-also"></a>参照  
 [Visual Studio から BizTalk アプリケーションへの BizTalk アセンブリの展開](../core/deploying-biztalk-assemblies-from-visual-studio-into-a-biztalk-application.md)