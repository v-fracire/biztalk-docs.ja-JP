---
title: "構造体の要素を EDI グループ |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 100a7118-9c02-474e-8685-9e4bb6f52e81
caps.latest.revision: "13"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 555d7b86e069adda4f7761b698793fd4ec2af721
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="edi-group-structural-element"></a>EDI のグループ構造体要素
グループには、1 つ以上のトランザクション セットが含まれます。 1 つ EDIFACT のグループには、同じ種類のトランザクション セットが含まれる必要があります。 X12 グループには、類似した種類のトランザクション セット (トランザクション セットとグループ (GS01-ST01) のマッピングに基づく) または同じ種類のトランザクション セットが含まれる場合があります。 1 つのグループ (GS01) 内で同時にできるリスト類似した X12 トランザクション セット (ST01)、次の表。  
  
|GS01|ST01|  
|----------|----------|  
|CF|844|  
|CF|849|  
|DX|894|  
|DX|895|  
|FR|821|  
|FR|827|  
|GC (GC)|920|  
|GC (GC)|924|  
|GC (GC)|925|  
|GC (GC)|926|  
|HC|837|  
|HC|837_D|  
|HC|837_I|  
|HC|837_P|  
|IA|110|  
|IA|980|  
|IO|310|  
|IO|312|  
|ME|198|  
|ME|200|  
|ME|201|  
|ME|245|  
|ME|261|  
|ME|262|  
|ME|263|  
|ME|833|  
|ME|872|  
|MG|203|  
|MG|206|  
|MG|259|  
|MG|260|  
|MG|264|  
|MG|266|  
|OG|875|  
|OG|876|  
|PK|196|  
|PK|839|  
|QG|878|  
|QG|879|  
|QG|888|  
|QG|889|  
|QG|896|  
|QO|313|  
|QO|315|  
|RO|300|  
|RO|301|  
|RO|303|  
|RQ|836|  
|RQ|840|  
|RS|869|  
|RS|870|  
|SL|135|  
|SL|139|  
|SO|302|  
|SO|311|  
|SO|317|  
|SO|319|  
|SO|322|  
|SO|323|  
|SO|324|  
|SO|325|  
|SO|326|  
|SO|361|  
|TO|197|  
|TO|199|  
|TO|265|  
|TO|485|  
|TO|486|  
|TP|460|  
|TP|463|  
|TP|466|  
|TP|468|  
|TP|490|  
|TP|492|  
|TP|494|  
|WA|140|  
|WA|141|  
|WA|142|  
|WA|143|  
  
> [!NOTE]
>  HIPAA 5010 グループでは、1 つのグループ内に異なるバージョンのトランザクション セットが許可されます。  
  
 トランザクション セットの処理中に例外が発生した場合は、EDI パーティのプロパティを使用して、インターチェンジ全体を停止するか、エラーが発生したトランザクション セットのみを停止するかが決定されます。  
  
 グループは機能グループ ヘッダー (X12 では GS、EDIFACT では UNG) で始まり、機能グループ トレーラー (X12 では GE、EDIFACT では UNE) で終わる必要があります。 グループ ヘッダーには、送信者と受信者コード、日付と時刻、ヘッダーとトレーラー、機能グループ、およびその他の情報内に含まれる可能性があるトランザクション セットのコレクションを定義するグループの識別子に一致する制御番号が含まれています。 グループ トレーラーには、グループ内のトランザクション セットの数を示す要素が含まれます。  
  
 グループは、EDIFACT インターチェンジでは省略可能です。 EDIFACT インターチェンジの場合は、グループが存在しない場合でも複数のトランザクション セットに含めることができます (UNG セグメントが存在しない)。 この場合、すべてのトランザクション セットは同じ種類でなければなりません。これは、1 つのグループに含まれるトランザクション セットは同じ種類である必要があるためです。 たとえば、1 つのグループ内、または複数のグループを含んでいない 1 つのインターチェンジ内に、APERAK トランザクション セットと ORDERS トランザクション セットの両方を含めることはできません。  
  
 グループは、X12 インターチェンジでは必須です。