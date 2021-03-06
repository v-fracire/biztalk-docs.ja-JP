---
title: DocType が設定されていないため、トランザクション セットの処理後に発生したエラー |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a323658c-77d8-4059-aa15-d88c08e5450d
caps.latest.revision: 8
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: df010d497f61a14644c46f8b7f5cdfa183340615
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "37003379"
---
# <a name="error-encountered-after-processing-transaction-sets-because-doctype-was-not-set"></a>DocType が設定されていないため、トランザクション セットの処理後にエラーが発生しました
## <a name="details"></a>詳細  
  
|                 |                                                                                        |
|-----------------|----------------------------------------------------------------------------------------|
|  製品名   |   [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]   |
| 製品バージョン |               [!INCLUDE[btsEDIVersion](../includes/btsediversion-md.md)]               |
|    イベント ID     |                                           -                                            |
|  イベント ソース   | [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] EDI |
|    コンポーネント    |                                       EDI エンジン                                       |
|  シンボル名  |                                     DocTypeNotSet                                      |
|  メッセージ テキスト   |     処理後に発生したエラー{0}トランザクション セットします。 DocType が設定されていません。     |
  
## <a name="explanation"></a>説明  
 このエラー/警告/情報イベントは、ST01 (X12 インターチェンジの場合) または UNH2.1 (EDIFACT インターチェンジの場合) がトランザクション セットに対して設定されなかったため、EDI 受信パイプラインで受信トランザクションを処理できなかったことを示します。  
  
## <a name="user-action"></a>ユーザーの操作  
 このエラーを解決するには、エラーの発生したトランザクション セットに対する ST01 または UNH1 セグメントが、有効なドキュメントの種類に設定されていることを確認します。