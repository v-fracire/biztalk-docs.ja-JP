---
title: アドレスが無効です (相対 uri にスラッシュが必要があります (&quot;-&quot;)) |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 1376f924-f119-4ba8-9be1-eea7ba5f3eb6
caps.latest.revision: 22
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 39a0e45cf540b07f167f2ca2a2ffcb52851e0327
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "37023536"
---
# <a name="invalid-address-relative-uri-needs-slash-quot-quot"></a>アドレスが無効です (相対 uri にスラッシュが必要があります (&quot;-&quot;))
## <a name="details"></a>詳細  
  
|                 |                                                                                    |
|-----------------|------------------------------------------------------------------------------------|
|  製品名   | [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] |
| 製品バージョン |             [!INCLUDE[btsWCFVersion](../includes/btswcfversion-md.md)]             |
|    イベント ID     |                                         0                                          |
|  イベント ソース   |                                         0                                          |
|    コンポーネント    |                                         0                                          |
|  シンボル名  |                                         0                                          |
|  メッセージ テキスト   |         アドレスが無効です。スラッシュ ("/") で始まる相対 URI を指定してください。          |
  
## <a name="explanation"></a>説明  
 正しい形式の相対アドレスを使用して WCF 分離受信場所が指定されていませんでした。 たとえば、 http://localhost/svc 相対アドレスとしては機能しません。 WCF 分離受信場所の "アドレス" プロパティを絶対アドレスに設定することはできません。  
  
## <a name="user-action"></a>ユーザーの操作  
 アドレスを構成するには、次の手順を実行します。  
  
#### <a name="to-configure-an-address"></a>アドレスを構成するには  
  
1. をクリックして**開始**、 をクリックして**すべてのプログラム**、 をクリックして**Microsoft [!INCLUDE[btsBizTalkServer2006r3ui](../includes/btsbiztalkserver2006r3ui-md.md)]** 、 をクリック**BizTalk Server 管理コンソール**です。  
  
2. コンソール ルートで展開**BizTalk Server 管理**、展開**BizTalk グループ**、展開**アプリケーション**します。  
  
3. アプリケーションを見つけて、トランスポートを特定します。  
  
4. トランスポート名を右クリックします。  
  
5. **[プロパティ]** をクリックします。  
  
6. ポート**型**一覧で、適切なポートを選択します。  
  
7. クリックして**構成**します。  
  
8. **WCF [**<em>トランスポートの種類</em>**] トランスポートのプロパティ**ダイアログ ボックスで、をクリックして、**全般**タブ。  
  
9. **アドレス (URI)** テキスト ボックスに、アドレスを変更します。 整形式の相対アドレスの一例は /path/service.svc です。  
  
   受信場所の詳細については、以下を参照してください。  
  
-   [Wcf-customisolated 受信場所を構成する方法](../core/how-to-configure-a-wcf-customisolated-receive-location.md)  
  
-   [Wcf-wshttp 受信場所を構成する方法](../core/how-to-configure-a-wcf-wshttp-receive-location.md)  
  
-   [Wcf-basichttp 受信場所を構成する方法](http://msdn.microsoft.com/library/43f18e5d-ba28-453c-b8ce-5bcdc6f27fdd)