---
title: SSO 展開の概要 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SSO, deploying example
- SSO, deploying
- deploying, SSO
- SSO, multiple computers
- examples, deploying
ms.assetid: 6eccee26-c392-41fe-97fb-3afe1685540f
caps.latest.revision: 8
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: c98a12c11ae735945f4e69631e7211c05c0b9186
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "37022368"
---
# <a name="sso-deployment-overview"></a>SSO 展開の概要
この例では、システムは次のコンピュータを含む 3 つのドメインに展開されています。  
  
 **ドメイン ORCH.com**  
  
- ORCH ドメイン コントローラ  
  
- HIS1、HISSO サーバー  
  
- HIS2、マスタ シークレット サーバー  
  
- HIS3、管理データベース  
  
  **ドメイン SQL.com**  
  
- SQL ドメイン コントローラ  
  
- SQL2、SSO データベース  
  
  **ドメイン HIS.com**  
  
- HIS ドメイン コントローラ  
  
- HIS4 データベース  
  
  この展開の定義について重要な点は次のとおりです。  
  
- ドメイン ORCH.com とドメイン SQL.com には、双方向の信頼関係があり、どちらの方向を使用するかを選択できます。  
  
- ドメイン ORCH.com は、[!INCLUDE[btsWinSvr2k8](../includes/btswinsvr2k8-md.md)] または [!INCLUDE[btsWinSvr2k8R2](../includes/btswinsvr2k8r2-md.md)] のネイティブの機能レベルとして構成されています。  
  
- すべての SSO サービスは、ORCH.com のドメイン ユーザー アカウント (Orch\SSOSvcUser) で実行されています。 ユーザーは、SQL.com ドメイン内の SQL2 コンピュータに対するアクセス許可を持つように構成されています。 ユーザーは、ORCH.com ドメイン内のプロトコル遷移および制約付き委任用に構成されています。  
  
- ORCH.com のもう 1 つのドメイン ユーザー (Orch\TestAppUser) は、テスト プログラムの実行用に設定されています。 このユーザーも、プロトコル遷移および制約付き委任用に構成されています。  
  
## <a name="see-also"></a>参照  
 [展開プロセス](../core/deployment-process.md)