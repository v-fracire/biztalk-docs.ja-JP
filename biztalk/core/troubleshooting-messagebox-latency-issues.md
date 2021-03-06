---
title: メッセージ ボックスの待機時間に関する問題のトラブルシューティング |Microsoft ドキュメント
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e9eb5789-80bd-40d4-8c27-7ae117fd9232
caps.latest.revision: 5
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 0e37fc970230bf218bcfd820611fb6b87322e535
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
ms.locfileid: "22279874"
---
# <a name="troubleshooting-messagebox-latency-issues"></a>メッセージ ボックスの遅延に関する問題のトラブルシューティング
理想の世界では、メッセージはいずれもメッセージ ボックス データベースに公開された時点で速やかに処理および配信され、メッセージ ボックス データベースのサイズが過剰に増加することはないかもしれません。 メッセージ ボックス内に参照されなくなったメッセージがあれば、メッセージ ボックス データベース テーブルを定期的にクリーンアップする SQL エージェント ジョブによってすぐに削除されます。  
  
 ところが現実の世界では、メッセージが予測可能な一定速度で届くことはまれで、SQL エージェント ジョブがメッセージ ボックス データベース テーブルをクリーンアップするには時間がかかります。  
  
 このため、シナリオによっては、メッセージ ボックスのサイズが急速に増加する可能性があります。  
  
 次の場合はメッセージ ボックスのサイズが過剰に肥大化し、処理全体の妨げとなる可能性があります。  
  
-   **「ホストの追跡を許可する」オプションを設定のある Biztalk ホスト インスタンスが停止している**です。 これは、メッセージ ボックス データベースから BizTalk 追跡データベース (BizTalkDTADb) への追跡データの移動を行うホストです。  
  
-   **SQL Server エージェントが実行されていない**これは、[後で、メッセージ ボックスに移動したデータを消去する]、BizTalkDTADb データベースにメッセージ ボックス データベースからデータを移動を行う SQL ジョブが実行されていない場合に発生することができます。 この問題を回避するため、SQL エージェント サービスを常に実行しておくことが非常に重要です。  
  
-   **SQL Server ジョブが無効になっている**なしの既定の SQL Server ジョブを無効にする命令型は、SQL Server エージェントが実行されている場合でもです。  
  
-   **BizTalkDTADb データベースのサイズが過剰**BizTalkDTADb データベースが非常に大きく、原因で時間がかかって BizTalkDTADb データベースに挿入する場合に発生します。 このような状態になると、TDDS (Tracking Data Delivery Service) によるデータの移動速度が低下し、メッセージ ボックス データベースにバックログが蓄積されるようになります。 この問題を回避するには、BizTalkDTADb データベースに対して SQL Server のアーカイブと削除のジョブを定期的に実行することが重要になります。  
  
-   **過剰なディスク I/O の待機時間**かどうか、メッセージ ボックス データベースにデータの着信レート、システムが処理できるよりも高速であり、BizTalkDTADb データベースにデータを移動バックログが蓄積されるメッセージ ボックス データベースにします。 バックログが増加し続けることは深刻な問題であり、システムのパフォーマンスが時間の経過に伴って低下します。 この問題を軽減する 1 つの方法は、時間の経過と共に発生するメッセージ バックログからシステムが確実に回復できるように、より高速なディスクの導入やハードウェアのアップグレードを行うことです。  
  
## <a name="plan-for-the-future"></a>将来の計画  
 上記のすべてのベスト プラクティスに従ったとしても、時間の経過と共に、BizTalkDTADb データベースに移動される追跡データの量は非常に大きくなります。 システムが最適なパフォーマンスを維持できるように、追跡データを定期的にアーカイブするデータベース メンテナンス プランを実装することが重要です。  
  
 BizTalkDTADb データベースに保持できる履歴データの量は、システムを経由してプッシュされるメッセージの量に応じて異なります。 高い負荷やスループットが発生しないシステムでは、このデータベースのサイズは比較的緩やかに増加するため、より多くの履歴データを BizTalkDTADb データベースに保持することができます。  
  
 実行時のパフォーマンスを損なわないように、BizTalkDTADb データベースに保持するデータは最小限にすることをお勧めします。