---
title: ボトルネックを回避するためのベスト プラクティス |Microsoft ドキュメント
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 81da2e31-dce0-43fb-841f-e65ff99e80a7
caps.latest.revision: 6
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 08f2291d6aa4d16c251a110bc6f94c6288dc5064
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
ms.locfileid: "22299666"
---
# <a name="best-practices-for-avoiding-bottlenecks"></a>ボトルネックを回避するためのベスト プラクティス
[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] の既定の設定は、多くのハードウェアやソフトウェアの構成に最適なパフォーマンスを提供しますが、シナリオによっては、設定や展開構成を変更すると効果的な場合があります。 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] を構成するときは、次のパフォーマンス ガイドラインを考慮してください。  
  
-   リソースの競合を防ぐためには、受信、オーケストレーション、および個別のホスト上の送信を分離します。 競合をさらに最小限に抑えるには、追跡サービスを他のホストから分離します。  
  
-   BizTalk Server を実行しているコンピューターの CPU 処理がボトルネックである場合は、cpu を追加または高速な Cpu へのアップグレードによって BizTalk Server を実行しているコンピューターをスケールします。  
  
## <a name="sql-server-guidelines"></a>SQL Server のガイドライン  
 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] で Microsoft SQL Server を構成するときは、次のパフォーマンス ガイドラインを考慮してください。  
  
-   可能であれば、高速なディスク サブシステムを SQL Server で使用するようにします。 独立したディスク型 10 の冗長アレイを使用して (RAID10/0 + 1) またはバックアップの電源装置と記憶域エリア ネットワーク (SAN)。  
  
-   BizTalk 追跡データベース (BizTalkDTADb) から別のサーバー上の各メッセージ ボックス データベースを分離します。 小規模な展開の CPU リソースがある場合があります、BizTalk 追跡データベースから別の物理ディスク上のメッセージ ボックス データベースを分離するための十分です。  
  
-   プライマリ メッセージ ボックス データベースは、CPU プロセッサの飽和やディスク操作 (ディスクの平均キュー長さ) からの待機時間によりボトルネックになる可能性があります。 CPU の処理がボトルネックである場合は、プライマリ メッセージ ボックスに CPU プロセッサを追加します。 それ以外の場合は、マスター メッセージ ボックス データベースでパブリッシングを無効にしてください。 こうすると、マスター メッセージ ボックス データベースより効率的に処理、他のメッセージ ボックス データベースにメッセージをルーティングできます。 パブリッシングを無効にするオプションは、複数のメッセージ ボックス データベースを使用している場合に有効です。  
  
-   ディスク操作がボトルネックとなっている場合は、BizTalk 追跡データベースを専用の SQL Server コンピューターまたは専用のディスクに移動します。 プライマリ メッセージ ボックス データベースでの CPU 処理もディスク操作がボトルネックでない場合は、既存のハードウェアを活用する同じ SQL Server コンピューターに新しいメッセージ ボックス データベースを作成できます。  
  
-   推奨事項に従って[、Databases2 のファイル グループを最適化する](../technical-guides/optimizing-filegroups-for-the-databases2.md)個別の物理ディスク上にデータベースのメッセージ ボックス データベースと BizTalk 追跡データベースのファイルには、トランザクションとデータ ログを分離します。  
  
-   データとログ ファイルには、十分な記憶域を割り当てます。 それ以外の場合 SQL Server では、すべてのログ ファイルが保存されているディスクの空き領域の消費は自動的にします。 ログ ファイルの初期サイズは、自分のシナリオで特定の要件によって異なります。 テスト結果に基づいて展開の平均ファイル サイズを見積もり、ソリューションの実装前に記憶域を拡張します。  
  
-   メッセージ ボックス、正常性と動作状況の追跡 (HAT)、およびビジネス アクティビティ監視 (BAM) などのディスクの使用率が高いデータベースに十分な記憶域を割り当てます。 ソリューションで BizTalk Framework メッセージング プロトコルを使用する場合は、BizTalk 構成データベース (BizTalkMgmtDb) に十分な記憶域を割り当てます。  
  
-   ビジネスによって必要があるなどデータの保有期間、および、シナリオで処理されたデータの量構成「DTA のアーカイブと削除」SQL Server エージェント ジョブ、HAT 追跡データベース、BizTalk 追跡データベースが大きくなりすぎないようにします。 データ挿入率の制限は、データベースのすべての容量に到達するため、このデータベースの容量増加でパフォーマンスが低下することができます。 これは、1 つの BizTalk 追跡データベースには、複数のメッセージ ボックス データベースがサポートされている場合に特に当てはまります。  
  
-   スケール アップ、ボトルネックを調査している場合、メッセージ ボックス データベースと BizTalk 追跡データベースをホストするサーバー。 Cpu の追加、メモリを追加する、高速の Cpu にアップグレードする、高速な専用ディスクを使用して、ハードウェアをスケール アップすることができます。  
  
-   複数のファイルへの TempDB ファイルの分割と、I/O 操作に関連するパフォーマンスの問題を解決する可能性があります。 一般的なガイドラインとして、プロセッサごとの 1 つのファイル データ ファイルを作成し、作成されたすべてのファイルは同じサイズを使用します。  
  
-   変更、データベース自動拡張 100 150 MB などの固定値に設定します。 既定では、データベース サイズの増加が 10% に構成されているが生じる可能性が遅延する大規模なデータベースを拡張するとき。  
  
-   SQL Server のメモリは、Min Server Memory および Max Server Memory の両方を同じ値に設定して、固定値に設定する必要があります。 一般に、SQL Server に物理メモリの 75% を割り当てるし、オペレーティング システムとアプリケーションの残りの部分の 25% のままにします。 専用の SQL Server の場合は、1 GB のオペレーティング システムを最小限に抑えるのために予約された量を減らすことができます。  
  
## <a name="see-also"></a>参照  
 [検索して、ボトルネックを解消します。](../technical-guides/finding-and-eliminating-bottlenecks.md)