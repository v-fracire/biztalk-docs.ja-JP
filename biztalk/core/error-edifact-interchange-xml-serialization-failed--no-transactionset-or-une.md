---
title: 無効な構造、ありません transactionSet または UNE のための Edifact インターチェンジの Xml シリアル化に失敗しました |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3ce1c219-f2ed-46c1-ae4b-8a4206f7cd01
caps.latest.revision: 8
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 9fc0661bfbc88c78a9afda7811c9a183b2160b05
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36986587"
---
# <a name="edifact-interchange-xml-serialization-failed-due-to-invalid-structure-no-transactionset-or-une"></a>無効な構造により、EDIFACT インターチェンジの XML シリアル化に失敗しました。TransactionSet または UNE はありません
## <a name="details"></a>詳細  
  
|                 |                                                                                                                         |
|-----------------|-------------------------------------------------------------------------------------------------------------------------|
|  製品名   |                   [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]                    |
| 製品バージョン |                               [!INCLUDE[btsEDIVersion](../includes/btsediversion-md.md)]                                |
|    イベント ID     |                                                            -                                                            |
|  イベント ソース   |                 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] EDI                  |
|    コンポーネント    |                                                       EDI エンジン                                                        |
|  シンボル名  |                                            EfactTransactionSetOrUneNotFound                                             |
|  メッセージ テキスト   | 無効な構造により、EDIFACT インターチェンジの XML シリアル化に失敗しました。 TransactionSet または UNE を検索しましたが、見つかりませんでした。 |
  
## <a name="explanation"></a>説明  
 このエラー/警告/情報イベントは、最初のセグメントが UNA または UNB のいずれのセグメントでもなかったため、EDI 受信パイプラインで受信 EDIFACT インターチェンジを処理できなかったことを示します。 UNA セグメントは省略可能ですが、UNB セグメントは必須です。  
  
## <a name="user-action"></a>ユーザーの操作  
 このエラーを解決するには、インターチェンジの送信者が、グループ内のトランザクション セットの後に別のトランザクション セットが続くか、または UNE セグメントが続くようにメッセージを構成していることを確認します。 その後、送信者にインターチェンジを再送信してもらいます。