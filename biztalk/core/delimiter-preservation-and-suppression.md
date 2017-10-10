---
title: "区切り記号の保存と抑制 |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 30985b94-625e-411a-8137-1c129bc197bf
caps.latest.revision: "8"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 1195e153eb94215bf8861b4856e4d2135b24443e
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="delimiter-preservation-and-suppression"></a>区切り記号の保存および非表示

## <a name="overview"></a>概要
区切られたレコードに適用される 2 つのプロパティ:**空のデータの区切り記号を保持する**と**[末尾の区切り記号の抑制**です。 これらのプロパティを使用すると、フラット ファイル アセンブラーが存在しないデータと末尾の区切り記号に関連付けられている区切り記号を処理する方法を制御できます。 設定すると、**空のデータの区切り記号を保持する**プロパティを**はい**(既定の設定は)、変換されたフラット ファイル メッセージ内の区切り記号が含まれています。  
  
-   データを含んでいないフィールド。  
  
-   関連付けられたタグを持たず、データを含んでいない直下のレコード。  
  
 設定すると、**空のデータの区切り記号を保持する**プロパティを**いいえ**、区切り記号は、レコードおよびフィールドがデータなしの変換されたフラット ファイルには含まれません。 さらの設定に関係なく、**空のデータの区切り記号を保持する**プロパティ、タグが定義されているデータなしの直下のレコードに変換されたフラット ファイル メッセージ内の区切り記号は含まれません。  
  
 設定すると、**末尾の区切り記号の非表示**プロパティを**なし**(既定の設定は)、変換されたフラット ファイル メッセージに 1 つまたは複数の末尾の区切り記号を含めることがあります。 設定すると、**末尾の区切り記号の非表示**プロパティを**はい**、末尾の区切り記号は、変換されたフラット ファイル メッセージに含まれません。  

## <a name="special-scenarios"></a>特殊なシナリオ  
 設定で、動作が原因となった特殊なケースがある、**空のデータの区切り記号を保持する**と**末尾の区切り記号の抑制する状況**プロパティが競合することをがします。 このような場合、後者のプロパティに関連付けられている動作**末尾の区切り記号の抑制**が優先されます。 また、これら 2 つのプロパティの設定によって競合が発生する可能性が高いと予測される状況もあります。  
  
 たとえば、**レコード**次のプロパティ値で定義されたノード。  
  
-   ノード名が MyRec である。  
  
-   タグ識別子が Rec である。  
  
-   子の区切り記号が , である。  
  
-   子の順序が挿入辞である。  
  
 5 つ含むに定義されていると**フィールド要素**ノードで次の名前 (も**フィールド属性**ノードまたは下位**レコード**ノード)。  
  
-   FieldElem1  
  
-   FieldElem2  
  
-   FieldElem3  
  
-   FieldElem4  
  
-   FieldElem5  
  
 次の主に空のこれを表す XML フラグメントを次に、想定**レコード**ノードは、フラット ファイル アセンブラーに渡されます。  
  
```  
<MyRec>  
    <FieldElem1 />  
    <FieldElem2 />  
    <FieldElem3>Val</FieldElem3>  
    <FieldElem4 />  
    <FieldElem5 />  
</MyRec>  
  
```  
  
 次の表は、生成される出力と、関連付けられている追加のプロパティの設定に異なる設定に基づいて、関連するスキーマ ノードの要件、**空のデータの区切り記号を保持する**(PDFED) および**末尾の区切り記号の抑制**(STD) プロパティです。  
  
|PDFED 設定|STD 設定|出力|追加のノード要件|  
|---|---|---|---|  
|はい|不可|Rec,,,Val,,|[なし] :|  
|不可|はい|Rec,Val|すべて**フィールド要素**ノードは省略可能として構成する必要があります。|  
|はい|はい|Rec,,,Val|という名前のノード**FieldElem4**と**FieldElem5**オプションとして構成する必要があります。|  
|不可|不可|Rec,Val,,|すべて**フィールド要素**ノードは省略可能として構成する必要があります。|  
  
 これらのプロパティ設定で、区切り記号が保存されない設定、または区切り記号を非表示にする設定を行うと、同じスキーマを使用してシリアル化したフラット ファイル データを解析できないという警告を示すメッセージが、次の場合に表示されます。  
  
-   ときに、**レコード**対象のノード、**空のデータの区切り記号を保持する**プロパティに設定されている**いいえ**と**抑制末尾の区切り記号**プロパティに設定されている**はい**、それぞれ、下位が含まれています**フィールド要素**ノード、**フィールド属性**ノード、または**レコード**のタグが指定されていないノードです。  
  
-   ときに、下位**フィールド要素**ノード、**フィールド属性**ノード、および**レコード**のタグが指定されていないノードが省略可能な場合に構成されていません (設定して、**Min Occurs**プロパティを 0 に設定)、スキーマにします。 ときに、**末尾の区切り記号の抑制**プロパティに設定されている**[はい]**最後にのみを構成する必要がこのような下位ノードが省略可能として。 ときに、**空のデータの区切り記号を保持する**プロパティに設定されている**なし**、すべての末尾を構成する必要が下位ノードが省略可能として。  
  
> [!NOTE]
>  XML 要素は、(おそらく省略可能) に関連付けられているときに区切り記号は常に保持**レコード**、**フィールド要素**、または**フィールド属性**ノードがまったくないです。レコードが省略可能なフィールドがありませんに依存する場合を除く、ビジネス ドキュメントの XML 表現。 つまり、データとデータを囲む XML タグが両方とも欠落している場合、対応する区切り記号は、ビジネス ドキュメントのフラット ファイル表記に必ず含まれます。  
  
 ここで、欠落した [フィールド要素] の直後に 2 つの [フィールド要素] を持つ子レコードを含むようにスキーマを変更します。 使用する子レコード要素が構成されている、& #124 です。(パイプ) 文字を区切り文字として。  
  
```  
<MyRec>  
    <FieldElem1 />  
    <FieldElem2 />  
    <FieldElem3>Val</FieldElem3>  
    <!-- <FieldElem4 /> -->  
    <ChildRec>  
        <InnerFieldElement1>Inner1</InnerFieldElement1>   
        <InnerFieldElement2>Inner2</InnerFieldElement1>  
    </ChildRec>  
    <FieldElem5 />  
</MyRec>  
  
```  
  
 このデータがフラット ファイル逆アセンブラーに渡されると、FieldElem4 の区切り記号は保存されませんが、その後のレコードは正常に区切られます。  
  
```  
,,Val,,Inner1,Inner2,,  
```  
  
## <a name="see-also"></a>参照  
-  [区切り記号付きレコードに関する注意点](../core/delimited-record-considerations.md)   
-  **空のデータ (フラット ファイル スキーマのノード プロパティ) の区切り記号の保存**と**末尾の区切り記号 (フラット ファイル スキーマのノード プロパティ) を抑制する**[!INCLUDE[ui-guidance-developers-reference](../includes/ui-guidance-developers-reference.md)]