---
title: ファクト作成コンポーネントを作成する方法 |Microsoft ドキュメント
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- GetFactTypes method
- CreateFacts method
- IFactCreator interface
- Business Rules Framework, code samples
- Business Rules Framework, fact creator
- Business Rules Framework, programming
ms.assetid: 0589be8e-34d6-4e55-b678-c1f8436d1f61
caps.latest.revision: 7
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 5cba9c46a147d912ae22644a30ef65c0b0213202
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
ms.locfileid: "22248666"
---
# <a name="how-to-create-a-fact-creator"></a>ファクト作成コンポーネントを作成する方法
ファクト作成コンポーネントを記述して、ファクトのインスタンスを作成できます。 ファクト作成コンポーネントを実装する必要があります**IFactCreator**とその**CreateFacts**メソッドおよび**GetFactTypes**メソッドです。 ファクト作成コンポーネントの dll を作成すると、ポリシー テスター内から参照できます。 次に、ファクト作成コンポーネントの実装例を示します。  
  
```  
public class MyFactCreator : IFactCreator  
{  
   private object[] myFacts;  
   public MyFactCreator()  
   {  
   }  
   public object[] CreateFacts ( RuleSetInfo rulesetInfo )  
   {  
      myFacts = new object[1];  
      myFacts.SetValue(new MySampleBusinessObject(),0);  
      return myFacts;  
   }  
   public Type[] GetFactTypes (RuleSetInfo rulesetInfo)  
   {  
      return null;  
   }  
}  
```