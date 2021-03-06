---
title: 受信アダプターのバッチでサポートされているトランザクション パブリケーション用のインターフェイス |Microsoft ドキュメント
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 5289e8b8-4447-4196-9f7c-5e60c6598d8d
caps.latest.revision: 9
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 27b51a67f63f3088ce64c9db35c368289ce156d2
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
ms.locfileid: "22257578"
---
# <a name="interfaces-for-a-transactional-batch-supported-receive-adapter"></a>バッチ処理に対応したトランザクション受信アダプター用のインターフェイス
メッセージのトランザクション送信が必要な場合、受信アダプターはトランザクションを作成して制御します。  
  
 トランザクション受信アダプターを作成し、上の Microsoft 分散トランザクション コーディネーター (MSDTC) トランザクションにポインターを渡します、**完了**のメソッド、 **IBTTransportBatch**インターフェイスです。 これにより、すべてのバッチ操作がその特定のトランザクション オブジェクトのスコープ内で実行されることが保証されます。 バッチ送信が完了すると、アダプターのコールバック メソッドがトランザクションをコミットまたはロールバックします。 どちらのアクションを実行するかは、トランスポート プロキシから返されるステータス、および場合によっては、アダプターが実行する、トランスポート プロキシには認識されない他のトランザクション関連処理によって決まります。 アダプターは、トランザクションの失敗または成功を判断します。 アダプター (コミットまたはロールバック) トランザクションの結果に報告、トランスポート プロキシを使用して、 **DTCCommitConfirm**のメソッド、**IBTDTCCommitConfirm**インターフェイスです。 トランザクションが成功した場合は `true` を渡し、失敗した場合は `false` を渡します。  
  
 バッチ処理に対応したトランザクション受信アダプターを作成するときの、オブジェクト間の対話処理を次に示します。  
  
 ![](../core/media/ebiz-sdk-devadapter2.gif "ebiz_sdk_devadapter2")  
DTC トランザクションを使用してメッセージのバッチを送信する受信アダプターのワークフロー  
  
## <a name="see-also"></a>参照  
 [アダプタの変数](../core/adapter-variables.md)   
 [開発、受信アダプター](../core/developing-a-receive-adapter.md)   
 [インスタンス化と初期化、アダプターの受信](../core/instantiating-and-initializing-a-receive-adapter.md)   
 [受信アダプターをインプロセスで用のインターフェイス](../core/interfaces-for-an-in-process-receive-adapter.md)   
 [受信アダプターの分離用のインターフェイス](../core/interfaces-for-an-isolated-receive-adapter.md)   
 [受信アダプターのバッチ サポート用のインターフェイス](../core/interfaces-for-a-batch-supported-receive-adapter.md)   
 [アダプターの受信要求-応答の同期用のインターフェイス](../core/interfaces-for-a-synchronous-request-response-receive-adapter.md)