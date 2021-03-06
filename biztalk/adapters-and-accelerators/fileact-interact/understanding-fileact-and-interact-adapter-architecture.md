---
title: 理解 FileAct および InterAct アダプターのアーキテクチャ |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 8f97a7fe-20df-4509-bb6e-53743c3a57df
caps.latest.revision: 16
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 7a587b70eb3ae603d59dd5a6f21270133b5a8125
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "37005307"
---
# <a name="understanding-fileact-and-interact-adapter-architecture"></a>理解 FileAct および InterAct アダプターのアーキテクチャ
SWIFT アダプターは、BizTalk アダプター フレームワークに基づきます。 BizTalk Server 内のアダプターの分類を使用して、FileAct および InterAct は、SWIFT アダプターを表す次。  
  
- カスタム アダプター。 これは、カスタム アダプター FileAct および Interact と呼ばれる独自の標準を使用する SWIFT ネットワークとやり取りするための専用です。  
  
- トランスポート アダプターです。 このアダプターは、SWIFT ネットワークとのメッセージを送受信する業務ソフトウェア アプリケーションを許可します。  
  
- 非トランザクションです。 アダプターを行わないの任意のトランザクション オブジェクトを使用して行う SWIFT ネットワークとやり取りします。  
  
- 分離。 受信アダプターが別のプロセスで実行し、通常の送信アダプターはプロセスで実行します。  
  
  BizTalk アダプター フレームワークについては、次を参照してください、"とは、アダプター フレームワーク"。 BizTalk Server ヘルプのトピックです。  
  
  FileAct および InterAct のアーキテクチャの概要を次の図に示します。  
  
  ![](../../adapters-and-accelerators/fileact-interact/media/035ebb05-ce11-447c-b56b-ba8b41e07e50.gif "035ebb05-ce11-447c-b56b-ba8b41e07e50")  
  
> [!NOTE]
>  Microsoft[!INCLUDE[swift_adapter](../../includes/swift-adapter-md.md)]厳格モード SWIFTNet リンク (SNL) API のみをサポートしています。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [SWIFTNet クライアントおよびサーバー](../../adapters-and-accelerators/fileact-interact/swiftnet-client-and-server.md)  
  
-   [SWIFT 送信アダプターのアーキテクチャ](../../adapters-and-accelerators/fileact-interact/swift-send-adapter-architecture.md)  
  
-   [SWIFT 受信アダプターのアーキテクチャ](../../adapters-and-accelerators/fileact-interact/swift-receive-adapter-architecture.md)  
  
-   [FileAct アダプターのアーキテクチャ](../../adapters-and-accelerators/fileact-interact/fileact-adapter-architecture.md)  
  
-   [InterAct アダプターのアーキテクチャ](../../adapters-and-accelerators/fileact-interact/interact-adapter-architecture.md)