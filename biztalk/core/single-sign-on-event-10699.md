---
title: 'シングル サインオン: イベント 10699 |Microsoft Docs'
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: cff26533-e4d7-47b5-92d5-bd8c72fab89a
caps.latest.revision: 11
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 3802f04d2adf7d95a6ff10ae208acabbc1acf8ad
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36983371"
---
# <a name="single-sign-on-event-10699"></a>シングル サインオン: イベント 10699
## <a name="details"></a>詳細  

|                 |                                                                                                                                                                                                                                       |
|-----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  製品名   |                                                                                                       エンタープライズ シングル サインオン                                                                                                       |
| 製品バージョン |                                                                                      [!INCLUDE[btsSSOVersion](../includes/btsssoversion-md.md)]                                                                                       |
|    イベント ID     |                                                                                                                 10699                                                                                                                 |
|  イベント ソース   |                                                                                                                ENTSSO                                                                                                                 |
|    コンポーネント    |                                                                                                                  N\A                                                                                                                  |
|  シンボル名  |                                                                                           SSO_INFO_EXTERNAL_PASSWORD_CHANGE_RECEIVED_REPLAY                                                                                           |
|  メッセージ テキスト   | 外部パスワード変更をアダプターから受け取りました (再生ファイルから)。%r<br /><br /> 追跡 ID: %1 %r<br /><br /> アダプター: % 2 %r<br /><br /> 外部アカウント: % 3 %r<br /><br /> クライアント ユーザー: % 4 %r<br /><br /> レコード数: %5 |

## <a name="explanation"></a>説明  
 この情報イベントは、再生ファイルに記録されたアダプターから外部パスワード変更を受け取ったことを示します。 SSO は、保存されていた外部パスワード変更を再生ファイルから再生しています。  

 ENTSSO サーバーから SSO データベースに接続できない場合、パスワード同期で再生ファイルが使用されます。 進行ファイルでは、SSO データベースとの接続が再度失われた場合に SSO で再生ファイルをどこまで読み取ることができるかを示します。  

## <a name="user-action"></a>ユーザーの操作  

- ユーザーの操作は必要ありません。  

  詳細については、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] ヘルプの次の情報を参照してください:   

- [パスワード同期を構成する方法](../core/how-to-configure-password-synchronization.md)  

- [パスワード同期](../core/password-synchronization2.md)
