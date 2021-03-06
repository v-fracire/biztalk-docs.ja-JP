---
title: 無効なセキュリティ値 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ee380da7-c05e-4b9b-84ee-f7ffee90eb0e
caps.latest.revision: 8
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 9d5c8cd6f07449ba426a9cb17f9f4aa880ff1b3e
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "37013747"
---
# <a name="invalid-security-value"></a>セキュリティの値が無効です
## <a name="details"></a>詳細  
  
|                 |                                                                                        |
|-----------------|----------------------------------------------------------------------------------------|
|  製品名   |   [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]   |
| 製品バージョン |               [!INCLUDE[btsEDIVersion](../includes/btsediversion-md.md)]               |
|    イベント ID     |                                           -                                            |
|  イベント ソース   | [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] EDI |
|    コンポーネント    |                                       EDI エンジン                                       |
|  シンボル名  |                         X12Ta1InvalidSecurityValueDescription                          |
|  メッセージ テキスト   |                                 セキュリティの値が無効です                                 |
  
## <a name="explanation"></a>説明  
 このエラー/警告/情報イベントは、ISA04 フィールドのセキュリティ情報または UNB6.1 フィールドの受信者の参照/パスワードの値が、サービス スキーマ (BaseArtifacts.dll 内の X12ServiceSchema または EdifactServiceSchema) で設定されたデータ型と桁数に準拠していなかったため、受信パイプラインで受信インターチェンジを処理できなかったことを示します。  
  
## <a name="user-action"></a>ユーザーの操作  
 このエラーを解決するには、ISA04 フィールドが X12_AN データ型で、長さが 10 桁 (末尾のスペースの有無とは無関係) であるか、または UNB6.1 フィールドが EDIFACT_AN データ型で、長さが 1 ～ 14 文字の範囲であることを確認します。 インターチェンジを再送信します。