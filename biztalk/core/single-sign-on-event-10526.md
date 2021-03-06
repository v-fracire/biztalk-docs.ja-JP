---
title: 'シングル サインオン: イベント 10526 |Microsoft Docs'
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0f72d466-8b63-453c-b608-f9d64f635f65
caps.latest.revision: 13
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 433190146391c494ff3b890c8332cc15fb947753
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "37024456"
---
# <a name="single-sign-on-event-10526"></a>シングル サインオン: イベント 10526
## <a name="details"></a>詳細  

|                 |                                                                                                                                                                   |
|-----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  製品名   |                                                                     エンタープライズ シングル サインオン                                                                     |
| 製品バージョン |                                                    [!INCLUDE[btsSSOVersion](../includes/btsssoversion-md.md)]                                                     |
|    イベント ID     |                                                                               10526                                                                               |
|  イベント ソース   |                                                                              ENTSSO                                                                               |
|    コンポーネント    |                                                                                N\A                                                                                |
|  シンボル名  |                                                                 SSO_ERROR_GENERATE_SECRET_FAILED                                                                  |
|  メッセージ テキスト   | 新しいマスター シークレットを生成できませんでした。%r<br /><br /> クライアント ユーザー: 1 %r<br /><br /> クライアント コンピューター: %2%r<br /><br /> 追跡 ID: % 3 %r<br /><br /> エラー コード: %4 |

## <a name="explanation"></a>説明  
 このエラー イベントは、ユーザーが新しいマスター シークレットを生成しようとしたが、失敗したことを示します。 原因としては、アクセス許可の問題 (マスター シークレットを生成するには SSO 管理者である必要がある) であるか、またはバックアップ ファイルへのマスター シークレットの書き込みに問題がある可能性があります。 これらの場合、アプリケーション イベント ログに関連するメッセージがあります。  

## <a name="user-action"></a>ユーザーの操作  
 このエラーを解決するには、以下の 1 つ以上の操作を実行します。  

- 関連するイベントまたはエラーについては、アプリケーション イベント ログを確認します。  

- 適切な SSO 管理者のアクセス許可があることを確認します。  

  詳細については、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] ヘルプの次の情報を参照してください:   

- [マスター シークレットを生成する方法](../core/how-to-generate-the-master-secret.md)  

- [マスター シークレットの管理](../core/managing-the-master-secret.md)
