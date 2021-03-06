---
title: アラートの頻度を変更する方法を評価 |Microsoft ドキュメント
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 68f326ed-2017-4853-89b9-146cb0785554
caps.latest.revision: 12
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 6f921699e9a98724c8ca2c36f99d7eb9b9848875
ms.sourcegitcommit: 5abd0ed3f9e4858ffaaec5481bfa8878595e95f7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2017
ms.locfileid: "25969072"
---
# <a name="how-to-change-the-frequency-with-which-alerts-are-evaluated"></a>警告を評価する頻度を変更する方法
SQL Notification Services ジェネレーターを既定の設定で展開すると、BAM イベント プロバイダーで発生するイベントに対してタイムリーに対応できない場合があります。 Notification Services の adf.xml ファイルを変更することで、警告のイベントを評価する頻度 (クォンタム期間) を上げることができます。  
  
## <a name="prerequisites"></a>前提条件  
 ここで示す手順を実行するには、プライマリ インポート データベースの読み取りと書き込みのアクセス許可を持つ [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] グループ、一般には [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] Administrators グループのメンバーとしてログオンする必要があります。  
  
### <a name="to-modify-the-notification-services-generator-quantum-duration"></a>Notification Services ジェネレーターのクォンタム期間を変更するには  
  
1.  Notification Services コマンド プロンプトを開きます。 をクリックして**開始**、 をクリックして**すべてのプログラム**、 をクリックして**Microsoft SQL Server 2005**をクリックして**構成ツール**をクリックして**Notification Services コマンド プロンプト**です。  
  
2.  Notification Services 構成ファイルを取得します。 コマンド プロンプトで次のように入力します。: **cscript ProcessBamNSFiles.vbs--get config.xml adf.xml \<PimaryImport データベース サーバー\> \< PimaryImport データベース名\>** です。  
  
3.  変更または追加、 \<QuantumDuration\>要素の下、 \<ApplicationExecutionSettings\>内のノード、adf.xml ファイル。 QuantumDuration 要素の詳細については、次を参照してください。 [http://go.microsoft.com/fwlink/?LinkId=78803](http://go.microsoft.com/fwlink/?LinkId=78803)です。  
  
4.  コマンド プロンプトで次のように入力します。: **cscript ProcessBamNSFiles.vbs-更新 config.xml adf.xml \<PimaryImport データベース サーバー\> \< PimaryImport データベース名\>です。**  
  
## <a name="see-also"></a>参照  
 [Notification Services 構成ファイル用の BAM コマンド ライン スクリプト](../core/bam-command-line-script-for-notification-services-configuration-files.md)