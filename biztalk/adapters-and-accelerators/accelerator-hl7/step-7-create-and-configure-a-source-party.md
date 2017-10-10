---
title: "手順 7: を作成し、送信元パーティの構成 |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d8788a9c-ae6f-461b-82e5-f4276d1d5e0c
caps.latest.revision: "7"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 32539b1c352ac1fd2b60d2acd4c5ee975e2c3d18
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="step-7-create-and-configure-a-source-party"></a>手順 7: を作成し、送信元パーティを構成します。
このステップでは、送信元パーティを構成して、送信メッセージのメッセージ ヘッダーの変換を有効にする送信ポートを割り当てるを作成します。  
  
### <a name="to-create-and-configure-a-source-party"></a>作成および送信元パーティの構成  
  
1.  BizTalk 管理コンソールで、右クリック**パーティ**、 をポイント**新規**、クリックして**パーティ**です。  
  
2.  **パーティ プロパティ**ダイアログ ボックスの [名前] フィールドの種類で**Tutorial_BatchSource**です。  
  
    > [!NOTE]
    >  このボックスに入力した値は、元の FHS3.1 から[!INCLUDE[btaBTAHL71.3abbrevnonumber](../../includes/btabtahl71-3abbrevnonumber-md.md)]FragmentedInboundBatch.txt、バッチ処理されたメッセージ。  
  
3.  コンソール ツリーでクリックして**送信ポート**です。  
  
4.  送信ポート ペインの 名前 フィールドの選択**Tutorial_2wayAck**です。  
  
5.  **[OK]**をクリックします。  
  
6.  をクリックして**開始**、 をポイント**すべてのプログラム**、 をポイント**Microsoft BizTalk\<バージョン > Accelerator 用 HL7**、クリックして**BTAHL7構成のエクスプ ローラー**です。  
  
7.  BTAHL7 構成エクスプ ローラーで、上、**パーティ** タブで、をクリックして**Tutorial_BatchSource**です。  
  
8.  選択、**バッチ定義**BTAHL7 構成エクスプ ローラーのタブ。 選択**[はい]**の**断片化のために必要な**、順にクリック**保存**です。  
  
9. 選択、**受信確認**タブです。**受信確認の種類** **OriginalMode**、順にクリック**保存**です。  
  
 進みます[手順 8: BizTalk Server を再起動して](../../adapters-and-accelerators/accelerator-hl7/step-8-restart-biztalk-server.md)です。