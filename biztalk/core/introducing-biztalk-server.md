---
title: "BizTalk Server の紹介 |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 06a4a31a-eefe-4b1b-89ca-2cba2b6fa587
caps.latest.revision: "17"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 544522fd2761cf12702ce517116bfaac84830084
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="introducing-biztalk-server"></a>BizTalk Server の紹介
どのようなアプリケーションであっても、孤立したものはありません。 かどうか好むと好まざる、システムを一緒に結び付けることが標準になりました。 しかし、ソフトウェアを接続するには、単なるバイト変換以上の作業が必要です。 組織がサービス志向に向かうにつれ、効率的なビジネス プロセスを作成して別々のシステムを一体化するという目標は、現実的になりつつあります。  
  
 Microsoft [!INCLUDE[btsBizTalkServer2006r3](../includes/btsbiztalkserver2006r3-md.md)] は、この目標をサポートします。 この最新リリースの BizTalk Server では、これまでのバージョンと同様に、多様なソフトウェアを接続でき、それらのソフトウェアを使用するプロセス ロジックをグラフィカルに作成および変更できます。 また、インフォメーション ワーカーは [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] を使用して、実行中のプロセスを監視したり、取引先と連携したり、他のビジネス指向のタスクを実行したりできます。  
  
 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] の主要な新機能は次のとおりです。  
  
-   アプリケーションの展開、監視、および管理をより強力にサポート  
  
-   インストールの大幅な簡略化  
  
-   ビジネス アクティビティ監視 (BAM) 機能の向上  
  
 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] では、他の Microsoft テクノロジの最新リリースも使用されています。 たとえば、.NET Framework 3.5 に基づいて構築され、開発ツールは Microsoft [!INCLUDE[vs2010](../includes/vs2010-md.md)] によりホストされます。 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] のストレージには、Microsoft の主要データベース製品の最新版である [!INCLUDE[btsSQLServer2008R2](../includes/btssqlserver2008r2-md.md)] を使用できます。 さらに、[!INCLUDE[btsBizTalkServer2006r3](../includes/btsbiztalkserver2006r3-md.md)] は 64 ビット版 Windows Server 上でも実行でき、大容量のメモリを活用できる以外に、新世代のハードウェアで提供されるさまざまなメリットを得られます。  
  
## <a name="what-is-biztalk-server"></a>BizTalk Server とは何ですか。  
 異なるシステムを効率的なビジネス プロセスへと統合するには、多くの難題が伴います。 そのために、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] にはさまざまなテクノロジが用意されています。 この製品の主要なコンポーネントを次に示します。  
  
 ![BizTalk Server コンポーネントの概要](../core/media/d167608e-7c51-4d52-b8fa-9d4149242934.gif "d167608e-7c51-4d52-b8fa-9d4149242934")  
  
 図に示すように、製品の中核部分は [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] エンジンです。 このエンジンの主要部分は次の 2 つに分かれています。  
  
-   その他のソフトウェアの範囲と通信する機能を提供するメッセージング コンポーネント。 このエンジンでは多様な通信アダプターによって、各種のプロトコルやデータ形式がサポートされています。これには、Web サービスやその他の多くのサービスが含まれます。  
  
-   グラフィカルに定義されたプロセス (オーケストレーション) を作成および実行するためのサポート機能。 エンジンのメッセージング コンポーネントの最上部に構築されるオーケストレーションには、ビジネス プロセスの全部または一部を実行するロジックが実装されます。  
  
 他にも、このエンジンと連動して、次のような BizTalk コンポーネントが用意されています。  
  
-   ビジネス ルール エンジン。複雑なルールのセットを評価するときに使用できます。  
  
-   グループ ハブ。開発者と管理者が、エンジンとその実行オーケストレーションを監視および管理するときに使用できます。  
  
-   エンタープライズ シングル サインオン (SSO) ユーティリティ。Windows システムと Windows 以外のシステムとの間で認証情報をマップするための機能が提供されます。  
  
 この基礎の上に、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] では、ビジネス アクティビティの監視機能が組み込まれています。インフォメーション ワーカーはこの機能を使用して、実行中のビジネス プロセスを監視できます。 画面には技術情報ではなくビジネス情報が表示されます。ビジネス ユーザーは、表示する情報を指定できます。  
  
## <a name="biztalk-server-and-the-challenge-of-connecting-diverse-systems"></a>BizTalk Server と、多様なシステムを接続する場合の課題  
 現代のビジネス プロセスのほとんどは、多かれ少なかれ、ソフトウェアを使用しています。 これらのプロセスには、1 つのアプリケーションを利用するだけのものもあれば、さまざまなソフトウェア システムに完全に依存しているものもあります。 多くの場合、使用されるソフトウェアは、異なる時期に、異なるプラットフォームを対象として、異なるテクノロジを基に作成されたものです。 このようなビジネス プロセスを自動化するには、さまざまなシステムを接続する必要があります。  
  
 この課題への対応は、ビジネス プロセス オートメーション (BPA)、ビジネス プロセス管理 (BPM) など、さまざまな名称で呼ばれています。 しかし名称とは関係なく、アプリケーションの統合には 2 つのシナリオを考えることが重要です。 1 つ目は、1 つの組織内でのアプリケーションの接続です。これは通常、エンタープライズ アプリケーション統合 (EAI) と呼ばれます。 2 つ目は、異なる組織間でのアプリケーションの接続です。これは、企業間 (B2B) 統合と呼ばれます。  
  
 下の図は、EAI 問題に対して適用される、中核となる BizTalk Server エンジンの単純な例です。 このシナリオでは、IBM メインフレームで実行されている在庫アプリケーションによって、商品の在庫が少ないことが検出され、その商品の追加注文要求が発行されます。 この要求は BizTalk Server オーケストレーションに送信され (ステップ 1)、オーケストレーションから組織の ERP アプリケーションに注文書の要求が発行されます (ステップ 2)。 Unix システムで実行される可能性があります、ERP アプリケーションから要求された PO (手順 3)、および BizTalk Server オーケストレーションが返送し、調達、おそらくに基づいて構築されたアプリケーション アイテムを注文する必要がありますを .NET Framework を使用して Windows (ステップ 4) に通知.  
  
 ![BizTalk エンジンに実装された EAI です。] (../core/media/7d8558da-03cf-494b-8334-efe0ea15a6a7.gif "7d8558da-03cf-494b-8334-efe0ea15a6a7")  
  
 この例では、各アプリケーションが、別のプロトコルを使用して通信を行います。 したがって、BizTalk Server エンジンのメッセージング コンポーネントでは、ネイティブな通信形式で各アプリケーションと対話できる必要があります。 また、完全なビジネス プロセスを認識する単体のアプリケーションは存在しません。 プロセスにかかわるソフトウェア間で調整を行う機能は、BizTalk Server オーケストレーションに実装されています。  
  
 組織内のアプリケーションを接続することは重要ですが、複数の組織にわたるアプリケーションを接続することには、さらに高い価値があります。 下の図は、このような企業間統合の簡単な例です。 この場合、図の最上部にある購入組織では、2 つの業者組織と対話する BizTalk Server オーケストレーションが実行されます。 また、業者 A も BizTalk Server を使用して、サプライ アプリケーションへの間接アクセスを提供しています。 業者 B は、別のベンダ製の統合プラットフォームを使用して、Web サービスなどから購入組織の BizTalk Server オーケストレーションに接続しています。  
  
 ![ビジネス &#45; へ (& a) #45; business の統合図](../core/media/b1d8787d-e842-468e-96c5-b68875d9abc3.gif "b1d8787d-e842-468e-96c5-b68875d9abc3")  
  
## <a name="see-also"></a>参照  
 [Understanding BizTalk Server](../core/understanding-biztalk-server.md)