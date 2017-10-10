---
title: "Oracle E-business Suite アダプターでトランザクションの処理 |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b443be9d-a93d-4836-8717-5ee9dad4442f
caps.latest.revision: "6"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: e00b31230760d1bb811b987c3b1a926bad803b6d
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="handle-transactions-with-the-oracle-e-business-suite-adapter"></a>Oracle E-business Suite アダプターでトランザクションを処理します。
[!INCLUDE[adapteroracleebusinesslong](../../includes/adapteroracleebusinesslong-md.md)]Oracle E-business suite 操作の実行中にトランザクションを開始しません。 代わりに、アダプターは、アダプターのクライアントによって提供されるトランザクション コンテキストを使用して操作を実行します。 使用してトランザクションで操作を実行するために、 [!INCLUDE[adapteroraclebusinessshort](../../includes/adapteroraclebusinessshort-md.md)]、する必要があります。  
  
-   アダプターのクライアントのトランザクションを有効にします。 例については、トランザクションを有効にする[!INCLUDE[btsBizTalkServer2006r3](../../includes/btsbiztalkserver2006r3-md.md)]を選択する必要があります、 **Use-transaction**  チェック ボックス、**トランザクション**の領域、**メッセージ**タブに移動して、Wcf-custom または Wcf-oracleebs ポートです。  
  
-   値を設定、 **UseAmbientTransaction**にプロパティのバインド**True**アダプターでします。 バインディング プロパティの詳細については、次を参照してください。 [BizTalk Adapter for Oracle E-business Suite バインド プロパティ読む](../../adapters-and-accelerators/adapter-oracle-ebs/read-about-the-biztalk-adapter-for-oracle-e-business-suite-binding-properties.md)です。  
  
> [!IMPORTANT]
>  アダプターを使用すると、Oracle E-business Suite でトランザクションを実行して、する必要がありますがインストールされている、 **Microsoft Transaction Server のサービスの Oracle**コンポーネントは、アダプターを実行しているコンピューターに、Oracle クライアントをインストールするときにクライアントです。  
  
## <a name="transactions-in-the-outbound-operations"></a>送信操作のトランザクション  
 [!INCLUDE[adapteroraclebusinessshort](../../includes/adapteroraclebusinessshort-md.md)]単一のトランザクションで送信操作を実行します。 複合操作は、すべての操作を実行して、1 つのトランザクションではなく異なる ODP.NET 接続を使用します。 送信側に表示される操作の詳細については、[!INCLUDE[adapteroraclebusinessshort](../../includes/adapteroraclebusinessshort-md.md)]を参照してください[アダプター画面 Oracle E-business Suite のメタデータをどのように?](https://msdn.microsoft.com/library/dd788431.aspx)です。  
  
## <a name="transactions-in-the-inbound-operations"></a>受信操作のトランザクション  
 [!INCLUDE[adapteroraclebusinessshort](../../includes/adapteroraclebusinessshort-md.md)]次の 2 つの受信操作を公開します。  
  
-   **ポーリング**: ポーリング ステートメントおよび (指定した場合)、ポーリング後ステートメントが実行されるトランザクションでは、一方、別のトランザクションでポーリングされたデータの使用可能なステートメントを実行します。 同様に、ポーリング ステートメントとポーリング後ステートメントは、実行同じ ODP.NET 接続を使用して一方、ODP.NET は別の接続を使用してポーリングされたデータの使用可能なステートメントを実行します。  
  
-   **通知**: 通知操作は 1 つの ODP.NET 接続を使用して、トランザクションで実行します。  
  
 受信側に表示される操作の詳細については、[!INCLUDE[adapteroraclebusinessshort](../../includes/adapteroraclebusinessshort-md.md)]を参照してください[アダプター画面 Oracle E-business Suite のメタデータをどのように?](https://msdn.microsoft.com/library/dd788431.aspx)です。  
  
## <a name="see-also"></a>参照  
[Oracle E-business Suite の BizTalk アダプターを理解します。](../../adapters-and-accelerators/adapter-oracle-ebs/understand-biztalk-adapter-for-oracle-e-business-suite.md)