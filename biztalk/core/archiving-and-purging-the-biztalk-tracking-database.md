---
title: アーカイブし、追跡データベースの削除 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7014cf31-86e8-4829-8055-056442329009
caps.latest.revision: 37
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 3556618df02c7a8c9df5d0d55c27eb69ed91eae2
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "37000856"
---
# <a name="archive-and-purge-the-biztalkdtadb-database"></a>アーカイブおよび BizTalkDTADb データベースの消去

## <a name="overview"></a>概要
BizTalk Server ではシステム上のより多くのデータが処理されるため、BizTalk 追跡 (BizTalkDTADb) データベースのサイズは増え続けます。 サイズが増加してもチェックされないので、システム パフォーマンスが低下し、TDDS (Tracking Data Decode Service) でエラーが発生することがあります。 一般的な追跡データに加えて、追跡メッセージもメッセージ ボックス データベースに累積されます。これにより、ディスクのパフォーマンスが低下します。  
  
BizTalk Server では、DTA Purge and Archive ジョブを使用して両方のプロセスを自動化します。 BizTalk 追跡データベースからデータをアーカイブまたは削除することで、システムを正常な状態に保てるだけでなく、アーカイブされた追跡データを将来使用するために保持できます。 BizTalk 追跡データベースのアーカイブは、長期にわたって累積され、ディスク領域を消費するため、定期的にセカンダリ ストレージに移動することをお勧めします。  
  
 BizTalk 追跡データベースからデータを削除すると、DTA Purge and Archive ジョブにより、メッセージおよびサービス インスタンスの情報、オーケストレーション イベントの情報、ルール エンジンの追跡データなど、さまざまな種類の追跡情報が削除されます。  
  
 追跡データ レコードの経過期間は、追跡データが BizTalk 追跡データベースに挿入された時刻に基づきます。 DTA Purge and Archive ジョブでは、このタイム スタンプを使用して、そのレコードがデータの有効期間よりも古くなっていないかどうかが継続的にチェックされます。 有効期間が過ぎると、そのたびに BizTalk 追跡データベースがアーカイブされ、新しいアーカイブ ファイルが作成されます。 さらに、ジョブ スケジュールで指定された SQL Server エージェント ジョブの間隔ごとに、完了した追跡データのうち、有効期間を経過しているものがすべて削除されます。  
  
 BizTalk Server では、論理削除と物理削除の概念が使用されています。 論理削除は完了したインスタンスを削除する場合に使用し、物理削除は不完全なインスタンスを削除する場合にのみ使用します。  
  
## <a name="soft-purge"></a>論理削除 : 
  
 DTA Archive and Purge ジョブでは、LiveHours パラメーターと LiveDays パラメーターを加算した値が、BizTalk Server 環境で管理するデータの有効期間になります。 この有効期間を経過している完了したインスタンスに関連付けられているデータはすべて削除されます。 既定では、DTA Archive and Purge ジョブは有効になっていません。 まずはジョブを構成し、その後で有効にする必要があります。  
  
 たとえば、20 分ごとに実行する DTA Purge and Archive ジョブを構成し、設定した = 1、LiveDays = 0。 初めてこの SQL Server エージェント ジョブの実行 (T0) では、アーカイブの作成によって追跡データベースのバックアップが行わし、エントリは、このタイムスタンプを持つデータベースに保存されます。 追跡データを削除するためには正常なアーカイブが必要です。 アーカイブが正常に行われた場合は、完了後 1 時間を経過したインスタンスに関連付けられたすべてのデータが削除されます。 ジョブが実行されるたびに、1 時間を経過した完了済みのデータは削除されます。 3 回目の実行 (1 時間後) では、過去 1 時間のセグメントで追跡データベースに挿入されたすべてのインスタンスのデータを含む新しいアーカイブが作成されます。  
  
 アーカイブを構成する方法と、削除の例では、一致するように、DTA Purge and Archive ジョブのステップを次に示します。  
  
```  
exec dtasp_BackupAndPurgeTrackingDatabase  
1, --@nLiveHours 1,   
0, --@nLiveDays   
1, --@nHardDeleteDays   
‘\\server\backup’, --@nvcFolder   
null, --@nvcValidatingServer   
0 --@fForceBackup Soft purge process  
```  
  
 前回のバックアップのタイムスタンプが BizTalk 追跡データベースに格納されています。このタイムスタンプの値により、前のアーカイブに含まれている場合のみ、データが削除されます。 さらに高い信頼性を確保する手段として、アーカイブを約 10 分ずつ重複させる措置がとられます。 上記の例に基づいた論理削除プロセスを次に示します。 アーカイブ タスクと削除タスクは必ずしも同時に発生するわけではないことに注意してください。  
  
 **論理削除プロセス**  
  
 ![論理削除プロセス](../core/media/archivingandpurging.gif "archivingandpurging")  
  
## <a name="hard-purge"></a>物理削除
  
 論理削除では完了したインスタンスと関連付けられたデータのみが削除されるため、無期限に実行される多数のループ インスタンスがある場合は、追跡データベースのサイズが増大するばかりか、これらのインスタンスは一切削除されません。 物理削除の日付を使用すると、サービスの存在を示す情報を除き、指定された間隔よりも前のすべての情報を削除することが可能になります。 使用して、物理削除を設定する、 <strong>@nHardDeleteDays</strong> Archive and Purge でパラメーターは、DTA Archive and Purge ジョブでステップ インします。 物理削除の設定は、必ず論理削除の設定よりも大きい値にしてください。 つまり、 <strong>@nHardDeleteDays</strong>の合計より大きくなければなりません<strong>@nLiveHours</strong>と <strong>@nLiveDays</strong>します。  
  
 アーカイブおよび削除には、次の表に示す機能があります。  
  
|機能|説明|  
|-------------|-----------------|  
|物理削除|指定された日付よりも前の不完全なインスタンスの情報を削除するように、時間間隔を構成できます。|  
|追跡メッセージの追跡データベースへのコピー|CopyTrackedMessageToDTA オプションを使用すると、追跡メッセージをメッセージ ボックス サーバーから BizTalk 追跡データベースに直接コピーできます。 これは、DTA Purge and Archive ジョブを使用してデータを削除するために必要です。|  
|アーカイブの検証|必要に応じてサーバーを設定するセカンダリ データベースが作成されるときに、アーカイブを検証することができます。|  
|BizTalk 追跡データベースの複数のバージョンに対する追跡サポート|BizTalk Server で追跡を使用することをサポートできるようにデータベース アーカイブです。|  
|追跡データの削減|生成された追跡情報を減らさずに、格納された追跡データの量を大幅に削減します。 その結果、追跡データベースのサイズの増大速度が遅くなります。|  
|高速な追跡操作 (データベース スキーマの大幅な最適化)|大規模データベースのメッセージやサービス インスタンスを検索するために追跡タスクを使用できます。この機能は大幅に最適化されています。|  
  
> [!NOTE]
>  性能上の問題があり、BizTalk 追跡データベースを削除することで一時的に対処している場合、追跡情報を収集しないように BizTalk を構成するには、グローバル追跡を無効にすることを検討してください。 参照してください[グローバル追跡をオフに](../core/how-to-turn-off-global-tracking.md)します。  
  
## <a name="next-steps"></a>次のステップ
  
-   [チェックリスト: BizTalk 追跡データベースのアーカイブおよび削除](../core/checklist-archiving-and-purging-the-biztalk-tracking-database.md)  
  
-   [BizTalk 追跡データベースのデータをアーカイブおよび削除するために BTS_BACKUP_USERS ロールを構成する](../core/configure-bts_backup_users-role-to-archive-and-purge-from-tracking-database.md)  
  
-   [DTA Purge and Archive ジョブの構成](../core/how-to-configure-the-dta-purge-and-archive-job.md)  
  
-   [BizTalk 追跡データベースからデータを削除する](../core/how-to-purge-data-from-the-biztalk-tracking-database.md)  
  
-   [BizTalk 追跡データベースからデータを手動で削除する](../core/how-to-manually-purge-data-from-the-biztalk-tracking-database.md)  
  
-   [アーカイブの自動検証の有効化](../core/how-to-enable-automatic-archive-validation.md)  
  
-   [追跡メッセージを BizTalk 追跡データベースにコピーする](../core/how-to-copy-tracked-messages-into-the-biztalk-tracking-database.md)  
  
-   [アーカイブおよび削除のプロセスのパフォーマンスの向上](../core/improving-the-performance-of-the-archiving-and-purging-process.md)  
  
-   [グローバル追跡の無効化](../core/how-to-turn-off-global-tracking.md)