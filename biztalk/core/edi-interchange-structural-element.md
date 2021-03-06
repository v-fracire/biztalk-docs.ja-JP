---
title: EDI インターチェンジの構造体要素 |Microsoft ドキュメント
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 03f47ae2-fa0f-4d88-a700-85f3d515d2d0
caps.latest.revision: 12
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: cc07ae40a3665b47b446b61e24954ca9c588a6a7
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
ms.locfileid: "22239530"
---
# <a name="edi-interchange-structural-element"></a>EDI のインターチェンジ構造体要素
インターチェンジは、EDI メッセージの最上位レベルの構造体要素です。 これには、2 つのパートナーによって交換される 1 つ以上のグループのコレクションが格納されます。 インターチェンジの送信先は、1 つの取引先である必要があります。 インターチェンジには、1 つ以上の種類のトランザクション セット/メッセージを格納できます。  
  
 インターチェンジでは、インターチェンジ自体とそれに含まれるグループおよびトランザクション セット/メッセージが、ヘッダーによって定義されます。 セグメント、データ要素、およびサブ要素は区切り記号によって定義されます。 各区切り記号には既定値がありますが、パーティによって異なる文字で定義されている可能性があります。 EDIFACT インターチェンジでインターチェンジの区切り記号として使用するために選択されている文字は、独立した UNA インターチェンジ ヘッダーで定義されます。 X12 インターチェンジでは、区切り記号が ISA インターチェンジ ヘッダーで定義されます。 X12 では、データ要素の区切り記号は 4 番目の文字位置にある文字であり、データ セグメント終了記号は最後の文字位置にある文字です。 他の X12 区切り記号およびすべての EDIFACT 区切り記号は、フィールドによって定義されます。たとえば、X12 コンポーネント区切り記号は ISA16 フィードによって定義され、EDIFACT データ要素の区切り記号は UNA2 フィールドによって定義されます。  
  
 インターチェンジには、EDI メッセージを定義するエンベロープが含まれます。 エンベロープはインターチェンジ ヘッダー (X12 では ISA、EDIFACT では UNA/UNB) で始まり、インターチェンジ トレーラー (IEA/UNZ) で終わる必要があります。 インターチェンジ ヘッダーには、送信者と受信者、日時、バージョン番号、ヘッダーとトレーラーに一致する制御番号、およびその他の情報を定義する要素が含まれます。  
  
 ISA12 フィールドと GS8 フィールド (X12 インターチェンジの場合)、および UNH2 フィールド (EDIFACT インターチェンジの場合) には、スキーマ探索に必要なバージョン情報が含まれます。  
  
 インターチェンジ トレーラーには、インターチェンジ内のグループの数を示す要素があります。  
  
> [!NOTE]
>  機能セキュリティ ヘッダー、機能保証ヘッダー、機能セキュリティ値セグメント、および機能セキュリティ トレーラー セグメントは、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] EDI および AS2 の対象外です。 このようなセグメントを含むインターチェンジを受信した場合、これらが認識不可能なセグメントであることを示すエラー ログが生成され、インターチェンジが中断されます。