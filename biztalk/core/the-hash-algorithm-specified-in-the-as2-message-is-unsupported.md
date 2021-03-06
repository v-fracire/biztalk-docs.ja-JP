---
title: AS2 メッセージに指定されたハッシュ アルゴリズムはサポートされていません |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 1b292238-f964-4275-bbfa-e21c9150abf7
caps.latest.revision: 8
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 8c3c46f65fb71ef810fc4e657df01e0065757cae
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "37008595"
---
# <a name="the-hash-algorithm-specified-in-the-as2-message-is-unsupported"></a>AS2 メッセージに指定されたハッシュ アルゴリズムがサポートされていません
## <a name="details"></a>詳細  
  
|                 |                                                                                        |
|-----------------|----------------------------------------------------------------------------------------|
|  製品名   |   [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]   |
| 製品バージョン |               [!INCLUDE[btsEDIVersion](../includes/btsediversion-md.md)]               |
|    イベント ID     |                                           -                                            |
|  イベント ソース   | [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] EDI |
|    コンポーネント    |                                       AS2 エンジン                                       |
|  シンボル名  |                            UnsupportedAS2HashAlgorithmError                            |
|  メッセージ テキスト   |            AS2 メッセージに指定されたハッシュ アルゴリズムがサポートされていません。             |
  
## <a name="explanation"></a>説明  
 このエラー/警告/情報イベントは、受信した AS2 メッセージの signed-receipt-micalg ヘッダーに指定された MIC ハッシュ アルゴリズムが有効な値ではないため、受信パイプラインで指定どおりに MDN を生成できなかったことを示します。  
  
## <a name="user-action"></a>ユーザーの操作  
 このエラーを解決するには、メッセージの送信者にアルゴリズムを MD5 または SHA1 に変更してもらい、メッセージを再送信します。