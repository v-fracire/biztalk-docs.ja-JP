---
title: 'シングル サインオン: イベント 11013 |Microsoft Docs'
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 450836dc-ddeb-4423-9966-69ad173f2c87
caps.latest.revision: 6
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 9f251dcbe15fc53c45f0b253cd4437e9e123d54d
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "37000315"
---
# <a name="single-sign-on-event-11013"></a>シングル サインオン: イベント 11013
## <a name="details"></a>詳細  
  
|                 |                                                                                                                                                                                                      |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  製品名   |                                                                                      エンタープライズ シングル サインオン                                                                                       |
| 製品バージョン |                                                                      [!INCLUDE[btsSSOVersion](../includes/btsssoversion-md.md)]                                                                      |
|    イベント ID     |                                                                                                11013                                                                                                 |
|  イベント ソース   |                                                                                                ENTSSO                                                                                                |
|    コンポーネント    |                                                                                                 なし                                                                                                  |
|  シンボル名  |                                                                                        SSO_WARN_NOT_APP_USER                                                                                         |
|  メッセージ テキスト   | クライアント ユーザーがアプリケーション ユーザー アカウントのメンバーではありません。%r<br /><br /> 追跡 ID: %1 %r<br /><br /> クライアント ユーザー: %2\\% 3 %r<br /><br /> アプリケーション名: % 4 %r<br /><br /> アプリケーション ユーザー: %5 |
  
## <a name="explanation"></a>説明  
 クライアント ユーザーがアプリケーション ユーザー アカウントのメンバーではありません。 この警告は、監査レベルが高に設定されている場合にのみ表示されます。  
  
## <a name="user-action"></a>ユーザーの操作  
 この状況を解決するには、クライアント ユーザーをアプリケーション ユーザー アカウントのメンバーにする必要があります。 今後警告を表示しない場合は、監査レベルを低くします。