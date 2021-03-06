---
title: 'シングル サインオン: イベント 10530 |Microsoft Docs'
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 4bb37305-26fe-46a7-958d-3ed7f6876a7b
caps.latest.revision: 12
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 38eb770f795d23286b2a057a428e3bfec73e1674
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36974883"
---
# <a name="single-sign-on-event-10530"></a>シングル サインオン: イベント 10530
## <a name="details"></a>詳細  

|                 |                                                                                                                    |
|-----------------|--------------------------------------------------------------------------------------------------------------------|
|  製品名   |                                             エンタープライズ シングル サインオン                                              |
| 製品バージョン |                             [!INCLUDE[btsSSOVersion](../includes/btsssoversion-md.md)]                             |
|    イベント ID     |                                                       10530                                                        |
|  イベント ソース   |                                                       ENTSSO                                                       |
|    コンポーネント    |                                                        N\A                                                         |
|  シンボル名  |                                            SSO_INFO_GOT_PREVIOUS_SECRET                                            |
|  メッセージ テキスト   | マスター シークレット サーバーから以前のシークレットを取得しました。%r<br /><br /> シークレット サーバー名: %1 %r<br /><br /> MSID: %2 |

## <a name="explanation"></a>説明  
 この情報イベントは、SSO が以前のマスター シークレットを取得したことを示します。  

## <a name="user-action"></a>ユーザーの操作  

- ユーザーの操作は必要ありません。  

  詳細については、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] ヘルプの次の情報を参照してください:   

- [マスター シークレットを生成する方法](../core/how-to-generate-the-master-secret.md)  

- [マスター シークレットの管理](../core/managing-the-master-secret.md)
