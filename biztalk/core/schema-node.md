---
title: "スキーマ ノードの |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7ea02c2a-ee00-4f44-9086-83d7ac4a8832
caps.latest.revision: "7"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: dee662cb9cb6e86b85a7760daf45af832a447b5f
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="schema-node"></a>[スキーマ] ノード

## <a name="overview"></a>概要
BizTalk エディターで、スキーマ階層の最上位は常に、**スキーマ**ノードで、名前を変更することはできません。 **スキーマ**ノードに対応、**スキーマ**XML スキーマ定義 (XSD) 言語表記のスキーマ内の要素。  
  
> [!NOTE]
>  BizTalk エディターで、**スキーマ**ノードは、文字列で表される\<スキーマ > スキーマ ツリー ビューでします。  
  
 一般のプロパティ、**スキーマ**の属性に対応しているノード、**スキーマ**スキーマの XSD 表記内の要素。 ノードのプロパティに関する概要については、次を参照してください。[ノードのプロパティ](../core/node-properties.md)です。 プロパティに関するリファレンス情報について、**スキーマ** ノードを参照してください、**スキーマ ノードのプロパティ**[!INCLUDE[ui-guidance-developers-reference](../includes/ui-guidance-developers-reference.md)]です。
  
 BizTalk エディターで、新しい XML スキーマを作成するときに、**スキーマ**ノードおよび**ルート**ノードが自動的に作成されます。  
  
## <a name="xsd-representation"></a>XSD 表記  
 例を次に、太字に対応するスキーマの XSD 表記内の行で、 **\<スキーマ >**スキーマのツリー ビュー内のノードです。  
  
```  
<?xml version="1.0" encoding="utf-16" ?>  
<xs:schema xmlns="http://BizTalk_Server_Project1.Schema2"  
    xmlns:b="http://schemas.microsoft.com/BizTalk/2003"  
    targetNamespace="http://BizTalk_Server_Project1.Schema2"  
    xmlns:xs="http://www.w3.org/2001/XMLSchema">  
    <xs:element name="Root">  
        <xs:complexType />  
    </xs:element>  
</xs:schema>  
```  
  
## <a name="see-also"></a>参照  
 [スキーマの BizTalk 表記](../core/biztalk-representation-of-schemas.md)   
 [ノードのプロパティ](../core/node-properties.md)   
 [ノードのプロパティを設定します。](../core/how-to-set-node-properties.md)