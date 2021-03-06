---
title: 'シングル サインオン: イベント 10742 |Microsoft Docs'
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ba62f878-ed12-421f-81ea-9285b2624fe9
caps.latest.revision: 10
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 43595ad7a6817bd63e200a80ea90e23bd0245ceb
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "37012995"
---
# <a name="single-sign-on-event-10742"></a>シングル サインオン: イベント 10742
## <a name="details"></a>詳細  

|                 |                                                                                                                                                                                                                                                                                                            |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  製品名   |                                                                                                                                         エンタープライズ シングル サインオン                                                                                                                                          |
| 製品バージョン |                                                                                                                         [!INCLUDE[btsSSOVersion](../includes/btsssoversion-md.md)]                                                                                                                         |
|    イベント ID     |                                                                                                                                                   10742                                                                                                                                                    |
|  イベント ソース   |                                                                                                                                                   ENTSSO                                                                                                                                                   |
|    コンポーネント    |                                                                                                                                                    N\A                                                                                                                                                     |
|  シンボル名  |                                                                                                                                         SSO_WARN_NO_UPDATE_ADAPTER                                                                                                                                         |
|  メッセージ テキスト   | アダプターを更新するには、クライアント ユーザーは SSO 管理者アカウントまたはアプリケーション管理者アカウントのメンバーであることが必要です。%r<br /><br /> クライアント ユーザー: 1 %r<br /><br /> SSO 管理者: % 2 %r<br /><br /> アプリケーション管理者: % 3 %r<br /><br /> アダプター: % 4 %r<br /><br /> エラー コード: %5 |

## <a name="explanation"></a>説明  
 この警告イベントは、指定されたアダプターの更新を試みましたが、使用されたユーザー アカウントが SSO 管理者アカウントまたはアプリケーション管理者アカウントのメンバーではないために完了できなかったことを示します。  

## <a name="user-action"></a>ユーザーの操作  
 この警告を解消するには、次の操作を行います:   

- SSO 管理者アカウントまたはアプリケーション管理者アカウントにユーザー アカウントを追加します。  

- 更新を再試行します。  

  詳細については、次のリソースを参照してください。  

- [パスワード同期を管理する方法](../core/how-to-administer-password-synchronization.md)
