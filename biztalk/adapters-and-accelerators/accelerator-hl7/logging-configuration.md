---
title: "ログの構成 |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- configuring, auditing
- configuring, logging
- logging, configuring
- auditing, configuring
ms.assetid: 5cd7aec1-bd38-4d37-9a79-b01eeb89337d
caps.latest.revision: "7"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 058a1fce8105a3147fb2e537a9182e7d886bb953
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="logging-configuration"></a>ログの構成
同時に、 [!INCLUDE[btsCoName](../../includes/btsconame-md.md)] [!INCLUDE[btsBizTalkServer2006r3](../../includes/btsbiztalkserver2006r3-md.md)]と[!INCLUDE[HL7_CurrentVersion_FirstRef](../../includes/hl7-currentversion-firstref-md.md)]医療機関病院、クリニック、看護住宅などのトランザクションとデジタル エンタープライズ アプリケーション統合 (EAI) 通信をセキュリティで保護を提供します。 [!INCLUDE[btsBizTalkServerNoVersion](../../includes/btsbiztalkservernoversion-md.md)]アプリケーションのアクティビティおよびトランザクション処理の調整、動的にメッセージをルーティング、検証、およびデータを変換する機能を提供し、さまざまなアダプタ経由で転送します。 [!INCLUDE[btaBTAHL71.3abbrevnonumber](../../includes/btabtahl71-3abbrevnonumber-md.md)]米国規格協会 ANSI accredited ヘルス レベル 7 (HL7) をリアルタイムで医療のデータを交換プロバイダーのネットワークで医療/管理用のアプリケーションによって使用される標準のメッセージングをサポートします。  
  
 Accelerator システムを通過する HL7 メッセージは非常に重要となります。 たとえば、データは、患者の医療や金融取引可能性があります。 HL7 のセキュリティとプライバシーの規制に準拠するには、システム管理者は、次の操作できる必要があります。  
  
-   保留メッセージをデバッグします。  
  
-   潜在的な侵入者を検出し、セキュリティ侵害のリスクを低減する継続的にシステムとファイルのアクセスを監視します。  
  
 このセクションでは、監査を構成して、ログを確認し、監査データおよびイベント ログを解釈することを有効にして、ログに記録されたデータに対してクエリを実行する概念および手順に関する情報を提供します。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [ログ記録処理について](../../adapters-and-accelerators/accelerator-hl7/about-the-logging-process.md)  
  
-   [ログの構成](../../adapters-and-accelerators/accelerator-hl7/configuring-logging.md)