---
title: "SWIFT テキスト |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: SWIFT, text
ms.assetid: 90851d38-7789-4b1b-813b-7943f77ab984
caps.latest.revision: "3"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: c80d8ee0343cbf8ac96d57119ef198d623159b26
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="swift-text"></a>SWIFT テキスト
メッセージ テキスト、財務 (FIN) メッセージのペイロードとすべての送信者、受信者、およびメッセージの種類を含むフィールドを除くデータ フィールドが含まれています。 これら 3 つのフィールドは、ヘッダー部分に含まれます。 一部のメッセージには、処理情報も提供する、オプションのユーザー ヘッダーも含まれます。  
  
 各 FIN メッセージ ペイロードは、一連のフィールドに定義されたシーケンス内で構成されます。 これらのフィールドは、次の規則に従います。  
  
-   フィールドには、必須または、シーケンス内でオプションがあります。  
  
-   シーケンスは、のサブシーケンスを含めることができ、サブシーケンスがシーケンス内で繰り返す必要があります。  
  
-   いくつかのメッセージ型のフィールドを使用することができます。  
  
-   フィールドの内部に、要素またはサブフィールドが可能性があります。 要素またはサブフィールドをいくつかのフィールドに一般的な可能性があります。  
  
-   各繰り返しシーケンスは、グループ ノードで表されます。  
  
-   各フィールド自体があります、複数の節レベル レコードとして各説明します。  
  
-   スキーマ要素は、最下位レベルのサブフィールドのみを表します。  
  
-   共通のレコードと要素は、以下に示すよう共通および基本のスキーマで定義されます。  
  
-   一部のフィールドは、(パーティ フィールドなど) のいくつかの形式で表すことができます。 このようなフィールドは、スキーマの選択フィールドとして定義されます。  
  
 一部のフィールドには、値のセットが制限されます。 ほとんどの場合、スキーマには、これらの値が一覧表示します。 スキーマ定義には、文字セットの検証も含まれます。