---
title: 'シングル サインオン: イベント 10694 |Microsoft Docs'
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 75faca65-48d9-45f6-b079-2b612ef3de76
caps.latest.revision: 11
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 45d5bcd178020e6aee2b16e3cd3fbababd6b8498
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36981651"
---
# <a name="single-sign-on-event-10694"></a>シングル サインオン: イベント 10694
## <a name="details"></a>詳細  

|                 |                                                                                     |
|-----------------|-------------------------------------------------------------------------------------|
|  製品名   |                              エンタープライズ シングル サインオン                              |
| 製品バージョン |             [!INCLUDE[btsSSOVersion](../includes/btsssoversion-md.md)]              |
|    イベント ID     |                                        10694                                        |
|  イベント ソース   |                                       ENTSSO                                        |
|    コンポーネント    |                                         N\A                                         |
|  シンボル名  |                         SSO_ERROR_REPLAY_INCORRECT_VERSION                          |
|  メッセージ テキスト   | 再生ファイルまたは進行ファイルに破損が検出されました。%r<br /><br /> ファイル名: %1 |

## <a name="explanation"></a>説明  
 このエラー イベントは、SSO が SSO データベースとの接続を再確立したが、破損のために再生ファイルを読み取れなかったことを示しています。 SSO で再生ファイルを開くことができない場合、次の再生ファイルに進みます (次の再生ファイルがある場合)。  

 ENTSSO サーバーから SSO データベースに接続できない場合、パスワード同期で再生ファイルが使用されます。 進行ファイルでは、SSO データベースとの接続が再度失われた場合に SSO で再生ファイルをどこまで読み取ることができるかを示します。  

## <a name="user-action"></a>ユーザーの操作  
 このエラーを解決するには、次の操作を行います。  

- 関連するイベントについては、システムおよびアプリケーションのイベント ログを確認します。  

  詳細については、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] ヘルプの次の情報を参照してください:   

- [パスワード同期を構成する方法](../core/how-to-configure-password-synchronization.md)  

- [パスワード同期](../core/password-synchronization2.md)
