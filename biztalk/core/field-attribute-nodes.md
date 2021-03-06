---
title: フィールド属性 ノード |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9e964c07-53e5-473f-84f2-05af4796cbbe
caps.latest.revision: 7
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: ef3cbf401ce5408c59ae164ca528c41a647eba2f
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36972141"
---
# <a name="field-attribute-nodes"></a>[フィールド属性] ノード

## <a name="overview"></a>概要
BizTalk エディターを使用する**フィールド属性**ノードは、単純な文字列や数値などの情報項目を表すため。 また、このノードは、目的の情報が、XML 要素の内容としてではなく、実際のメッセージ インスタンスに属性の値として現れる場合に使用されます。 要素の内容として格納されている情報の詳細については、次を参照してください。[フィールド要素 ノード](../core/field-element-nodes.md)します。  

 最も基本的な用途の**フィールド属性**の子ノードとしてノードの場合は**レコード**、ノードの子ノードとしても使用**属性グループ**ノード。 後者の場合、**フィールド属性**ノードの子である、**属性グループ**ノードは、いずれかの属性として使用**レコード**そのを含むノード**属性グループ**ノード。 詳細については**属性グループ**ノードを参照してください[属性グループ ノード](../core/attribute-group-nodes.md)します。  

> [!NOTE]
>  BizTalk エディターでは、要素と属性要素の両方で表現できる、**フィールド**ノードがスキーマ ツリー ビューで、XSD ウィンドウにおける XML 表記で、それらに関連付けられている別のアイコン、およびVisual Studio のプロパティ ウィンドウでさまざまなプロパティ。  

 XML メッセージに含まれる特定の情報項目 (ここでいう情報項目とは、文字列や数値など、1 つの独立した単純型のこと) では、その情報を要素の属性として表すべきか、要素のサブ要素として表すべきかという問題があります。 一般に、格納される値が不連続であり、数が少なく、要素そのもののセマンティクスが変わりやすい場合は、情報項目を属性として表します。 同じ値が繰り返し出現する場合、取りうる値の範囲が大きい場合、(文字列などが) 長くなってしまう場合、順序に関連性のある複数の兄弟値のいずれかが格納される場合などは、情報項目をサブ要素として表した方が適切な結果が得られる傾向があります。 既存の XML の種類のスキーマを作成する場合を文書化を使用して選択した、**フィールド要素**ノードまたは**フィールド属性**特定の情報項目のノードは既に行われましたとXML に一致するノードを使用する必要があります。  

> [!NOTE]
>  ルート ノードがない可能性があります**フィールド**属性。 **フィールド**にアタッチされている属性、**ルート**ノードは、スキーマには保存されません。  

## <a name="xsd-representation"></a>XSD 表記  
 ときに、**フィールド属性**ノードの挿入、**レコード**ノードで他の子ノードの最後に挿入されます、**レコード**ノード。 これは、後に挿入されているが含まれています、**シーケンス**、**選択肢**、または**すべて**要素、属性ノードを含む前後にあったすべての属性ノード。挿入されます。 次の例は、新しい**フィールド属性**太字内のノードの最後に挿入された、**レコード**ノード (ノードが自身の id を明確にするという名前) が使用します。  

```  
<xs:element name="ContainingRecord">  
    <xs:complexType>  
        <xs:sequence>  
            <xs:element name="FieldElement" type="xs:string" />  
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
- [[属性グループ] ノード](../core/attribute-group-nodes.md)
