---
title: トランザクション セットの重複する制御番号が見つかりました |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 1b2779a0-b365-4c4b-81c7-8f9284748b6e
caps.latest.revision: 9
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: d6b9b55dc5cd61bc4c8c806f2dc42259cadf2f69
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36977709"
---
# <a name="transaction-set-duplicate-control-number-found"></a>トランザクション セットの重複する制御番号が見つかりました
## <a name="details"></a>詳細  
  
|                 |                                                                                        |
|-----------------|----------------------------------------------------------------------------------------|
|  製品名   |   [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]   |
| 製品バージョン |               [!INCLUDE[btsEDIVersion](../includes/btsediversion-md.md)]               |
|    イベント ID     |                                           -                                            |
|  イベント ソース   | [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] EDI |
|    コンポーネント    |                                       EDI エンジン                                       |
|  シンボル名  |                          X12TsDuplicateNumberFoundDescription                          |
|  メッセージ テキスト   |                     トランザクション セットの重複する制御番号が見つかりました                     |
  
## <a name="explanation"></a>説明  
 このエラー/警告/情報イベントは、インターチェンジのいずれかのグループ内のトランザクション セット制御番号が、そのグループ内の別のトランザクション セットの制御番号と同じであったため、受信パイプラインで受信 X12 インターチェンジを処理できなかったことを示します。  
  
## <a name="user-action"></a>ユーザーの操作  
 このエラーを解決するには、次のいずれかの操作を行います。  
  
-   受信インターチェンジのトランザクション セットのトランザクション セット制御番号を変更し、グループ内でトランザクション セットの制御番号が重複しないようにします。  
  
-   次のようにして、重複するトランザクション セット制御番号の有無の確認を無効化します。  
  
    1.  BizTalk Server 管理コンソールを開きます。  
  
    2.  インターチェンジを送信したパーティの [EDI のプロパティ] ダイアログ ボックスを開きます。  
  
    3.  X12 インターチェンジの場合、[EDI のプロパティ] ダイアログ ボックスの [X12 インターチェンジ処理のプロパティ] ページで、[グループ内で重複している ST2 (トランザクション セット制御番号) を確認する] をオフにします。  
  
    4.  EDIFACT インターチェンジの場合、オフ、"チェックが重複している unh1 (トランザクション セット参照番号) グループで"EDIFACT インターチェンジ処理プロパティ ページで、[EDI のプロパティ] ダイアログ ボックスのプロパティ。