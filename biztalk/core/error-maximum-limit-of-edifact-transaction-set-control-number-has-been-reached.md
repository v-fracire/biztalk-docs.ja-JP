---
title: 受信確認の生成に失敗しましたパーティの設定の Edifact トランザクション セット制御番号の最大の制限に達した |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: bcbb6374-0403-42b0-892b-b35157a2c74a
caps.latest.revision: 11
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: b639f80d6ad203074e0542df6672f2d7b89aa2ec
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "37001347"
---
# <a name="acknowledgement-generation-has-failed-as-maximum-limit-of-edifact-transaction-set-control-number-has-been-reached-for-party-settings"></a>パーティの設定の EDIFACT トランザクション セット制御番号が上限に到達したため、受信確認の生成に失敗しました
## <a name="details"></a>詳細  
  
|                 |                                                                                                                                                                                                                                          |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  製品名   |                                                                            [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]                                                                            |
| 製品バージョン |                                                                                        [!INCLUDE[btsEDIVersion](../includes/btsediversion-md.md)]                                                                                        |
|    イベント ID     |                                                                                                                    -                                                                                                                     |
|  イベント ソース   |                                                                                                            BizTalk Server EDI                                                                                                            |
|    コンポーネント    |                                                                                                                EDI エンジン                                                                                                                |
|  シンボル名  |                                                                                                                    -                                                                                                                     |
|  メッセージ テキスト   | 上限のパーティのトランザクション セット制御番号に達した許容される Edifact 受信確認の生成に失敗しました{0}します。 パートナー アグリーメント マネージャーで、[Party in sender role] の [UNH 1] フィールドに移動して、カウンターをリセットしてください。 |
  
## <a name="explanation"></a>説明  
 このエラー/警告/情報イベントは、受信確認のトランザクション セット参照番号 (UNH1) で入力された制御番号が UNH1 の最大許容値より大きいために、BizTalk Server が EDIFACT インターチェンジの受信確認を生成できなかったことを示します。 この場合、BizTalk Server は EDI パーティのプロパティを使用して受信確認を作成しました。  
  
 トランザクション セット参照番号の最大値は、参照番号で使用する桁数によって決まります。 最大文字数は、参照番号が 14 文字、プレフィックスが 13 文字、サフィックスが 13 文字、3 つすべてのフィールドの組み合わせで 14 文字です。  
  
## <a name="user-action"></a>ユーザーの操作  
 このエラーを解決するには、[UNG および UNH セグメントの定義] ページのトランザクション セット参照番号 (UNH1) の参照番号フィールド (UNH1.2) を最大値よりも小さい値に設定し直します。 BizTalk Server 管理コンソールでの EDI のプロパティ ダイアログ ボックスで、このプロパティを設定します。