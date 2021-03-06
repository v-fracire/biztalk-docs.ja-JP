---
title: 'シングル サインオン: イベント 10584 |Microsoft Docs'
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 8af9377d-b4fd-48a6-961a-3629b3db644a
caps.latest.revision: 6
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 0188f09ab94bd14df0dbe3fee0b91341cd9eb087
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36996723"
---
# <a name="single-sign-on-event-10584"></a>シングル サインオン: イベント 10584
## <a name="details"></a>詳細  
  
|                 |                                                                |
|-----------------|----------------------------------------------------------------|
|  製品名   |                   エンタープライズ シングル サインオン                    |
| 製品バージョン |   [!INCLUDE[btsSSOVersion](../includes/btsssoversion-md.md)]   |
|    イベント ID     |                             10584                              |
|  イベント ソース   |                             ENTSSO                             |
|    コンポーネント    |                              なし                               |
|  シンボル名  |                   SSO_WARN_NO_IMPERSONATION                    |
|  メッセージ テキスト   | クライアントを偽装できませんでした。%r<br /><br /> エラー コード: %1 |
  
## <a name="explanation"></a>説明  
 クライアントの偽装は、クライアントの ID を確認するために ENTSSO システムで行う処理です。 システムがクライアントを偽装できない場合、3 つのいずれかの状況が発生している可能性があります。 クライアントが通常のアクティビティを実行しようとしたか、クライアントがシステムのセキュリティに侵入しようとしたか、またはクライアント アプリケーションが偽装をブロックするように設計されている可能性があります。  
  
## <a name="user-action"></a>ユーザーの操作  
 クライアント アプリケーションを探し、どのような処理が行われようとしているか、およびクライアント アプリケーションが偽装をブロックしているかどうかを特定します。