---
title: 符号なし整数プロパティの値が無効です |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 63b0398f-7848-4971-8c08-95923d80cbe3
caps.latest.revision: 3
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: de6af46fc5719e8ccbe52dbfb419e104915d051e
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36973939"
---
# <a name="the-unsigned-integer-property-value-is-not-valid"></a>符号なし整数プロパティの値が無効です
## <a name="details"></a>詳細  
  
|                 |                                                                                        |
|-----------------|----------------------------------------------------------------------------------------|
|  製品名   |   [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]   |
| 製品バージョン |               [!INCLUDE[btsEDIVersion](../includes/btsediversion-md.md)]               |
|    イベント ID     |                                           -                                            |
|  イベント ソース   | [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] EDI |
|    コンポーネント    |                                       EDI エンジン                                       |
|  シンボル名  |                               Err_InvalidUnsignedInteger                               |
|  メッセージ テキスト   |                   符号なし整数プロパティの値が無効です。                    |
  
## <a name="explanation"></a>説明  
 このエラー/警告/情報イベントは、メッセージをバッチ処理するかどうかを判断する際に、BizTalk Server がコンテキスト プロパティを比較できなかったことを示します。  
  
## <a name="user-action"></a>ユーザーの操作  
 このエラーを解決するには、アクティブなバッチに含まれているフィルターで、符号なし整数を指定する XSD に無効な値を持つコンテキスト プロパティが指定されていないことを確認します。