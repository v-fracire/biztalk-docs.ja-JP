---
title: フィールド要素 ノード |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 65b5e1f6-283f-4172-9bc2-f04a0ea6753d
caps.latest.revision: 7
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 6c06a3f2fd55dc720fd0d37beaea49de76cbf101
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "37004227"
---
# <a name="field-element-nodes"></a>[フィールド要素] ノード

## <a name="overview"></a>概要
BizTalk エディターを使用する**フィールド要素**ノードは、単純な文字列や数値などの情報項目を表すため。 また、このノードは、目的の情報が XML 要素に関連付けられた属性の値としてではなく、実際のメッセージ インスタンスに XML 要素の内容として現れる場合に使用されます。 属性値として格納されている情報の詳細については、次を参照してください。[フィールド属性 ノード](../core/field-attribute-nodes.md)します。  

> [!NOTE]
>  BizTalk エディターでは、要素と属性要素の両方で表現できる、**フィールド**ノードが、スキーマ ツリー ビューで、XSD ウィンドウにおける XML 表記で、それらに関連付けられている別のアイコン、およびVisual Studio のプロパティ ウィンドウでさまざまなプロパティ。  

 XML メッセージに含まれる特定の情報項目 (ここでいう情報項目とは、文字列や数値など、1 つの独立した単純型のこと) では、その情報を要素の属性として表すべきか、要素のサブ要素として表すべきかという問題があります。 一般に、格納される値が不連続であり、数が少なく、要素そのもののセマンティクスが変わりやすい場合は、情報項目を属性として表します。 同じ値が繰り返し出現する場合、取りうる値の範囲が大きい場合、(文字列などが) 長くなってしまう場合、順序に関連性のある複数の兄弟値のいずれかが格納される場合などは、情報項目をサブ要素として表した方が適切な結果が得られる傾向があります。 既存の XML の種類のスキーマを作成するだけの場合を文書化を使用して選択した、**フィールド要素**ノードまたは**フィールド属性**特定の情報項目のノードは既に行われましたXML に一致するノードを使用する必要があります。  

## <a name="xsd-representation"></a>XSD 表記  
 ときに、**フィールド要素**ノードの挿入、**レコード**ノード内の他の子ノードの最後に挿入されます、**シーケンス**内の要素、 **レコード**ノード。 次の例は、新しい**フィールド要素**太字内のノードの最後に挿入された、**シーケンス**内の要素を**レコード**(自分の id を明確にするという名前のノードを持つノード).  

```  
<xs:element name="ContainingRecord">  
    <xs:complexType>  
        <xs:sequence>  
            <xs:element name="ExistingFieldElement" type="xs:string" />  
            <xs:element name="EmptyNestedRecord">  
                <xs:complexType />  
            </xs:element>  

        </xs:sequence>  
        <xs:attribute name="ExistingFieldAttribute" type="xs:string" />  
    </xs:complexType>  
</xs:element>  

```  

## <a name="see-also"></a>参照  
- [スキーマの BizTalk 表記](../core/biztalk-representation-of-schemas.md)   
- [ノードのプロパティ](../core/node-properties.md)   
- **[フィールド要素] ノード プロパティ** [!INCLUDE[ui-guidance-developers-reference](../includes/ui-guidance-developers-reference.md)]
- [ノードのプロパティを設定する方法](../core/how-to-set-node-properties.md)
