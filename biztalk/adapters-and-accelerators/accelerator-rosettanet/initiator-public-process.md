---
title: 開始側パブリック プロセス |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- public processes, initiator
- CIDX, 0A1 messages
- messages, 0A1 messages
- messages, message flow
- messages, public processes
- 0A1 messages
- public processes, message flow
ms.assetid: 371d0792-d346-405b-a8f4-2dfa64dd1566
caps.latest.revision: 4
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 5fa1cd2fc73e37590e25fb381f509c2ad74cd9e8
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36968443"
---
# <a name="initiator-public-process"></a>開始側パブリック プロセス
このプロセスは、開始 RNIF ビジネス メッセージを作成して送信することにより、開始側システムで RNIF (RosettaNet Implementation Framework) メッセージングを開始します。  
  
## <a name="message-flow-in-the-initiator-public-process"></a>開始側パブリック プロセスのメッセージ フロー  
 開始側パブリック プロセスのメッセージ フローは次のとおりです。  
  
1. 開始側パブリック プロセスは、サービス コンテンツ ポートを介して、Service Content と添付ファイルをプライベート プロセスから受信します。  
  
2. パブリック プロセスはプライベート プロセスに応答を送信しますが、これ以上の処理は行いません。  
  
3. マイクロソフトに通知を受信するパブリック プロセス場合、[!INCLUDE[BTARN_CurrentVersion_FirstRef](../../includes/btarn-currentversion-firstref-md.md)]メッセージ正常に送信して、パブリック プロセスとその状態、開始側プライベート プロセスに戻るを終了します。  
  
4. [!INCLUDE[btaBTARN3.3abbrevnonumber](../../includes/btabtarn3-3abbrevnonumber-md.md)] がメッセージを正常に送信したことを知らせる通知を受信すると、パブリック プロセスは (応答側のアクションを待つ) 待機状態になります。  
  
5. 次のアクションが発生すると、待機状態が終了します。  
  
   1.  パブリック プロセスが、応答側から受信確認シグナルを受信した場合。  
  
        シグナルの否認不可が必須 (プロセス構成で設定されている) の場合、プロセスはダイジェストを読み取り、シグナルのダイジェストと元のアクション メッセージのダイジェストを関連付けてから、シグナルを保存します。  
  
        パブリック プロセスが、シグナルのヘッダーと Service Content をプライベート プロセスに送信した場合。  
  
   2.  パブリック プロセスが、応答側からダブル アクションの応答メッセージを受信した場合。  
  
        プロセスが、Service Content とヘッダーを応答メッセージから抽出し、プライベート プロセスに送信した場合。  
  
        動作が同期の場合、プロセスは Service Content メッセージ部を Preamble、Service Header、Delivery Header (RNIF 2.01 の場合のみ) でラップして、RNIF シグナル メッセージを作成します。 プロセスは、開始側と応答側の間での取引先アグリーメントに保存されている情報 (双方の構成情報と PIP 変数) を使って Preamble とヘッダーを作成します。 次に、シグナル メッセージを応答側に送信します。  
  
        動作が非同期の場合、プロセスが終了します。  
  
   3.  パブリック プロセスが、応答側からエラー通知メッセージ (NoF) を受信した場合。 パブリック プロセスは、対応する状態メッセージを開始側プライベート プロセスに送信します。 プライベート プロセスがエラーを処理し、両方のプロセスを終了します。  
  
   4.  パブリック プロセスが、(プロセス構成で設定されている) 受信確認までの時間内に受信確認シグナルを受け取らなかった場合。 この場合、次のいずれかが発生します。  
  
        (プロセス構成で設定されている) 再試行回数が 0 になっておらず、動作が非同期の場合、パブリック プロセスはメッセージを再送信します。  
  
        (プロセス構成で設定されている) 再試行回数が 0 になっておらず、動作が同期の場合、パブリック プロセスは 0A1 メッセージを開始します。  
  
       > [!NOTE]
       >  CIDX は、0A1 メッセージをサポートしていません。  
  
        正常に送信できずに再試行回数が 0 になった場合、パブリック プロセスはエラー メッセージを送信します。設定が CIDX でない場合は、パブリック プロセスは 0A1 メッセージを送信します。  
  
        動作が同期で、設定が CIDX でないとき、パブリック プロセスは 0A1 メッセージを開始します。  
  
   5.  アクションが Time to Perform で定めた実行までの時間内に発生しない場合で、設定が CIDX でないとき、パブリック プロセスは 0A1 メッセージを送信します。  
  
## <a name="see-also"></a>参照  
 [パブリック プロセス](../../adapters-and-accelerators/accelerator-rosettanet/public-processes.md)   
 [レスポンダー パブリック プロセス](../../adapters-and-accelerators/accelerator-rosettanet/responder-public-process.md)