---
title: クローズ タイムアウトが無効です |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b4510329-9fd9-428f-91a3-d72723e9a5e4
caps.latest.revision: 9
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: a73c7a6a21b57b8e8fbdff75d2c54d00e90b0a55
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36969475"
---
# <a name="invalid-close-timeout"></a>クローズ タイムアウトが無効です
## <a name="details"></a>詳細  

|                 |                                                                                          |
|-----------------|------------------------------------------------------------------------------------------|
|  製品名   |    [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]    |
| 製品バージョン |                [!INCLUDE[btsWCFVersion](../includes/btswcfversion-md.md)]                |
|    イベント ID     |                                            0                                             |
|  イベント ソース   |                                            0                                             |
|    コンポーネント    |                                            0                                             |
|  シンボル名  |                                            0                                             |
|  メッセージ テキスト   | クローズ タイムアウトが無効です。 有効な範囲: 0 ~ 23 時間、0 ~ 59 分、および 0 ~ 59 秒。 |

## <a name="explanation"></a>説明  

## <a name="user-action"></a>ユーザーの操作  
 タイムアウト範囲を構成するには、次の手順に従います。  

#### <a name="to-configure-the-timeout-range"></a>タイムアウト範囲を構成するには  

1. クリックして**開始**、 をクリックして**すべてのプログラム**、 をクリックして[!INCLUDE[btsBizTalkServerStartMenuItemui](../includes/btsbiztalkserverstartmenuitemui-md.md)]、 をクリック**BizTalk Server 管理**します。  

2. コンソール ルートで  [!INCLUDE[btsBizTalkServerAdminConsoleui](../includes/btsbiztalkserveradminconsoleui-md.md)]、展開**BizTalk グループ**、展開**アプリケーション**します。  

3. アプリケーションを特定し、次にトランスポートを特定します。  

4. トランスポート名を右クリックします。  

5. **[プロパティ]** をクリックします。  

6. ポート**型**一覧で、適切なポートを選択します。  

7. クリックして**構成**します。  

8. **WCF [**<em>トランスポートの種類</em>**] プロパティ**ダイアログ ボックスで、をクリックして、**バインド**タブ。  

9. タイムアウト範囲が有効なことを確認します。 使用可能な値は、0 ～ 23 時間、0 ～ 59 分、0 ～ 59 秒です。
