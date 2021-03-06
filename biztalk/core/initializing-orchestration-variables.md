---
title: オーケストレーション変数の初期化 |Microsoft ドキュメント
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- orchestrations, variables
ms.assetid: 770e4e55-1fb9-4b43-854c-63aec5a3c5ba
caps.latest.revision: 8
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: a90fbc33343e3576d6199a0a97a7a57ca881f720
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
ms.locfileid: "22256826"
---
# <a name="initializing-orchestration-variables"></a>オーケストレーション変数の初期化
変数の値は、[プロパティ] ウィンドウで設定することによって初期化できます。 たとえば、設定、**初期値**System.Int32 型の変数を初期化するために 32 です。 文字列型の値に初期値を追加するときは、プロパティ ウィンドウで初期値を引用符で囲む必要があります。 文字列に引用符を含める場合は円記号をエスケープ文字として使用し、文字列にリテラル円記号を含める場合は連続する円記号を使用します。 場合は、変数の値を指定しないと、変数は既定値を割り当てる、オーケストレーションのインスタンスを作成するとすぐにします。  
  
 変数がクラスのインスタンスである場合は、コンストラクターを指定して初期化できます。 既定では、**既定コンス トラクターを使用**プロパティに設定されている**True**場合、既定のコンス トラクターは使用できません。 したがって、既定のコンス トラクターが呼び出されます。 既定のコンス トラクターを使用する場合で改めて変数を初期化する必要はありません、**式**図形を 2 回、コンス トラクターの呼び出しを回避します。 場合、**既定のコンス トラクターを使用して**プロパティに設定されている**False**既定のコンス トラクターは呼び出されません以外の場合は、式でコンス トラクターを呼び出すまたは使用する前に、変数に割り当てを作成する必要がありますで、オーケストレーションです。 さらに、コンス トラクターは、入力パラメーターを必要とする場合は、設定する必要あります**既定のコンス トラクターを使用**に**False**からコンス トラクターを呼び出すと、**式**図形の例では、`myVariable = myNamespace.myClass (param1, param2)`です。  
  
 変数を明示的に初期化する必要が唯一の状況は、オーケストレーションに複数のアクティブ化が含まれている受信で利用できるよう、**スコープ**、**並列アクション**、または**リッスン**図形です。 この場合、自動初期化が無効になり、使用する必要があります、**式**図形、変数を初期化します。 配置する必要があります、**式**図形のそれぞれのアクティブ化されたら、および任意の変数には、オーケストレーションでアクセスする前にします。