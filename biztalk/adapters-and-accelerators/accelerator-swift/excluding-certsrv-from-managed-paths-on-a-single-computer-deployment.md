---
title: 1 台のコンピューター展開上のパスを管理から CertSrv を除外する |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- managed paths
- certificate server (CertSrv)
- certificates, certificate server (CertSrv)
ms.assetid: 39916663-b80e-49d8-ba9b-49276eb564fc
caps.latest.revision: 3
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 1651131369ef4a8e0c4683b82f5b97163e33382f
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36987843"
---
# <a name="excluding-certsrv-from-managed-paths-on-a-single-computer-deployment"></a>1 台のコンピューターの展開の管理パスから CertSrv を除外します。
デプロイした場合[!INCLUDE[btaA4SWIFT2.3abbrevnonumber](../../includes/btaa4swift2-3abbrevnonumber-md.md)]1 台のコンピューターに証明書サーバーをインストールすることも、同じコンピューターにする必要がある証明書サーバー (/certsrv を指定します) を除外する Microsoft SharePoint Server のサーバーの全体管理の管理パスから。  
  
### <a name="to-exclude-certsrv-from-the-managed-paths"></a>管理パスから CertSrv を除外するには  
  
1.  をクリックして**開始**、 をポイント**すべてのプログラム**、 をポイント**管理ツール**、順にクリックします**SharePoint Central Administration**。  
  
2.  サーバーの全体管理] ウィンドウで、**仮想サーバーの構成**セクションで、[**仮想サーバー設定を構成**します。  
  
3.  仮想サーバーの一覧] ウィンドウで、[**既定の Web サイト**します。  
  
4.  仮想サーバーの設定] ウィンドウで、**仮想サーバーの管理**セクションで、[**管理パスの定義**します。  
  
5.  管理パスの定義 ウィンドウで、**新しいパスを追加**セクションに、入力**CertSrv**で、**パス**テキスト ボックス。 **型**セクションで、**エクスクルード パス**します。 **[OK]** をクリックします。  
  
6.  管理パスの定義ウィンドウを閉じます。