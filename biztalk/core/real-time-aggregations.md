---
title: "リアルタイム集計 |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- BAM, aggregations
- aggregations [BAM], real-time data
ms.assetid: 0ef44641-e067-4108-b318-f4373ca8fa8f
caps.latest.revision: "9"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: c1bc335c1c53fe106c460b7dcb5a27b803db97b1
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="real-time-aggregations"></a>リアルタイム集計
多次元集計の特定のスライスでは、時間が重要な要素になる場合があります。このような場合には、スライスをリアルタイムで使用することが必要になります。 たとえば、生鮮食料品を販売する業者では、配送の各段階での製品数量の集計をリアルタイムで利用できるようにする必要があります。 同時に、代表的な顧客の年齢などの他の集計を、ビジネス インテリジェンス分析のために月末にのみ実行する必要がある場合もあります。  
  
 BAM には、アクティビティ ストレージ テーブルからのトリガーによって維持されるテーブルとして、リアルタイム集計 (RTA) が実装されています。 注文書 (PO) を処理する場合、RTA ビューは次の図の例のようになります。  
  
 ![](../core/media/bam-realtime-aggregations.gif "bam_realtime_aggregations")  
BAM リアルタイム集計  
  
 この図では、Redmond から 100 ドルの新しい PO を受け取ると、`Count=Count+1` や `Amount=Amount+$100` などの演算が行われ、対応する {Redmond, InProcess} 行のセルに金額が加算されます。  
  
 その後、その注文が出荷されると、金額が行 {Redmond, InProcess} から削除され、行 {Redmond, Shipped} に加算されます。  
  
 BAM は特定のオンライン時間帯のデータを RTA 内に維持してから、削除します。 テーブルの対応する行を変更することで、オンライン時間帯を構成することができます**bam_Metadata_RealTimeAggregations**です。  
  
 リアルタイム集計では、次のような状況が発生します。  
  
-   リアルタイム集計は、BAM のデータ書き込み速度に大きく影響します。 したがって、集計構造の中で重要なスライスのみを RTA として定義してください。  
  
-   リアルタイム集計のディメンション レベルの制限は 14 です。 たとえば、州と都市のデータ ディメンションの場所を作成する場合 (State と City) の 2 つのレベルとしてカウントされます。 進捗ディメンションのレベル数は、ツリーの深さで数えます。時間ディメンションのレベル数は、サブユニットの総数で数えます。 たとえば、年、月、日の時間ディメンションで時間としてカウントされます 4 つのレベルです。  
  
-   BAM は型のリアルタイムの集計をサポートしていません**Min**と**Max**です。 BAM では、集計が**カウント**、**合計**、および**平均**です。  
  
-   RTA のデータは特定のビジネス マイルストーンではなく、サーバーのタイム スタンプに従って古くなります。そのため、常に RTA の時間ディメンションを作成し、すべてのデータ スライスでそのディメンションを使用する必要があります。  
  
-   同じ BAM アクティビティを使用する RTA を複数定義しないでください。 そのような RTA を複数定義した場合、BAM データをアーカイブしたときに RTA データが不正確になります。  
  
 リアルタイム集計は、BAM のデータ書き込み速度に大きく影響します。 したがって、集計構造の中で重要なスライスのみを RTA として定義してください。  
  
 リアルタイム集計のディメンション レベルの制限は 14 です。 たとえば、州と都市のデータ ディメンションの場所を作成する場合 (State と City) の 2 つのレベルとしてカウントされます。 進捗ディメンションのレベル数は、ツリーの深さで数えます。時間ディメンションのレベル数は、サブユニットの総数で数えます。 たとえば、年、月、日の時間ディメンションで時間としてカウントされます 4 つのレベルです。  
  
 BAM は型のリアルタイムの集計をサポートしていません**Min**と**Max**です。 BAM では、集計が**カウント**、**合計**、および**平均**です。  
  
 同じ BAM アクティビティを使用する RTA を複数定義しないでください。 そのような RTA を複数定義した場合、BAM データをアーカイブしたときに RTA データが不正確になります。  
  
## <a name="see-also"></a>参照  
 [集計とは何ですか。](../core/what-is-an-aggregation.md)