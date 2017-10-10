---
title: "ノードのプロパティを設定する方法 |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c0c79eac-d9ba-45e2-a6e9-770b2bcb2067
caps.latest.revision: "6"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 13dc0f13814808a69c4c4b9c3976e9047acde5b1
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="how-to-set-node-properties"></a>ノードのプロパティを設定する方法
BizTalk スキーマにノードを挿入した後で、そのノードのプロパティを既定値から変更することが必要になる場合があります。 ノードの種類ごとに、固有の一連のプロパティがあります。また、これらのプロパティでは、あるプロパティの設定が他のプロパティの使用に影響を与える場合もあります。 たとえば、設定する前に、**既定の囲み文字**のプロパティ、**スキーマ** ノードを設定する必要がある、**既定の囲み文字の種類**プロパティかを**文字**または**16 進**、それによって、前者のプロパティを表す形式を確立します。 さらに、これらのプロパティが使用可能なも全体は、**解析**プロパティのカテゴリが属する、しない限り、**フラット ファイル拡張子**を使用して有効になっているが、**スキーマ エディター拡張機能**プロパティです。  

 ノードのプロパティは広範にわたり、複雑です。サポートする XSD (XML Schema Definition) 言語についても同様です。 このトピックでは、ノードのプロパティの確認および設定に関する一般的な手順ついて、簡単に説明します。 これらのプロパティの詳細についてはなどに関する情報など、既定値と値を許可するを参照してください、**スキーマ プロパティのリファレンス**です。 に関する情報に直接でも詳細については、XSD の概念と要素の大半のノード プロパティを基になるの参照[Web 上の XSD](../core/xsd-resources-on-the-web.md)です。  

詳細については、これらのプロパティとスキーマ プロパティのリファレンスで[!INCLUDE[ui-guidance-developers-reference](../includes/ui-guidance-developers-reference.md)]です。

  
## <a name="examine-a-node-property-value"></a>ノードのプロパティ値を調べる  
  
1.  BizTalk エディターで、確認するプロパティを含むスキーマを開いて、そのプロパティが含まれるノードを選択します。  
  
2.  必要に応じて F4 キーを押し、[!INCLUDE[btsVStudioNoVersion](../includes/btsvstudionoversion-md.md)] のプロパティ ウィンドウを開きます。  
  
3.  必要に応じて、目的のプロパティが表示されるように [プロパティ] ウィンドウをスクロールし、値を確認します。  
  
     プロパティ ウィンドウの上部のボタンを使用して、プロパティの表示方法を、カテゴリ別でアルファベット順に、またはカテゴリに関係なく (カテゴリを表示しないで) アルファベット順に並べ替えることができます。  
  
## <a name="set-a-node-property-value"></a>ノードのプロパティ値を設定します。  
  
1.  BizTalk エディターで、設定するプロパティを含むスキーマを開いて、そのプロパティが含まれるノードを選択します。  
  
2.  必要に応じて F4 キーを押し、[!INCLUDE[btsVStudioNoVersion](../includes/btsvstudionoversion-md.md)] のプロパティ ウィンドウを開きます。  
  
3.  必要に応じて、目的のプロパティが表示されるように [プロパティ] ウィンドウをスクロールします。  
  
     プロパティ ウィンドウの上部のボタンを使用して、プロパティの表示方法を、カテゴリ別でアルファベット順に、またはカテゴリに関係なく (カテゴリを表示しないで) アルファベット順に並べ替えることができます。  
  
4.  プロパティ名の右の値フィールドに、プロパティの値を設定します。 プロパティの種類によって、値を入力する場合と、ドロップダウン リスト (値フィールドを選択すると表示される) から値を選択する場合があります。 両方の操作ができるプロパティもあります。 一部のプロパティが省略記号を表示 (**.**) ボタンをダイアログ ボックスに、コレクションなどの値が複雑なクリックされた開きますを設定することができます。  
  
5.  プロパティに新しい値を入力したら、最後に <localizedText>Enter</localizedText> キーを押します。  
  
##  <a name="clear-a-node-property-value"></a>ノード プロパティ値をクリアします。  
  
1.  目的のプロパティが含まれるノードを選択します。  
  
2.  [プロパティ] ウィンドウでオフにして、プロパティ値を右クリックし、をクリックするプロパティの値をダブルクリック**削除**です。  
  
## <a name="restore-a-node-property-to-its-default-value"></a>ノード プロパティの既定値に復元します。  
  
1.  目的のプロパティが含まれるノードを選択します。  
  
2.  [プロパティ] ウィンドウで、既定値にリセットし、をクリックするプロパティ名を右クリックし**リセット**です。  
  
## <a name="see-also"></a>参照  
 [既存のノードの操作](../core/working-with-existing-nodes.md)