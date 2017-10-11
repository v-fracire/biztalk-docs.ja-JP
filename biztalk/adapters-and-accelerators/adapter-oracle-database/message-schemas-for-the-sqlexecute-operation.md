---
title: "SQLEXECUTE 操作のメッセージ スキーマ |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: SQLEXECUTE operations, message schemas for
ms.assetid: 744645f4-0674-44e0-bf8d-8df70086b0f1
caps.latest.revision: "2"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 8c0ee3d0905f5ee4205cb5f9e2357573bdbf55b4
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="message-schemas-for-the-sqlexecute-operation"></a>SQLEXECUTE 操作のメッセージ スキーマ
[!INCLUDE[adapteroracle](../../includes/adapteroracle-md.md)]LOB システムに存在成果物のための厳密に型指定されたメタデータを表示し、これらの成果物の標準的な操作を公開します。 ただし、アプリケーションがアプリケーションにビジネス ロジックによって駆動される任意の SQL ステートメントの実行を必要がありますのシナリオがあります。 たとえばをする可能性があります。  
  
-   表示されませんがデータベースのアイテムに対して操作を実行、 [!INCLUDE[adapteroracle_short](../../includes/adapteroracle-short-md.md)]。 たとえば、CURVAL または Oracle シーケンスの NEXTVAL を取得します。  
  
-   データ定義言語の操作です。たとえば、テーブルを作成します。  
  
-   デザイン時に存在しませんでした、データベースの成果物の操作を実行します。たとえば、ビジネス ロジックによって作成される一時テーブル内のレコードを更新します。  
  
-   によって表示される演算よりもテーブルでより複雑な DML 操作を実行、 [!INCLUDE[adapteroracle_short](../../includes/adapteroracle-short-md.md)]; の例は、結合句を含むクエリを実行します。  
  
 [!INCLUDE[adapteroracle_short](../../includes/adapteroracle-short-md.md)]サーフェスのようなシナリオをサポートするために、SQLEXECUTE 操作と呼ばれる特別な操作です。 この操作を使用するの任意の SQL ステートメントを指定することができます、 [!INCLUDE[adapteroracle_short](../../includes/adapteroracle-short-md.md)] Oracle データベースで実行します。 SQL ステートメントに渡す入力パラメーターの複数のブロックを指定することもできます。 [!INCLUDE[adapteroracle_short](../../includes/adapteroracle-short-md.md)]パラメーターのセットごとに、SQL ステートメントを実行し、汎用的な (弱い型指定) のレコード セットとして出力を返します。  
  
> [!NOTE]
>  IN を渡すことができ、プロシージャ、関数、および SQLEXECUTE 操作内のパッケージに IN OUT パラメーターです。 Oracle データベースで指定されたパラメーターで呼び出された成果物が実行されます。ただし、SQLEXECUTE 操作返さない外の値と、クライアントに IN OUT パラメーターです。 設定するように、専用の操作を呼び出すことによってプロシージャ、関数、またはパッケージを起動する場合は、Microsoft にお勧めする、[!INCLUDE[adapteroracle_short](../../includes/adapteroracle-short-md.md)]これら Oracle の成果物用に公開します。  
  
 次の XML は、SQLEXECUTE 操作の構造を示しています。  
  
```  
<SQLEXECUTE xmlns="SQLEXECUTE">  
  <SQLSTATEMENT> [STATEMENT] </SQLSTATEMENT>  
  <PARAMETERSCHEMA>[PARAM_SPEC]</PARAMETERSCHEMA>  
  <PARAMETERSET>  
    <PARAMETERDATA>  
      <PARAMETER xmlns:c="http://schemas.microsoft.com/2003/10/Serialization/Arrays">  
        <c:string>[PARAM_VAL_1]</c:string>  
      </PARAMETER>  
    </PARAMETERDATA>  
    …  
  </PARAMETERSET>  
</SQLEXECUTE>  
```  
  
 [ステートメント] = SQL ステートメントを実行します。たとえば、"選択 * emp から WHERE empno =: emp_no"です。  
  
 [PARAM_SPEC] で、SQL ステートメントとそのデータ型は IN パラメーターの一覧を =たとえば、"emp_no 数"です。  
  
 [PARAM_VAL_1] の最初のパラメーターの値を = です。  
  
 各\<PARAMETERDATA > セクションには、完全なセットが含まれています。\<パラメーター > 内のスキーマに一致する要素、 \<PARAMETERSCHEMA > セクションでします。 \<PARAMETERSET > 複数を含めることができる\<PARAMETERDATA > セクションでします。 これは、大文字と小文字、SQL ステートメントが各パラメーター セットに対して 1 回の複数回実行されます。  
  
## <a name="see-also"></a>参照  
 [メッセージと BizTalk Adapter 用 Oracle Database のメッセージ スキーマ](../../adapters-and-accelerators/adapter-oracle-database/messages-and-message-schemas-for-biztalk-adapter-for-oracle-database.md)