---
title: Functoid カテゴリ |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 029905e2-f01a-436a-b2ed-a364379c9cc5
caps.latest.revision: 10
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 6bf0b07020bb58725d7a9b20f0bc514c2421d02e
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "37015322"
---
# <a name="functoid-categories"></a>Functoid カテゴリ
BizTalk の Functoid は、使用目的に応じてカテゴリに分けられています。 たとえば、データベース Functoid は実行時にデータベースからデータを抽出することを目的とし、数値演算 Functoid は数学的演算を実行するために使用されます。 BizTalk マッパーでは、Functoid は [!INCLUDE[btsVStudioNoVersion](../includes/btsvstudionoversion-md.md)] ツールボックスにカテゴリごとに表示されます。 

## <a name="categories--description"></a>カテゴリと説明
次の表に、Functoid カテゴリ、カテゴリの簡単な説明、および各カテゴリの Functoid の一覧を、該当するリファレンス ページへのリンクと共に示します。  
  
|Functoid カテゴリ <br/><br/> カテゴリの説明|カテゴリに含まれる Functoid|  
|---|---|  
|**詳細設定** <br /><br /> 主にループ レコードと共に使用します。 また、任意のスクリプトやコンパイル済みコードを実行する場合にも使用します。|Assert、インデックス、ループのイテレーション、一括コピー、Nil 値、レコードの数、スクリプティング、テーブルの抽出、テーブル値のマッピングにすると、値のマッピング (フラット化) をループします。|  
|**変換** <br /><br /> ASCII型への変換、ASCII型からの変換、および数値基本型間の変換で使用します。|ASCII 文字の値の ASCII 文字、16 進数、8 進数|  
|**累積的です** <br /><br /> 平均および連結など、ループ レコードの数学的演算を実行する場合に使用します。|累積平均、累積的な連結、累積最大値、累積最小値、累積合計|  
|**[データベース]** <br /><br /> データベースからデータを抽出し、送信先インスタンス メッセージで利用する場合に使用します。|データベースを参照して、エラーが返される、メッセージの書式設定、アプリケーション ID の取得、アプリケーション値の取得、共通 ID の取得、共通値の取得、アプリケーション ID の削除、共通の ID 値抽出の設定|  
|**日付と時刻** <br /><br /> 現在の日時の取得、および時刻の差分を算出する場合に使用します。|日、日付、日付と時刻、時間を追加します。|  
|**論理** <br /><br /> より大きい、論理的な実態など、さまざまな論理演算を実行する場合に使用します。|Equal、Greater Than より大きいまたは Equal To、IsNil、小さい場合、論理数値、論理、論理 AND、日付検査、論理的な実体に等しいまたはそれよりも小さいいない、論理 OR、文字列の検査が等しくないです。|  
|**数学** <br /><br /> 加算および乗算など、さまざまな数値演算を実行する場合に使用します。|絶対値、加算、除算、整数、最大値、最小値、剰余、減算、乗算、ラウンド、平方根|  
|**[指数]** <br /><br /> 対数および三角関数など、さまざまな科学計算を実行する場合に使用します。|10 ^ n、アーク タンジェント、底指定対数、常用対数、コサイン、自然指数関数、自然対数、サイン、タンジェント、X ^ Y|  
|**String** <br /><br /> スペースの削除および文字列の連結など、さまざまな文字列関数を実行する場合に使用します。|小文字、サイズ、文字列の連結、文字列の抽出、文字列の検索文字列を左、文字列左スペース削除、文字列、文字列右スペース削除、大文字|  
  
> [!NOTE]
>  通常、Functoid の目的は名前で判断できます。  
> 
> [!NOTE]
>  Microsoft に含まれているすべての functoid[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]を除きインライン c# は、**データベース**functoid。  
  
## <a name="see-also"></a>参照  
 [基本 Functoid](../core/basic-functoids.md)   
 [高度な Functoid](../core/advanced-functoids.md)