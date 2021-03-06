---
title: X12 グローバル トランザクションの上限エラー確認の生成に失敗しました |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 8bbcae14-6e5c-4f79-87c6-311b4b54c7ff
caps.latest.revision: 9
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 3ef251a7e9af04245d1987e2d196a03f7c01b911
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36980483"
---
# <a name="error-ack-generation-has-failed-as-maximum-limit-of-x12-transaction-global"></a>X12 グローバル トランザクションの上限エラー確認の生成に失敗しました
## <a name="details"></a>詳細  
  
|                 |                                                                                                                                                                                                                                                     |
|-----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  製品名   |                                                                                 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]                                                                                  |
| 製品バージョン |                                                                                             [!INCLUDE[btsEDIVersion](../includes/btsediversion-md.md)]                                                                                              |
|    イベント ID     |                                                                                                                          -                                                                                                                          |
|  イベント ソース   |                                                                                                                 BizTalk Server EDI                                                                                                                  |
|    コンポーネント    |                                                                                                                     EDI エンジン                                                                                                                      |
|  シンボル名  |                                                                                                                          -                                                                                                                          |
|  メッセージ テキスト   | Guest の設定の X12 トランザクション セット制御番号が、許容される上限に到達したため、受信確認の生成に失敗しました。 パートナー アグリーメント マネージャーで、[Global configuration sender role] の [ST 2] フィールドに移動して、カウンターをリセットしてください。 |
  
## <a name="explanation"></a>説明  
 このエラー/警告/情報イベントは、受信確認のトランザクション セット参照番号 (ST2) で入力された制御番号が ST2 の最大許容値より大きいために、BizTalk Server が X12 インターチェンジの受信確認を生成できなかったことを示します。 この場合、BizTalk Server は EDI グローバル プロパティを使用して受信確認を作成しました。  
  
 トランザクション セット制御番号の最大値は、制御番号で使用する桁数によって決まります。 3 つのフィールドを合わせた最大長は 9 文字です。プレフィックス フィールドとサフィックス フィールドの最大長は 8 文字です。  
  
## <a name="user-action"></a>ユーザーの操作  
 このエラーを解決するには、[GS および ST セグメントの定義] ページのトランザクション セット制御番号 (ST2) の制御番号フィールド (ST2.2) を最大値よりも小さい値に設定し直します。 BizTalk Server 管理コンソールの [EDI グローバル プロパティ] ダイアログ ボックスには、このプロパティを設定します。