---
title: AS2 パイプラインのプロパティの構成 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- bts10.edir2.AS2.pipeline.properties
ms.assetid: 7faf6b05-710a-4d00-8c77-590ce9d9f962
caps.latest.revision: 7
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 0d2bb679e4e150382cd8ff3e80c838d269ba908f
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36988875"
---
# <a name="configuring-as2-pipeline-properties"></a>AS2 パイプラインのプロパティの構成
パイプラインのプロパティは、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] が送信または受信されたインターチェンジに解決されるアグリーメントを特定できなかった場合に、受信または送信 AS2 メッセージの処理で使用されます。  
  
## <a name="prerequisites"></a>前提条件  
 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 管理者グループまたは [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] B2B Operators グループのメンバーとしてログオンしている必要があります。  
  
## <a name="as2-pipeline-properties"></a>AS2 パイプラインのプロパティ  
 AS2 パイプラインでは、次のプロパティを設定できます。  
  
|プロパティ|新しく使用する機能|値|パイプライン/ステージ|  
|--------------|---------|------------|---------------------|  
|ContentTransferEncoding|バイナリ データを ASCII テキスト形式で表現するために使用する方法を示します。|8bit (既定)<br /><br /> 7bit<br /><br /> 8bit|AS2EdiSend/エンコード<br /><br /> AS2Send/エンコード|  
  
### <a name="to-set-a-pipeline-property"></a>パイプライン プロパティの設定  
  
1. [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 管理コンソールで、プロパティを設定するパイプラインを使用している受信場所または送信ポートを右クリックします。 **[プロパティ]** をクリックします。  
  
2. プロパティを設定する対象のパイプラインの横にある省略記号ボタン ([…]) をクリックします。  
  
3. プロパティの値を入力し、クリックして**OK**します。  
  
## <a name="see-also"></a>参照  
 [BizTalk Server AS2 ソリューションの開発と構成](../core/developing-and-configuring-biztalk-server-as2-solutions.md)