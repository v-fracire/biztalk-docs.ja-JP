---
title: 追加の BAM プライマリ インポート データベースを参照する方法 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ea80b32c-f2cb-4aca-89f4-d5b72e1ba021
caps.latest.revision: 13
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 54982491ca8ce2c7ca7acd9e176a7341b2642c78
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36992315"
---
# <a name="how-to-reference-additional-bam-primary-import-databases"></a>追加の BAM プライマリ インポート データベースを参照する方法
管理者を使用して、**参照を有効にする**コマンドを追加の BAM プライマリ インポート データベースを参照します。 分散 BAM アクティビティの表示を容易にするには、複数の BAM プライマリ インポート データベースを参照します。  
  
### <a name="to-enable-a-reference-to-an-additional-bam-primary-import-database"></a>追加の BAM プライマリ インポート データベースへの参照を有効にするには  
  
1. 次のように、コマンド プロンプトを開きます: をクリックして**開始**、 をクリックして**実行**、型**cmd**、順にクリックします**OK**。  
  
2. [!INCLUDE[btsBiztalkServerPath](../includes/btsbiztalkserverpath-md.md)]Tracking に移動します。  
  
3. コマンド ライン プロンプトで、次の入力: **bm 参照を有効にする TargetServer:\<ターゲット サーバー\> - TargetDatabase:\<ターゲット データベース\>** ここで、 \<*ターゲット サーバー* \>によって指定されるターゲットの BAM プライマリ インポート データベースを SQL server の名前は置き換え\<ターゲット データベース\>が存在します。 Enter キーを押します。  
  
## <a name="see-also"></a>参照  
 [BAM 管理ユーティリティ](../core/bam-management-utility.md)