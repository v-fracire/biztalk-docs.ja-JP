---
title: アグリーメントにアクセスできません |。Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 72890ee9-54c9-48ed-8c6e-8b329d79c68b
caps.latest.revision: 16
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 4b9c8d8126a7b38d95adfce1e813dd2a86ccde24
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "37024536"
---
# <a name="unable-to-access-agreement"></a>アグリーメントにアクセスできません
## <a name="details"></a>詳細  

|                 |                                                                                        |
|-----------------|----------------------------------------------------------------------------------------|
|  製品名   |   [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]   |
| 製品バージョン |               [!INCLUDE[btsEDIVersion](../includes/btsediversion-md.md)]               |
|    イベント ID     |                                           -                                            |
|  イベント ソース   | [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] EDI |
|    コンポーネント    |                                       EDI エンジン                                       |
|  シンボル名  |                              UnableToLocateAS2PartyError                               |
|  メッセージ テキスト   |            アグリーメントにアクセスできません。 AS2From: {0} AS2To:{1}します。 エラー: {2}             |

## <a name="explanation"></a>説明  
 このエラーは、BizTalk Server が、指定された修飾子と値のパーティを見つけられなかったことを示します。  

## <a name="user-action"></a>ユーザーの操作  
 このエラーを解決するには、特定の修飾子のパーティ エイリアスを作成します。  

1. クリックして**開始**、] をクリックして**すべてのプログラム**、] をクリックして[!INCLUDE[btsBizTalkServerStartMenuItemui](../includes/btsbiztalkserverstartmenuitemui-md.md)]、順にクリックします**BizTalk Server 管理**します。  

2. [コンソール ルートで [ [!INCLUDE[btsBizTalkServerAdminConsoleui](../includes/btsbiztalkserveradminconsoleui-md.md)]、展開**BizTalk グループ**、] をクリック**パーティ**します。  

3. 適切なパーティを右クリックします。  

4. **[プロパティ]** をクリックします。  

5. [*パーティ名*]**パーティ プロパティ**] ダイアログ ボックスに、入力**ediint-as2 From 値**で、**名前**列。  

6. パーティ名を入力、**値**列。  

7. [**OK**] をクリックします。
