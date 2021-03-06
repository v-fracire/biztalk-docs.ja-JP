---
title: 'シングル サインオン: イベント 10727 |Microsoft Docs'
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 8ff7ac94-6f1e-4e56-853e-efc50b1fa1b6
caps.latest.revision: 11
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 5f25dd71e223452707ff00e23b6a3a3bc797d10f
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36970547"
---
# <a name="single-sign-on-event-10727"></a>シングル サインオン: イベント 10727
## <a name="details"></a>詳細  

|                 |                                                                                                                                          |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------|
|  製品名   |                                                        エンタープライズ シングル サインオン                                                         |
| 製品バージョン |                                        [!INCLUDE[btsSSOVersion](../includes/btsssoversion-md.md)]                                        |
|    イベント ID     |                                                                  10727                                                                   |
|  イベント ソース   |                                                                  ENTSSO                                                                  |
|    コンポーネント    |                                                                   N\A                                                                    |
|  シンボル名  |                                                      SSO_WARN_REPLAY_RECORD_FAILED                                                       |
|  メッセージ テキスト   | 保存された外部パスワード変更の再生が失敗しました。%r<br /><br /> アダプター: % 1 %r<br /><br /> ファイル名: % 2 %r<br /><br /> エラー コード: %3 |

## <a name="explanation"></a>説明  
 この警告は、再生ファイルに記録されたパスワード変更を SSO が再生できなかったことを示します。  

 ENTSSO サーバーから SSO データベースに接続できない場合、パスワード同期で再生ファイルが使用されます。 進行ファイルでは、SSO データベースとの接続が再度失われた場合に SSO で再生ファイルをどこまで読み取ることができるかを示します。  

## <a name="user-action"></a>ユーザーの操作  
 この警告を解決するには、次の操作を行います:   

- 関連するイベントについては、システムおよびアプリケーションのイベント ログを確認します。  

  詳細については、次のリソースを参照してください。  

- [パスワード同期を構成する方法](../core/how-to-configure-password-synchronization.md)  

- [パスワード同期](../core/password-synchronization2.md)
