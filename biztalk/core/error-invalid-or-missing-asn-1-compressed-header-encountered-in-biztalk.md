---
title: 無効か見つかりません ASN.1 圧縮ヘッダー圧縮解除処理中に発生した |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6e59afea-436c-42c0-b424-0b72dd9db9a8
caps.latest.revision: 12
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 682b30bdb513aa9318dbc56cd592aa0009d56e39
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "37011963"
---
# <a name="invalid-or-missing-asn1-compressed-header-encountered-during-decompression-processing"></a>圧縮解除処理中に無効な ASN.1 圧縮ヘッダーが検出されたか、ASN.1 圧縮ヘッダーが見つかりませんでした
## <a name="details"></a>詳細  
  
|                 |                                                                                        |
|-----------------|----------------------------------------------------------------------------------------|
|  製品名   |   [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]   |
| 製品バージョン |               [!INCLUDE[btsEDIVersion](../includes/btsediversion-md.md)]               |
|    イベント ID     |                                           -                                            |
|  イベント ソース   | [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] EDI |
|    コンポーネント    |                                       AS2 エンジン                                       |
|  シンボル名  |                                           -                                            |
|  メッセージ テキスト   | 圧縮解除処理中に無効な ASN.1 圧縮ヘッダーが検出されたか、ASN.1 圧縮ヘッダーが見つかりませんでした |
  
## <a name="explanation"></a>説明  
 このエラーは、圧縮データの ASN.1 構造に関係しています。 このエラーは、圧縮データの送信者が作成した圧縮データの構造に誤りがあるか、メッセージの改ざん (無許可の変更) があったことを示します。  
  
## <a name="user-action"></a>ユーザーの操作  
 圧縮データの構造を見直し、メッセージの改ざんがないかどうかを確認します。