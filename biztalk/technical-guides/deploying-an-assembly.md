---
title: アセンブリを展開する |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 65f8ee21-0e52-4a74-b114-864a3069659c
caps.latest.revision: 2
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 5fb363b6060b0c06436b36202100e855062c026f
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36984771"
---
# <a name="deploying-an-assembly"></a>アセンブリを展開します。
アセンブリを展開するアセンブリがビルドされ、オーケストレーション、パイプライン、スキーマ、およびローカルの BizTalk 管理データベースに格納されているマップ (アイテム) と共にインポートします。 最初に、この開発環境で行われます。  
  
 また、展開は、Visual Studio 内のプロジェクト プロパティで指定した BizTalk アプリケーションとアセンブリを関連付けます。 ソリューションを展開したら、BizTalk Server 管理コンソールや BTSTask コマンド ライン ツールを使用して、展開したアセンブリおよびそのアイテムを表示したり管理したりすることができます。 できますアーティファクトを管理するか個別にまたは、アプリケーション内でグループ化します。  
  
## <a name="deploying-an-assembly"></a>アセンブリを展開します。  
 次の方法で、アプリケーションにアセンブリを追加できます。  
  
- Visual Studio 環境内からアプリケーションにアセンブリを配置します。  
  
- BizTalk Server 管理コンソール内からアプリケーションに BizTalk Server アセンブリを手動で追加します。  
  
- コマンドラインからスクリプトを使用してアプリケーションに BizTalk アセンブリを追加します。  
  
- BizTalk Server 管理コンソール内から他のアプリケーションから BizTalk Server アセンブリに移動します。  
  
  アセンブリをアプリケーションに追加する方法の詳細については、次を参照してください。 [BizTalk アプリケーションに Visual Studio から BizTalk アセンブリを展開する](http://go.microsoft.com/fwlink/?LinkID=154719)(http://go.microsoft.com/fwlink/?LinkID=154719)します。  
  
## <a name="redeploying-assemblies"></a>アセンブリを再デプロイします。  
 開発し、BizTalk アセンブリのデバッグを処理中には、複数回再配置する必要があります。 BizTalk Server では、再デプロイする簡単なメカニズムを提供します。 バージョン番号を変更せずにアセンブリを展開する場合は、再デプロイのプロパティを使用できます。 BizTalk Server のすべてのアセンブリを再デプロイする手順が自動的に実行します。  
  
 アセンブリを再展開の詳細については、次を参照してください。 [Visual Studio から BizTalk アセンブリを再デプロイする方法](http://go.microsoft.com/fwlink/?LinkID=154720)(http://go.microsoft.com/fwlink/?LinkID=154720)します。  
  
### <a name="best-practices-for-redeploying-an-assembly"></a>アセンブリを再デプロイするためのベスト プラクティス  
 **新しいアセンブリを GAC にインストールする必要があります。**  
  
- アセンブリを再デプロイするときに、グローバル アセンブリ キャッシュ (GAC) に常にアセンブリの新しいバージョンをインストールする必要があります。 このインストールは、再展開の後に行えます。 詳細については、次を参照してください。[を GAC にアセンブリをインストールする方法](http://go.microsoft.com/fwlink/?LinkID=154828)(http://go.microsoft.com/fwlink/?LinkID=154828)します。  
  
  **常に再デプロイするソリューション レベルでの依存関係がある場合**  
  
- ソリューションに複数のアセンブリがあり、そのソリューションの 1 つ以上のアセンブリが再展開するアセンブリに依存している場合、ソリューション レベルで目的のアセンブリを再展開する必要があります。 プロジェクト レベルでアセンブリを再デプロイするときに BizTalk Server が停止、参加解除、バインド解除、およびこのアセンブリが依存しているまたはこのアセンブリに依存しているいずれかのすべてのアセンブリで、成果物を削除するためです。 BizTalk Server では、アイテムの展開、バインド、参加、開始を行う追加手順は実行されません。 ソリューション全体を再展開すると、依存関係に基づいているソリューションのすべてのアイテムを展開解除して再展開するのに必要な手順が、BizTalk Server によって自動的に実行されます。  
  
  **依存アセンブリを手動で再展開する必要があります。**  
  
- アセンブリが展開解除されますが、次の場合、展開、バインド、および対象のアセンブリを再展開した後、各依存アセンブリのアイテムを参加させる追加手順の実行が必要である場合に BizTalk Server が依存アセンブリに常に展開解除、アセンブリに依存します。  
  
   プロジェクト レベルでアセンブリを再展開する際に、同じソリューションの別のアセンブリが目的のアセンブリに依存している場合。  
  
   ソリューション レベルでアセンブリを再展開する際に、別のソリューションに依存アセンブリが存在する場合。  
  
  **ホスト インスタンスを再起動する必要があります。**  
  
- アセンブリ バージョン番号を変更せずにオーケストレーションを含むアセンブリを再展開すると、BizTalk 管理データベースの既存のアセンブリは上書きされます。 ただし、変更が有効になる前に、オーケストレーションがバインドされているホストの各ホスト インスタンスを再起動する必要があります。 オプションを指定して、アセンブリの再展開時に、ローカル コンピューター上のすべてのホスト インスタンスを自動的に再起動することができます。  
  
   アセンブリ バージョン番号を変更せずにオーケストレーションを含むアセンブリを再展開すると、BizTalk 管理データベースの既存のアセンブリは上書きされます。 ただし、変更が有効になる前に、オーケストレーションがバインドされているホストの各ホスト インスタンスを再起動する必要があります。 オプションを指定して、アセンブリの再展開時に、ローカル コンピューター上のすべてのホスト インスタンスを自動的に再起動することができます。 展開のプロパティの詳細については、次を参照してください。 [Visual Studio の配置プロパティを設定する方法](http://go.microsoft.com/fwlink/?LinkID=154718)(http://go.microsoft.com/fwlink/?LinkID=154718)します。  
  
   手動で停止し、各ホスト インスタンスを開始できます。 停止して、ホスト インスタンスの開始の詳細については、次を参照してください。[ホスト インスタンスを停止する方法](http://go.microsoft.com/fwlink/?LinkID=154829)(http://go.microsoft.com/fwlink/?LinkID=154829)と[ホスト インスタンスを開始する方法](http://go.microsoft.com/fwlink/?LinkID=154830)(http://go.microsoft.com/fwlink/?LinkID=154830)します。