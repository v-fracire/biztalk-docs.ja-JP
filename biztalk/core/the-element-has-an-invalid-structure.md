---
title: 要素に無効な構造が |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: bb94843c-cd21-48e3-ba30-aed0518b4d78
caps.latest.revision: 8
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: b626343ed00add57d6deab4b349a75b4df2164a1
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36987701"
---
# <a name="the-element-has-an-invalid-structure"></a>要素の構造が無効です
## <a name="details"></a>詳細  
  
|                 |                                                                                        |
|-----------------|----------------------------------------------------------------------------------------|
|  製品名   |   [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]   |
| 製品バージョン |               [!INCLUDE[btsEDIVersion](../includes/btsediversion-md.md)]               |
|    イベント ID     |                                           -                                            |
|  イベント ソース   | [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] EDI |
|    コンポーネント    |                                       EDI エンジン                                       |
|  シンボル名  |                      X12NseStructurallyInvalidElementDescription                       |
|  メッセージ テキスト   |                       要素 '{0}' が無効な構造                       |
  
## <a name="explanation"></a>説明  
 このエラー/警告/情報イベントは、データ要素に、該当するスキーマで指定されている構造がなかったため、受信パイプラインで受信インターチェンジを処理できなかったか、または送信パイプラインで送信インターチェンジを処理できなかったことを示します。  
  
## <a name="user-action"></a>ユーザーの操作  
 このエラーを解決するには、送信インターチェンジのデータ要素の構造を修正するか、またはインターチェンジの送信者に対して、受信インターチェンジのデータ要素の構造を変更し、ドキュメント スキーマに準拠するように依頼します。