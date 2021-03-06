---
title: BAM イベント ソフトウェアのインストール |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a3638d34-f5a8-4ffd-99eb-d38aed4c0732
caps.latest.revision: 14
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: ca5d13e058799113d7847fe6377ce82c7e0a7ea5
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "37000291"
---
# <a name="installing-the-bam-eventing-software"></a>BAM イベント ソフトウェアのインストール
BAM イベント API を使用する BAM ソリューションを実装するか、または Windows Workflow Foundation 用に BAM インターセプターを使用するように Windows Workflow Foundation または Windows Communication Foundation アプリケーションを構成するには、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] セットアップ プログラムを使って BAM イベント ソフトウェアをインストールする必要があります。 このソフトウェアは、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] ランタイムの一部としてインストールするか、または [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] セットアップ アプリケーションで [追加ソフトウェア] の [BAM イベント サポート] を選択して単独でインストールできます。  
  
### <a name="to-install-the-bam-eventing-software"></a>BAM イベント ソフトウェアをインストールするには  
  
1. WF アプリケーションをホストするコンピューターに、管理者特権を持つアカウントでログオンします。  
  
2. [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] インストール CD からセットアップ プログラムを実行します。  
  
3. 選択されたオプションをすべてオフにします。 この手順を実行しないと、不要なソフトウェアがインストールされる場合があります。  
  
4. 展開**追加ソフトウェア**を選び、 **BAM イベント**チェック ボックスをオンします。  
  
5. **[次へ]** をクリックします。  
  
6. **[インストール]** をクリックします。  
  
7. インストール手順が完了したら、クリックして**OK**します。  
  
    これで BAM イベント ソフトウェアがインストールされます。  
  
> [!NOTE]
>  この方法で BAM インターセプター ライブラリをインストールする場合は、追加のライセンスを購入する必要がありません。  
  
 BAM インターセプターのパフォーマンス カウンター データを監視する場合は、まず InstallUtil.exe を使用してパフォーマンス カウンターを登録する必要があります。  
  
### <a name="to-register-bam-interceptor-performance-counters-by-using-installutilexe"></a>InstallUtil.exe を使用して BAM インターセプター パフォーマンス カウンターを登録するには  
  
1. 開始**[!INCLUDE[btsVStudioNoVersion](../includes/btsvstudionoversion-md.md)]コマンド プロンプト**に管理者として。  
  
2. コマンド プロンプトで次のコマンドを入力します。  
  
    InstallUtil [!INCLUDE[btsBiztalkServerPath](../includes/btsbiztalkserverpath-md.md)]Tracking\Microsoft.BizTalk.Bam.Interceptors.dll  
  
3. 型**終了**、し、enter キーを押してコマンド プロンプトを閉じます。  
  
    これで BAM インターセプター パフォーマンス カウンターが使用可能になります。  
  
> [!NOTE]
>  既定では、管理者アカウントと一部のシステム アカウントにのみ、パフォーマンス データをログに記録するアクセス許可が与えられます。 [!INCLUDE[btsWinSvrNoVersion](../includes/btswinsvrnoversion-md.md)] でのアクセスを可能にするには、ワークフロー アプリケーションの実行に使用するアカウントを Performance Log Users グループに追加します。  
  
## <a name="see-also"></a>参照  
 [BAM ソリューションを実装します。](../core/implementing-bam-solutions.md)   
 [BizTalk Server 2013 および 2013 R2 のインストール概要](http://msdn.microsoft.com/library/8041926c-cfc9-4eaf-9c28-a2c6e8015bc5)