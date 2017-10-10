---
title: "関連付けセット |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- correlation sets, inspecting
- correlation sets, about correlation sets
- correlation sets, passing as parameters
- messages, correlation sets
- correlation sets
- correlation sets, following correlation sets
- correlation sets, initializing
ms.assetid: 528dcd6c-d364-4bb8-8deb-cd4a0791867f
caps.latest.revision: "11"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 28d11e5e174808ca7718d5fef98b3ad079cffc18
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="correlation-sets"></a>関連付けセット
関連付けセットを定義することによって、オーケストレーション インスタンスを使用して、このようなメッセージの関連付けを行うことができます。 関連付けセットは、一連のプロパティ*値を指定して*です。 これは、単なるプロパティの一覧である関連付けの種類とは異なります。 受信メッセージがそれぞれに一致する値を持つこれらのプロパティの一部を持っていない場合は、関連付けは失敗し、オーケストレーション インスタンスはメッセージを受信しません。  
  
 関連付けセットは、メッセージを関連付けるプロパティのセットを定義します。 これらは、プロパティ スキーマで前に定義された任意のプロパティにすることができ、BizTalk の基本インストールの一部としてインストールされる GlobalPropertySchemas と共に展開された "システム" のプロパティを含む一部の BizTalk プロジェクトを使用して展開できます。 関連付けセットでは、メッセージが特定のオーケストレーションでの処理対象となるために、メッセージに含まれている必要がある一連のプロパティとその値を定義します。  
  
 たとえば、関連付けの種類は、次のプロパティで構成される可能性が考えられます。  
  
|関連付けの種類のプロパティ|使用可能な XML 表記|  
|-------------------------------|---------------------------------|  
|社会保障番号|\<SSN >\</SSN >|  
|誕生日|\<DOB >\</DOB >|  
|Gender|\<性別 >\<性別/>|  
  
 この関連付けの種類から派生した関連付けセットは、次のプロパティと値で構成される可能性が考えられます。  
  
|関連付けセットのプロパティおよび値|可能な XML 表現|  
|-------------------------------------|---------------------------------|  
|社会保障番号 = 222112222|\<SSN > 222112222\</SSN >|  
|誕生日 = “1/1/1995”|\<DOB >「1/1/1995」\</DOB >|  
|性別 = 男性|\<性別 > M\<性別/>|  
  
> [!NOTE]
>  各関連付けセットは最大 3 つのパラメーターをサポートします。  
  
## <a name="initializing-correlation-sets"></a>イニシャライズ関連付けセット  
  
-   **受信アクションで初期化される関連付けセット**  
  
     受信アクションで初期化される関連付けセットは、オーケストレーションの対応する受信アクションによって処理されるように、公開されたメッセージに存在する必要がある正確なプロパティのセットだけを定義します。 関連付けセットの初期化によって、ドキュメント内の対応する値に基づいて関連付けの種類から関連付けセットが作成されます。  
  
-   **送信アクションで初期化される関連付けセット**  
  
     送信アクションで初期化される関連付けセットは、ドキュメント内の対応する値に基づいて関連付けの種類から作成され、送信ドキュメント内の関連付けのプロパティを昇格させます。  
  
## <a name="following-correlation-sets"></a>フォロー関連付けセット  
 フォロー関連付けセットは、非アクティブ化受信アクションまたは送信アクションだけに対してバインドできます。 フォロー関連付けセットは、前に初期化された関連付けセットと共に指定されます。  
  
-   **受信アクションにバインドされたフォロー関連付けセット**  
  
     受信アクションにバインドされているフォロー関連付けセットは、ドキュメントが受信されるためにそのドキュメントに含める必要があるプロパティと値のセットを定義します。  フォロー関連付けセットを持つ受信アクションは、前に初期化された関連付けセットからのプロパティを含むドキュメントを受け入れます。  
  
-   **送信アクションにバインドされたフォロー関連付けセット**  
  
     送信アクションにバインドされているフォロー関連付けセットは、関連付けセットのプロパティのセットが送信ドキュメントで昇格されることを指示します。  
  
## <a name="inspecting-correlation-sets"></a>関連付けセットの調査  
 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] では、関連付けセットを調査する機能が提供されます。 次のようなコードを使用して、式図形の関連付けセットを調査できます。  
  
```  
MsgLen = Correlation_1(BTS.MessageLength);  
```  
  
 上記の例は、という名前の変数を作成している前提としています**MsgLen**型の**System.Int16** 、オーケストレーションに相関関係が含まれているとは、名前付きセット**Correlation_1**。. 関連付けセットを調査する機能は、別のオーケストレーションによってオーケストレーションに渡された関連付けの値を調査する必要がある場合に、役立つことがあります。  
  
## <a name="passing-correlation-sets-as-parameters-to-orchestrations"></a>オーケストレーションにパラメーターとして関連付けセットを渡す  
 相関関係を渡すことができます*で*他のオーケストレーションへのパラメーターです。