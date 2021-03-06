---
title: インデックスを作成する方法 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Create-Index command [BAM]
- indexes [BAM], creating
- indexes [BAM], aggregations
- creating, indexes [BAM]
- aggregations [BAM], indexes
ms.assetid: 456d94e6-2e84-4d12-ad38-49f9eeb103f3
caps.latest.revision: 19
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: b15fd07049ee31162b2ed69f38a99d26100e08c4
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36989699"
---
# <a name="how-to-create-an-index"></a>インデックスを作成する方法
管理者を使用して、**インデックスの作成**コマンドを特定のチェックポイントで指定したアクティビティにインデックスを作成します。  
  
### <a name="to-create-an-index-on-an-activity"></a>アクティビティにインデックスを作成するには  
  
1. コマンド プロンプトから次のディレクトリを参照:[!INCLUDE[btsBiztalkServerPath](../includes/btsbiztalkserverpath-md.md)]追跡します。  
  
2. 型**bm インデックスの作成-indexname:\<インデックス名\>-アクティビティ:\<アクティビティ名\>-チェックポイント:\<チェックポイント 1\>** します。  
  
   > [!NOTE]
   >  ユーザー アカウント制御 (UAC) をサポートするシステムでは、管理者特権を使用してこのツールを実行することが必要な場合があります。  
  
3. **Enter**キーを押します。  
  
## <a name="see-also"></a>参照  
 [BAM 動的インフラストラクチャの管理](../core/managing-the-bam-dynamic-infrastructure.md)   
 [BAM 管理ユーティリティ](../core/bam-management-utility.md)   
 [インデックスを削除する方法](../core/how-to-delete-an-index.md)   
 [集計のインデックスの一覧を取得する方法](../core/how-to-get-a-list-of-indexes-on-an-aggregation.md)