---
title: "コードの一覧の管理 |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a924c814-d077-4aea-bacb-bf2e8a3dee01
caps.latest.revision: "6"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 13b98fac659c30d1e8e6da50689fc2086d090be4
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="code-list-management"></a>コード リストの管理

## <a name="overview"></a>概要
XSD を使用すると、要素または属性に対して使用できる特定の有効な値を指定できます。 この機能は、使用可能なを使用して、**列挙**要素。 データ型を継承する場合、**フィールド要素**または**フィールド属性**ノードで利用可能になるプロパティのいずれかの制限によって、**制限**カテゴリは、**列挙**プロパティです。 このプロパティを使用して、開くことができます、**列挙エディター**  ダイアログ ボックスの対応する要素または属性がインスタンス メッセージ内の有効と見なされる必要があります、値を入力できます。  
  
 Microsoft BizTalk Server には、スキーマにおける列挙を管理するためのもう 1 つの方法として、コード リストという便利な機能が用意されています。 コード リストは、Microsoft Access データベースを使って各種の選択肢 (列挙値) を格納することにより一元的な管理を実現します。 さらを使用して入力する必要があります、直感的でない数値コードの場合は、列挙値を使用する必要があります、**列挙**プロパティ、コードの一覧で使用する Access データベースを作成するテーブル機能には、これらの数値のテキストの説明が含まれます。 テキストの説明についてで使用される、 **CodeList**にくいではなく、ダイアログ ボックスは、同等の数値がわかりにくくなります。  

## <a name="use-the-code-list"></a>コード リストを使用します。  
 コード リスト機能を使用するには、以下に示す手順に従ってください。  
  
-   Access データベースと適切な名前のテーブル (および必要な列) を作成し、値を格納する必要があります。  
  
    -   テーブルの名前は、の組み合わせ、**標準**と**標準バージョン**のプロパティ、**スキーマ**ノード、アンダー スコア (_) 文字で区切られます。 たとえば、設定した場合、**標準**のプロパティ、**スキーマ**xml ノードと**標準バージョン**プロパティが MyVersion1、によって指定される Access データベース、**CodeList データベース**プロパティは、XML_MyVersion1 という名前のテーブルを持つ必要があります。  
  
        これらのプロパティの詳細について[!INCLUDE[ui-guidance-developers-reference](../includes/ui-guidance-developers-reference.md)]です。

    -   このテーブルは、3 つの列 (Code、Value、Desc など) で構成します。最初の列を各行を提供して、選択した場合に対応するデータの許可される可能性がある可能性があります、列挙のいずれか、相互に関連する行を識別**フィールド要素**または**Field 属性**ノード。 最初の列の値が同じになっている行はすべて、グループとしてまとめられます。 通常、これらの値には整数が使用されますが、スペースが含まれていなければ文字列を使用することもできます。  
  
         各行の 2 番目と 3 番目の列には、それぞれ、列挙値に対応する値とテキスト表現を格納します。  
  
         たとえば、次の Access データベース テーブルには、関連する 3 つの列挙値が 2 セット含まれています。 最初の列の値は、行の関連付けに使用されるもので、任意の値を使用できます。  
  
        |コード|値|Desc|  
        |----------|-----------|----------|  
        |1|13|[赤]|  
        |1|16|[緑]|  
        |1|19|[青]|  
        |2|1|小|  
        |2|2|Medium|  
        |2|3|大|  
  
-   3 つのプロパティを適切に構成する必要があります、**スキーマ**ノード。  
  
    -   **CodeList データベース**プロパティは、作成した Access データベースの名前に設定する必要があります。  
  
    -   **標準**と**標準バージョン**区切りアンダー スコア (_) 文字と組み合わせたときは、ときに、適切な内のテーブルの指定した名前を形成するようにプロパティを設定する必要がありますAccess データベース。  
  
-   実際に選択されている、特定の Access データベース内の値の使用**フィールド要素**または**フィールド属性**ノード、2 つのプロパティを構成する必要があります。  
  
    -   設定する必要があります、 **Derived By**プロパティを**制限**です。 その他のプロパティを構成する必要があります**CodeList**、この手順を実行するまで有効になりません。  
  
    -   値を入力する必要があります、 **CodeList**最初の列の値に対応するプロパティ (、**コード**列) の指定したデータベース内の 1 つまたは複数の行。 このアクションが、選択した対応する列挙値のセットを識別する**フィールド要素**または**フィールド属性**ノード。  
  
         省略記号ボタンをクリックする必要があります (**.**) の右側にある、 **CodeList**を開くにはプロパティの値フィールド、 **CodeList**  ダイアログ ボックス。 このダイアログ ボックスで、チェック ボックスを使用して、選択した場合に対応するインスタンス メッセージ データの有効な値として許可する値を選択**フィールド要素**または**フィールド属性**ノード。 選択できるのは、使用可能な値のサブセットだけです。 たとえば、上のテーブルの例に値 1 を入力する場合、 **CodeList** 、プロパティ、 **CodeList**  ダイアログ ボックスには、赤、緑、および青の選択肢にが含まれます。 赤と緑のチェック ボックスをオンにして青のチェック ボックスを選択しない場合でも、以前の色だけは、選択した有効な値として XSD に表示されます**フィールド要素**または**フィールド属性**ノード。  
  
> [!NOTE]
>  **CodeList**と**CodeList データベース**プロパティとデザイン時にのみ使用されますが、対応する設定として、XSD に保持されます、**列挙**プロパティです。 に対して、実行時にすべての値の検証、**列挙**プロパティのみです。  
  
> [!CAUTION]
>  指定された**フィールド要素**または**フィールド属性**ノード、両方は使用しないでください、**列挙**プロパティおよび**CodeList**プロパティです。 2 つのプロパティを同時に使用した場合、最初に入力したプロパティ値が、最後に入力したプロパティ値によって上書きされます。  
  
## <a name="see-also"></a>参照  
 [スキーマを作成する際の考慮事項](../core/considerations-when-creating-schemas.md)