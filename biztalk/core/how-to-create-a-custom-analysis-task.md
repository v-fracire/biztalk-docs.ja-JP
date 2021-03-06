---
title: カスタム分析タスクを作成する方法 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- BAM, DTS tasks
- DTS tasks
- DTS packages, tasks
- BAM, processing
ms.assetid: 6046c113-fb58-4e72-8f48-5470e52be9a8
caps.latest.revision: 7
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: f8683e95373bbfa806cc9ac9ae27e90a661d006e
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36977587"
---
# <a name="how-to-create-a-custom-analysis-task"></a>カスタム分析タスクを作成する方法
BAM データを処理するためのカスタム DTS タスクを作成する最も簡単な方法は、BAM で自動生成されるパッケージを基に作成を開始して、すべてのデータ処理を必要に応じて置き換えることです。  
  
### <a name="to-create-a-custom-dts-task"></a>カスタム DTS タスクを作成するには  
  
1. OLAP キューブを必要とする BAM 定義を作成します。 たとえば、Excel のウィザードを使用し、1 つのピボットテーブル® レポートを RTA 以外のビューとして残します。  
  
2. BAM によって作成される、キューブ処理用の DTS パッケージを開きます。 BAM では、各ビューは、bam_an _ と呼ばれるこのような 1 つのパッケージを作成します。\<*ビュー名*\>します。  
  
3. DTS デザイナーでパッケージを開き、最初の 2 つのステップと最後のステップを除くすべてのステップを削除します。 また、プライマリ インポート データベースへの接続を保持することが必要な場合もあります。  
  
4. 最初の ActiveX® タスクのプロパティを編集します。 DTSGlobalVariables.Parent.Steps が含まれている行は削除済みのステップを参照しているので、すべて削除します。 スクリプトの先頭部分は次のとおりです。  
  
   ```  
   serverName = "<your server here>"   
   databaseName = "<your analysis database here>"  
   cubeName = "<your cube name here>"  
   ```  
  
   > [!NOTE]
   >  "データ分析開始" タスク (このパッケージの 2 番目のタスク) は非常に重要です。このタスクにより、パッケージに次の機能が提供されます。  
   > 
   > - 完了したアクティビティの増分処理用の移動ウィンドウ (bam_(BamView)_View(Activity)_CompletedInstancesWindow という名前の動的 SQL ビュー)  
   >   -   進行状況 - bam をという名前のテーブルに含まれるアクティビティのスナップショット\_(BamView) _View (Activity) _ActiveInstancesSnapshot します。  
  
5. データを挿入しない期間に短いトランザクションでビューとテーブルを取得します。これにより取得されるデータは、プライマリ インポート データベースの瞬間的なスナップショットを表します。 ビューやテーブルを基本の入力データとして実際のデータ変換を行う、1 つ以上のステップを実装します。 分析タスクの目的が OLAP キューブの設定以外の場合は、最後にジョブがコミットされたときのタイムスタンプを保持し、最初の ActiveX タスクを、このタイムスタンプをグローバル変数 "CompletedCubeLastProcessTime" に割り当てるコードに置き換えることを忘れないでください。 2 番目のタスクでは、この変数を使用して、データが不足していないこと、および DTS パッケージがクラッシュまたは再起動した場合にデータ処理が 2 回行われていないことを確認します。  
  
6. 最後に、"データ分析終了" という最終的なタスクを呼び出す必要があります。 このタスクは、処理済みの完了したアクティビティを解放します。これにより、オンライン時間帯以外のときに、そのアクティビティをプライマリ インポートからアーカイブおよび削除することができます。  
  
## <a name="see-also"></a>参照  
 [ビジネス アクティビティの使用の監視](../core/using-business-activity-monitoring.md)