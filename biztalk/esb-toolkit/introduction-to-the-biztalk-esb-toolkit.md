---
title: BizTalk ESB Toolkit の概要 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- ESBToolkitV2.introduction
ms.assetid: 98a957b8-5855-4872-b7e7-58a2e1d6b2b8
caps.latest.revision: 8
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 5cfab980a869029d565d378aaf0f75a147403f3e
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36986723"
---
# <a name="introduction-to-the-biztalk-esb-toolkit"></a>BizTalk ESB Toolkit の概要
アーキテクチャと、Microsoft の内容について説明します[!INCLUDE[esbToolkit](../includes/esbtoolkit-md.md)]します。 ドキュメントは、および再利用可能なサービスと新しいエンド ツー エンドに既存のサービスの迅速な組織の柔軟で、セキュリティで保護を有効にするエンタープライズ アプリケーションを開発の Enterprise Service Bus (ESB) アーキテクチャ パターンを適用する方法も示していますビジネス プロセス。  

## <a name="what-is-an-enterprise-service-bus"></a>エンタープライズ サービス バスとは何ですか。  
 サービス指向アーキテクチャ (SOA) を有効にするためのインフラストラクチャの実装のコンテキストで Enterprise Service Bus が広く使用されているターム。 ただし、SOA ソリューションの展開の実際の経験、ESB は包括的なサービス指向インフラストラクチャ (SOI) を構築するために必要な多くのコンポーネントの 1 つだけを説明しました。 さまざまな方向で進化してきた"ESB"という用語 — 個々 の ESB との統合プラットフォーム ベンダーの解釈と特定の SOA イニシアティブの要件の定義が異なります。  

 Microsoft では、Microsoft が成功した多くの現実 SOI 実装から収集された経験に基づき、エンタープライズ サービス バスで従来エンタープライズ アプリケーション統合 (EAI)、ベースのアーキテクチャ パターンのコレクションにするメッセージ指向ミドルウェア、Web サービス、.NET と Java の相互運用性、ホスト システム統合、およびサービス レジストリおよび資産リポジトリとの相互運用。 図 1 は、エンタープライズ サービス バスのアーキテクチャを示しています。  

 ![ESB の概要](../esb-toolkit/media/esboverview.gif "ESBOverview")  

 **図 1**  

 **Enterprise Service Bus のアーキテクチャによって提供される接続の概要を示したもの**  

<!---  Old text with old links
## The Industry View of ESB  
 There are many sources of information about ESB design, architecture, infrastructure, and implementation available from industry suppliers, system integrators, and independent sources.  
-->
<!---    
 IBM defines ESB as a system that "...enables a business to make use of a comprehensive, flexible, and consistent approach to integration while also reducing the complexity of the applications being integrated. Due to the complex and varying nature of business needs, ESB is an evolutional progression that unifies message oriented, event driven and service oriented approaches for integrating applications and service." IBM describes the advantages as "...greater reuse of IT assets by separating application logics and integration tasks, so you can reduce the number, size, and complexity of integration interfaces," and the ability to "...add or change services with minimal interruption to existing IT environment; reduce cost and risk involved as business changes and new opportunities arise." For more information, see [WebSphere software](http://go.microsoft.com/fwlink/p/?LinkId=185958)([http://go.microsoft.com/fwlink/p/?LinkId=185958](http://go.microsoft.com/fwlink/p/?LinkId=185958))on the IBM Web site.  
-->
<!---    Old text with old links
 Sonic Solutions provide a comprehensive examination of ESB, discussing the principle aspects, and the IT and business benefits. They describe the requirement for ESB: "To integrate old and new, service-oriented architecture (SOA) needs an infrastructure that can connect any IT resource, whatever its technology or wherever it is deployed." For more information, see [Enterprise Service Bus (ESB)](http://go.microsoft.com/fwlink/p/?LinkId=185959)([http://go.microsoft.com/fwlink/p/?LinkId=185959](http://go.microsoft.com/fwlink/p/?LinkId=185959)) on the Sonic Solutions Web site.  
-->
<!---    Old text with old links
 TIBCO Software define ESB as "...a standards-based communication layer in a service- oriented architecture (SOA) that enables services to be used across multiple communication protocols [to] simplify service deployment and management, and promote service reuse in a heterogeneous environment." They suggest, in order to provide these capabilities, ESBs "...support both open standards and proprietary technologies, including Web services and UDDI-based registries to discover and publish services, Java Message Service (JMS) and other widely deployed messaging protocols, standards-based (XML) transformations, and basic message routing." For more information, see [Enterprise Service Bus (ESB)](http://go.microsoft.com/fwlink/p/?LinkId=185960)([http://go.microsoft.com/fwlink/?LinkId=185960](http://go.microsoft.com/fwlink/p/?LinkId=185960)) on the TIBCO Web site.  
-->
<!---    Old text with old links
 In the description of his book, Enterprise Service Bus, author David Chappell states that "Rather than conform to the hub-and-spoke architecture of traditional enterprise application integration products, ESB provides a highly distributed approach to integration." He adds "...with unique capabilities that allow individual departments or business units to build out their integration projects in incremental, digestible chunks, maintaining their own local control and autonomy, while still being able to connect together each integration project into a larger, more global integration fabric, or grid." For more information, see Enterprise Service Bus by David Chappell:  
-->
<!---    Old text with old links
-   Chappell, David. Enterprise Service Bus. Sebastopol, CA: O'Reilly Media, Inc. 2004.  
-->


## <a name="the-biztalk-esb-toolkit"></a>BizTalk ESB Toolkit
 このドキュメントでは、全体を紹介アーキテクトと開発者 ESB アーキテクチャの概念をによってアドレス指定された、 [!INCLUDE[esbToolkit](../includes/esbtoolkit-md.md)]、一般に認められた ESB ユース ケースのセットを通じて ESB コンポーネントの機能について説明します。  

 このセクションの概要を提供します、 [!INCLUDE[esbToolkit](../includes/esbtoolkit-md.md)]、次のトピックが含まれています。  

- [BizTalk ESB Toolkit の概要](../esb-toolkit/overview-of-the-biztalk-esb-toolkit.md)  

- [BizTalk ESB Toolkit の内容](../esb-toolkit/contents-of-the-biztalk-esb-toolkit.md)  

  このドキュメントでは、次のトピックのセクションも含まれます。  

- [BizTalk ESB Toolkit の作業の開始](../esb-toolkit/getting-started-with-the-biztalk-esb-toolkit.md)  

- [主要なシナリオと開発タスク](../esb-toolkit/key-scenarios-and-development-tasks.md)  

- [Itinerary Designer を利用してスケジュールを作成する](../esb-toolkit/creating-itineraries-using-itinerary-designer.md)  

- [BizTalk ESB Toolkit サンプル アプリケーション](../esb-toolkit/biztalk-esb-toolkit-sample-applications.md)  

- [BizTalk ESB Toolkit を変更し、拡張する](../esb-toolkit/modifying-and-extending-the-biztalk-esb-toolkit.md)  

- [BizTalk ESB Toolkit による管理](../esb-toolkit/administration-with-the-biztalk-esb-toolkit.md)  

- [SOA ガバナンス統合](../esb-toolkit/soa-governance-integration.md)  

- [トラブルシューティング](../esb-toolkit/troubleshooting-the-biztalk-esb-toolkit.md)
