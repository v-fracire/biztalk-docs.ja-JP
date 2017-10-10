---
title: "チェックリスト: BizTalk アプリケーションの配置 |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- checklists, deploying
- applications, deploying
- deploying [applications], checklists
- checklists, applications
- applications, checklists
ms.assetid: 0f936475-eea7-49b0-a4ea-9488b4ce3847
caps.latest.revision: "18"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 76384f4684d22d2e8293013598d82a25a0543876
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="checklist-deploy-a-biztalk-application"></a>チェックリスト: BizTalk アプリケーションを展開します。
|手順|リファレンス|  
|----------|---------------|  
|BizTalk アプリケーションの展開機能について説明します。 また、バインド ファイルを使用して、アプリケーションをすばやく簡単に展開する方法についても説明します。|[BizTalk アプリケーションの展開と管理を理解する](../core/understanding-biztalk-application-deployment-and-management.md)、[バインド ファイルとアプリケーションの展開](../core/binding-files-and-application-deployment.md)|  
|展開を実行するための適切なアクセス許可があることを確認します。|[展開して、BizTalk アプリケーションの管理に必要なアクセス許可](../core/permissions-required-for-deploying-and-managing-a-biztalk-application.md)|  
|[!INCLUDE[btsVStudioNoVersion](../includes/btsvstudionoversion-md.md)] で、BizTalk ソリューション内の各プロジェクトの展開プロパティを設定します。 このプロパティには、データベース サーバーの名前、グループの BizTalk 管理データベースの名前、および展開先 BizTalk アプリケーションの名前が含まれます。 再展開を有効にして、再展開時にホスト インスタンスを自動的に再起動するオプションを指定することもできます。|[Visual Studio での展開のプロパティを設定する方法](../core/how-to-set-deployment-properties-in-visual-studio.md)|  
|[!INCLUDE[btsVStudioNoVersion](../includes/btsvstudionoversion-md.md)] から BizTalk アセンブリを展開先アプリケーションに展開します。|[Visual Studio から BizTalk アセンブリを展開する方法](../core/how-to-deploy-a-biztalk-assembly-from-visual-studio.md)|  
|.NET アセンブリ、Readme ファイル、環境固有のバインド ファイル、およびスクリプトを追加したり、ポートや受信場所を構成したりして、BizTalk アプリケーションを完成させます。 さらに、ファイルの格納場所などのインフラストラクチャをホスト コンピューターに追加します。|[作成して、BizTalk アプリケーションを変更する](../core/creating-and-modifying-biztalk-applications.md)、[バインド ファイルとアプリケーションの展開](../core/binding-files-and-application-deployment.md)|  
|BisTalk アプリケーションを .msi ファイルにエクスポートします。この .msi ファイルは、アプリケーションを別の BizTalk グループにインポートしたり、アプリケーションを必要なコンピューターにインストールする際に使用します。|[BizTalk アプリケーションをエクスポートする方法](../core/how-to-export-a-biztalk-application.md)|  
|.msi ファイルをインポートして、展開先の BizTalk グループ内に BizTalk アプリケーションを作成します。 環境固有のバインド ファイルを追加した場合は、インポート時に適用するバインドを選択できます。|[BizTalk アプリケーションをインポートする方法](../core/how-to-import-a-biztalk-application.md)|  
|ポート構成の変更など追加の変更をアプリケーションに加えて、アプリケーションが展開先の環境で動作するようにします。 アプリケーションに何らかの変更を加えた場合は、実行するコンピューターにアプリケーションをインストールする際に使用する .msi ファイルにアプリケーションをエクスポートします。 必要に応じて、別の展開先 BizTalk グループにアプリケーションをインポートすることもできます。|[作成して、BizTalk アプリケーションを変更する](../core/creating-and-modifying-biztalk-applications.md)、[アプリケーションにバインド ファイルを追加する方法](../core/how-to-add-a-binding-file-to-an-application2.md)、[を BizTalk アプリケーションをエクスポートする方法](../core/how-to-export-a-biztalk-application.md)、 [BizTalk をインポートする方法アプリケーション](../core/how-to-import-a-biztalk-application.md)|  
|.msi ファイルを使用して、アプリケーションを実行するすべてのコンピューターにアプリケーションをインストールし、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 管理コンソールからアプリケーションを起動します。|[BizTalk アプリケーションをインストールする方法](../core/how-to-install-a-biztalk-application.md)|  
  
## <a name="see-also"></a>参照  
 [BizTalk アプリケーションの展開と管理のチェックリスト](../core/biztalk-application-deployment-and-management-checklists.md)