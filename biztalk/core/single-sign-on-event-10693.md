---
title: 'シングル サインオン: イベント 10693 |Microsoft Docs'
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 672bac7d-0ccc-4a42-a49d-57e387f4cf3a
caps.latest.revision: 11
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 8f9dd254fd81d54f0c60a2ea8b0a143e94ddd516
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "37009483"
---
# <a name="single-sign-on-event-10693"></a>シングル サインオン: イベント 10693
## <a name="details"></a>詳細  

|                 |                                                                                                        |
|-----------------|--------------------------------------------------------------------------------------------------------|
|  製品名   |                                       エンタープライズ シングル サインオン                                        |
| 製品バージョン |                       [!INCLUDE[btsSSOVersion](../includes/btsssoversion-md.md)]                       |
|    イベント ID     |                                                 10693                                                  |
|  イベント ソース   |                                                 ENTSSO                                                 |
|    コンポーネント    |                                                  N\A                                                   |
|  シンボル名  |                                    SSO_WARNING_REPLAY_CANNOT_CREATE                                    |
|  メッセージ テキスト   | 再生を作成または進行状況の file.%r できませんでした。<br /><br /> ファイル名: %1 %r<br /><br /> エラー コード: %2 |

## <a name="explanation"></a>説明  
 この警告イベントは、SSO データベースへの接続が失われたときに、SSO が再生ファイルや進行状況ファイルを作成できなかったことを示します。  

 ENTSSO サーバーから SSO データベースに接続できない場合、パスワード同期で再生ファイルが使用されます。 進行ファイルでは、SSO データベースとの接続が再度失われた場合に SSO で再生ファイルをどこまで読み取ることができるかを示します。  

## <a name="user-action"></a>ユーザーの操作  
 このエラーを解決するには、次の操作を行います。  

- 関連するイベントについては、システムおよびアプリケーションのイベント ログを確認します。  

  詳細については、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] ヘルプの次の情報を参照してください:   

- [パスワード同期を構成する方法](../core/how-to-configure-password-synchronization.md)  

- [パスワード同期](../core/password-synchronization2.md)
