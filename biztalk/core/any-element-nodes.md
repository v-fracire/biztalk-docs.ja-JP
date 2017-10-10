---
title: "すべての要素ノード |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c7e30fcf-31bc-4d48-9bc7-0be90e927127
caps.latest.revision: "7"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: c24eb75020f715245fc2b17f4bc1f81a7e34cd35
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="any-element-nodes"></a>すべての要素ノード
BizTalk エディターで行うこともできます、 **Any 要素**不明な要素が表示されるインスタンス メッセージ内の場所を示すためにノードです。 これにより、特定の要素がインスタンス メッセージ内の特定の場所に出現することはあらかじめわかっているが、要素の名前や複雑さの程度が不確定な状況にも対応できます。 配置した場合、 **Any 要素**ノードのスキーマでは、BizTalk 内で適切な位置には、このようなメッセージの不明な部分を処理できます。 唯一の要件は、対応する XML が整形式であることです。  
  
> [!NOTE]
>  BizTalk エディターで、 **Any 要素**ノードは、文字列で表されます\<任意 > スキーマ ツリー ビューでします。  
  
> [!NOTE]
>  整形式 XML としてメッセージの未知の部分を検証を使用して内容を制御できます、 **Process Contents**プロパティです。 多くの場合を設定する必要があります、 **Process Contents**プロパティを**Skip**の場所にあるインスタンス メッセージの内容を**Any 要素**に処理するノードです。 既定値を保持**Strict**の**Process Contents**プロパティは、インスタンス メッセージの検証の成功をできなくなります。  
> 
> このプロパティの詳細について[!INCLUDE[ui-guidance-developers-reference](../includes/ui-guidance-developers-reference.md)]です。
  
## <a name="xsd-representation"></a>XSD 表記  
 ときに、 **Any 要素**ノードに追加された、**レコード**ノード、または別のノードを追加するように、**シーケンス グループ**、**選択肢グループ**、または**すべてのグループ**ノード、1 つの XML タグが、対応する XML スキーマ定義 (XSD) 言語表記のスキーマに追加します。 次の例では、新しい**Any 要素**を既存の XSD 表記が太字で示すように、ノードが追加されました**レコード**ノードが格納されている、**フィールド要素**ノード。  
  
```  
<xs:element name="ExistingRecord">  
    <xs:complexType>  
        <xs:sequence>  
             <xs:element name="ExistingFieldElement" type="xs:string" />  
            <xs:any />  
        </xs:sequence>  
    </xs:complexType>  
</xs:element>  
```  
  
 想定されるので、 **Process Contents**のプロパティ、**すべての要素**に設定されているノード**Skip**内でこのスキーマ フラグメントで、によって管理されるインスタンスメッセージ**ExistingRecord**要素が通常含まれる、 **ExistingFieldElement**任意の複雑性の任意の 1 つの要素の後に文字列データを含む要素です。  
  
## <a name="see-also"></a>参照  
 [スキーマの BizTalk 表記](../core/biztalk-representation-of-schemas.md)   
 [ノードのプロパティ](../core/node-properties.md)   
 [ノードのプロパティを設定する方法](../core/how-to-set-node-properties.md)   
 [任意の属性ノード](../core/any-attribute-nodes.md)