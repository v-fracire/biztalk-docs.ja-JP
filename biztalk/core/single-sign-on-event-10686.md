---
title: 'シングル サインオン: イベント 10686 |Microsoft Docs'
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a3e71f2a-e51d-4736-b06a-117142d30dae
caps.latest.revision: 11
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 363ec7268ca3088a4d7658bbf4497099c810f92f
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36987993"
---
# <a name="single-sign-on-event-10686"></a>シングル サインオン: イベント 10686
## <a name="details"></a>詳細  

|                 |                                                                           |
|-----------------|---------------------------------------------------------------------------|
|  製品名   |                         エンタープライズ シングル サインオン                         |
| 製品バージョン |        [!INCLUDE[btsSSOVersion](../includes/btsssoversion-md.md)]         |
|    イベント ID     |                                   10686                                   |
|  イベント ソース   |                                  ENTSSO                                   |
|    コンポーネント    |                                    N\A                                    |
|  シンボル名  |                          SSO_INFO_REPLAY_STARTED                          |
|  メッセージ テキスト   | 保存された外部パスワード変更を再生しています。%r<br /><br /> 再生ファイル: %1 |

## <a name="explanation"></a>説明  
 この情報イベントは、SSO が保存された外部パスワード変更ファイルを再生していることを示します。 ENTSSO サーバーから SSO データベースに接続できない場合、パスワード同期で再生ファイルが使用されます。  

## <a name="user-action"></a>ユーザーの操作  

- ユーザーの操作は必要ありません。  

  詳細については、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] ヘルプの次の情報を参照してください:   

- [パスワード同期を構成する方法](../core/how-to-configure-password-synchronization.md)  

- [パスワード同期](../core/password-synchronization2.md)
