---
title: MQSeries アダプターの高可用性 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- performance, MQSeries adapters
- MQSeries adapters, availability
- MQSeries adapters, performance
- high availability, MQSeries adapters
ms.assetid: 4339b10b-b35d-47c0-b78a-c60207e06c8e
caps.latest.revision: 16
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 145577ce280595ff959596cff99fd08f334e8993
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "37008851"
---
# <a name="mqseries-adapter-high-availability"></a>MQSeries アダプターの高可用性
MQSeries アダプターを使用する場合、次に示すいくつかの方法で可用性を向上させることができます。  
  
- [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 用にフォールト トレランスのホスティング環境を設定します。  
  
- IBM WebSphere MQ で Windows クラスタリングを使用します。  
  
  フォールト トレランスについては、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]を参照してください[BizTalk Server のサンプル アーキテクチャ](../core/sample-biztalk-server-architectures.md)と[フォールト トレランスのためのプラットフォームの計画](../core/planning-your-platform-for-fault-tolerance.md)で[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]ヘルプします。  
  
  [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] MQSeries アダプターが MQSAgent コンポーネントのリモート インストールと通信できるようにするには、IBM WebSphere MQ がインストールされている [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] およびサーバー上でネットワーク COM+ アクセスを有効にしておいてください。 ネットワーク COM + アクセスを有効にする方法の詳細については、マイクロソフト サポート技術情報の資料 817065 を参照してください。"Windows Server 2003 でネットワーク COM + アクセスを有効にする方法」でご利用いただけます[ http://go.microsoft.com/fwlink/?LinkId=196580](http://go.microsoft.com/fwlink/?LinkId=196580)します。  
  
  [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] MQSeries アダプターと共に使用される MQSAgent (MQSAgent2) COM+ アプリケーションをクラスター化するための要件はありません。 このコンポーネントの高可用性を確保するためには、各クラスター ノードにコンポーネントをインストールしてください。 COM+ アプリケーションが停止した場合、クライアントから次に呼び出されたときに開始されます。  
  
## <a name="see-also"></a>参照  
 [MQSeries アダプターの使用](../core/using-the-mqseries-adapter.md)