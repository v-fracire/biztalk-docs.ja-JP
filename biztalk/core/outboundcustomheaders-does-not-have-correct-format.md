---
title: "OutboundCustomHeaders は正しい形式はいません |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6097762b-01c9-48b8-8cee-ccd6b11d28d4
caps.latest.revision: "9"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: b3b81a8c9c605f646a8ac0b6df2045af05eb58e5
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="outboundcustomheaders-does-not-have-correct-format"></a>OutboundCustomHeaders は正しい形式はいません
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]|  
|製品バージョン|[!INCLUDE[btsWCFVersion](../includes/btswcfversion-md.md)]|  
|イベント ID|0|  
|イベント ソース|0|  
|コンポーネント|0|  
|シンボル名|0|  
|メッセージ テキスト|OutboundCustomHeaders は正しい形式ではありません|  
  
## <a name="explanation"></a>説明  
 WCF の値。InboundHeaders または WCF です。OutboundCustomHeaders が次の形式ではありません:\<ヘッダー >...\</headers >。  
  
## <a name="user-action"></a>ユーザーの操作  
 プロパティ値のラップ\<ヘッダー > 要素。  
  
 詳細については、次のリソースを参照してください、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]ヘルプします。  
  
-   [パイプライン コンポーネントでの WCF メッセージにおける SOAP ヘッダーの使用](../core/using-soap-headers-in-wcf-messages-with-pipeline-components.md)