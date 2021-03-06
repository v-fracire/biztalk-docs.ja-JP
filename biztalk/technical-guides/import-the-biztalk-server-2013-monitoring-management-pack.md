---
title: BizTalk Server 2013 Monitoring 管理パックのインポート |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: bee2bfe9-4eb0-46d4-8eee-75182202080c
caps.latest.revision: 7
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 7756a6ca4301f7536a0e4964117f11cb92eb2fcd
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36993787"
---
# <a name="import-the-biztalk-server-2013-monitoring-management-pack"></a>BizTalk Server 2013 Monitoring 管理パックをインポートします。
管理パックをインポートする方法についてで管理パックをインポートする方法を参照してください。 [Operations Manager 2007 R2 または 2012](http://go.microsoft.com/fwlink/?LinkId=142351) (<http://go.microsoft.com/fwlink/?LinkId=142351>)。 後に、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]管理パックのインポートは、次の手順を実行して初期構成を完了します。  
  
### <a name="to-configure-the-management-pack"></a>管理パックを構成するには  
  
1.  新しい管理パック作成上書きやその他のカスタマイズを格納します。  
  
2.  エージェント プロキシ設定を有効にするには、これらの手順に従います。  
  
    1.  オペレーション コンソールを開くし、[管理] ボタンをクリックします。  
  
    2.  管理者 ウィンドウで次のようにクリックします。**エージェントで管理**します。  
  
    3.  一覧内のエージェントをダブルクリックします。  
  
    4.  [セキュリティ] タブで、次のように選択します。**このエージェントをプロキシとして動作させ、他のコンピューター上の管理オブジェクトを検出できるようにする**します。  
  
    5.  BizTalk Server にインストールされている各エージェントには、手順 3 ~ 4 を繰り返します。