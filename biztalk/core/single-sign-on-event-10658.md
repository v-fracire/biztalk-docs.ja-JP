---
title: 'シングル サインオン: イベント 10658 |Microsoft Docs'
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c5bee12d-502b-4fee-bc84-25807eb0e48e
caps.latest.revision: 10
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: dd6ea4cb33e6df4fe8a59fc1041861bdb530aaa4
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36982251"
---
# <a name="single-sign-on-event-10658"></a>シングル サインオン: イベント 10658
## <a name="details"></a>詳細  

|                 |                                                                                   |
|-----------------|-----------------------------------------------------------------------------------|
|  製品名   |                             エンタープライズ シングル サインオン                             |
| 製品バージョン |            [!INCLUDE[btsSSOVersion](../includes/btsssoversion-md.md)]             |
|    イベント ID     |                                       10658                                       |
|  イベント ソース   |                                      ENTSSO                                       |
|    コンポーネント    |                                        N\A                                        |
|  シンボル名  |                   SSO_ERROR_PASSWORD_SYNC_ADAPTERS_START_FAILED                   |
|  メッセージ テキスト   | 外部アダプターのパスワード同期を開始できませんでした。%r<br /><br /> エラー コード: %1 |

## <a name="explanation"></a>説明  
 このエラー イベントは、外部アダプターのパスワード同期を開始できなかったことを示します。  

## <a name="user-action"></a>ユーザーの操作  
 このエラーを解決するには、以下の 1 つ以上の操作を実行します。  

-   関連するイベントについては、アプリケーションとシステムのイベント ログを確認します。  

-   アダプター構成プロパティを確認します。  

## <a name="more-info"></a>詳細  

- [パスワード同期を管理する方法](../core/how-to-administer-password-synchronization.md)  

- **エンタープライズ シングル サインオン UI のヘルプ** [!INCLUDE[ui-guidance-developers-reference](../includes/ui-guidance-developers-reference.md)]
