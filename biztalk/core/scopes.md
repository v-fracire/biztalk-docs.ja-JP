---
title: "スコープ |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- scopes, exception handling
- Scope shape [Orchestration Designer], nesting
- scopes, variables
- scopes, Scope shape [Orchestration Designer]
- Scope shape [Orchestration Designer], exception handling
- scopes, transactions
- scopes, synchronization
- scopes, nesting
- Scope shape [Orchestration Designer], transactions
ms.assetid: 51d81ce4-0034-4415-b6ab-4c952737c1bd
caps.latest.revision: "11"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 2bc4d1b5d926540477293591ade8123126be1b84
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="scopes"></a>スコープ
スコープは、アクションをグループ化するためのフレームワークです。 これは主に、トランザクションの実行および例外処理に使用されます。  
  
 1 つのスコープには、1 つ以上のブロックが含まれます。 スコープには本体があり、オプションとして任意の数の例外処理ブロックを付加できます。 スコープの特性に応じて、オプションの補正ブロックも使用できます。 スコープによっては、例外処理だけに使用され、補正が不要な場合もあります。 明示的にトランザクションに使用されるスコープもあり、それらは常に、ユーザーが既定の補正ハンドラーに対して作成するオプションの補正ハンドラーと共に、既定の補正ハンドラーを持ちます。 トランザクション スコープには、既定の例外ハンドラー、および既定の例外ハンドラーに対してユーザーが作成する任意の数の追加の例外ハンドラーもあります。  
  
## <a name="synchronized-scopes"></a>同期スコープ  
 スコープを同期するか、同期しないかを指定できます。 スコープを同期することによって、スコープ内でアクセスされた任意の共有データがオーケストレーション内の 1 つ以上の並列アクションによって書き込まることがなくなり、別のアクションがそのデータを読み取っている間にそのデータに対する書き込みが行われることもなくなります。  
  
 アトミック トランザクション スコープは、常に同期されます。 同期されたスコープ内のすべてのアクションは、同期済みと見なされます。同様に、そのスコープの任意の例外ハンドラーのすべてのアクションも同期済みと見なされます。 トランザクション スコープの補正ハンドラーのアクションは、同期されません。  
  
> [!CAUTION]
>  処理方法を慎重に計画しないと、デッドロック状態が発生する可能性があることに注意してください。 たとえば、オーケストレーション A の 1 つの並列の 2 つの分岐は、それぞれ同じメッセージにアクセスし、1 つはメッセージを送信し、もう 1 つはメッセージを受信します。このため、両方の分岐が同期スコープを持つ必要があります。 2 番目のオーケストレーションはメッセージを受信し、返信します。 オーケストレーション A の送信側の分岐が、受信側の分岐の前にロックを受信し、デッドロック状態で終了する可能性があります。  
  
## <a name="nesting-of-scopes"></a>スコープの入れ子  
 入れ子にすることができます**スコープ**他の内部の図形**スコープ**図形です。 スコープを入れ子にするための規則は次のとおりです。  
  
-   トランザクション スコープまたは同期スコープは、同期スコープ内 (同期スコープの例外ハンドラーを含む) に入れ子にすることはできません。  
  
-   アトミック トランザクションのスコープ内には、その他のトランザクション スコープを入れ子にすることはできません。  
  
-   トランザクション スコープは、トランザクションでないスコープまたはオーケストレーション内に入れ子にすることはできません。  
  
-   スコープは 21 レベル分の深さまで入れ子にすることができます。  
  
-   **オーケストレーションの呼び出し**図形はスコープ内に含めることができますが、呼び出されたオーケストレーションは処理、他のと同じで入れ子にされたトランザクション、および同じ規則が適用されます。  
  
-   **オーケストレーションを開始**図形はスコープ内に含めることができます。 入れ子に関する制限事項は、開始したオーケストレーションには適用されません。  
  
## <a name="scope-variables"></a>スコープ変数  
 スコープ レベルで、メッセージ、関連付けセットなどの変数を宣言できます。 ただし; オーケストレーション変数とスコープ変数に同じ名前を使用することはできません。名前の隠ぺいすることはできません。  
  
## <a name="see-also"></a>参照  
 [トランザクションを使用して、例外の処理](../core/using-transactions-and-handling-exceptions.md)   
 [アトミック トランザクション](../core/atomic-transactions.md)