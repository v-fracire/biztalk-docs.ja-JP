---
title: BAM プライマリ インポート データベースへの参照を無効にする方法 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 78d2d644-6ebb-4051-ae59-af7d0fb75753
caps.latest.revision: 16
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 5b89e9df78d91a6e4737b964223f81983e74dd29
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36998195"
---
# <a name="how-to-disable-a-bam-primary-import-database-reference"></a>BAM プライマリ インポート データベースへの参照を無効にする方法 
管理者を使用して、**無効にする参照**指定された BAM プライマリ インポート データベースへの参照を無効にするコマンド。  
  
### <a name="to-disable-a-reference-to-a-bam-primary-import-database"></a>BAM プライマリ インポート データベースへの参照を無効にするには  
  
1. 次のように、コマンド プロンプトを開きます: をクリックして**開始**、 をクリックして**実行**、型**cmd**、順にクリックします**OK**。  
  
2. [!INCLUDE[btsBiztalkServerPath](../includes/btsbiztalkserverpath-md.md)]Tracking に移動します。  
  
3. コマンド ライン プロンプトで、次の入力: **bm 無効にする参照 TargetServer:\<ターゲット サーバー\> - TargetDatabase:\<ターゲット データベース\>[-サーバー:\<server\> ][-データベース:\<データベース\>]** ここで、 **\<**<em>ターゲット サーバー</em> **\>** によって指定されるターゲットの BAM プライマリ インポート データベースを SQL server の名前は置き換え\<*ターゲット データベース*\>が存在します。 **Enter**キーを押します。  
  
## <a name="see-also"></a>参照  
 [BAM 管理ユーティリティ](../core/bam-management-utility.md)