---
title: 'シングル サインオン: イベント 10569 |Microsoft Docs'
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 2e051a84-51c1-4e63-be55-6278a1d17c5e
caps.latest.revision: 7
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 25665947921bb316a4d931228016eaf917b4a685
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36987203"
---
# <a name="single-sign-on-event-10569"></a>シングル サインオン: イベント 10569
## <a name="details"></a>詳細  
  
|                 |                                                                                                                                                                                                        |
|-----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  製品名   |                                                                                       エンタープライズ シングル サインオン                                                                                        |
| 製品バージョン |                                                                       [!INCLUDE[btsSSOVersion](../includes/btsssoversion-md.md)]                                                                       |
|    イベント ID     |                                                                                                 10569                                                                                                  |
|  イベント ソース   |                                                                                                 ENTSSO                                                                                                 |
|    コンポーネント    |                                                                                                  なし                                                                                                   |
|  シンボル名  |                                                                                    SSO_WARN_NO_UPDATE_BY_APP_ADMIN                                                                                     |
|  メッセージ テキスト   | このアプリケーション管理者アカウントを、アプリケーション管理者が変更することはできません。%r<br /><br /> アプリケーション名: %1 %r<br /><br /> アプリケーション管理者: % 2 %r<br /><br /> エラー コード: %3 |
  
## <a name="explanation"></a>説明  
 このアプリケーション管理者アカウントを、アプリケーション管理者が変更することはできません。  
  
## <a name="user-action"></a>ユーザーの操作  
 アプリケーション管理者アカウントを変更するには、SSO 関連アプリケーション管理者以上である必要があります。