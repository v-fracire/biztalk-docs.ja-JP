---
title: "Oracle データベースでシノニムに対する操作 |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 608e8c36-ac78-4d7d-aca4-be552505fc2b
caps.latest.revision: "5"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 006107f5f21d017a79b7aa11f70fb1728bb5639a
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="operations-on-synonyms-in-oracle-database"></a>Oracle データベースでシノニムに対する操作
[!INCLUDE[adapteroracle_short](../../includes/adapteroracle-short-md.md)]シノニムに対して操作を実行することができます。 シノニムは、エイリアスまたはデータベース オブジェクト (テーブル、ビュー、ストアド プロシージャ、関数、およびパッケージ) などのフレンドリ名です。 Oracle でのシノニムについての詳細については、次を参照してください。 [http://go.microsoft.com/fwlink/?LinkId=138058](http://go.microsoft.com/fwlink/?LinkId=138058)です。  
  
## <a name="advantages-of-using-synonyms"></a>シノニムを使用する利点  
 シノニムは、次のシナリオで役立ちます。  
  
-   **スキーマが異なる作業**: を別の SQL ステートメントを使用して、それらのオブジェクトにアクセスする必要がある場合を使用して別のスキーマ、およびスキーマ間でオブジェクトにアクセスする必要があります。 スキーマでオブジェクトのシノニムを作成し、オブジェクトにアクセスする SQL ステートメントでシノニムを使用できます。 別のスキーマ内の基になるオブジェクトにアクセスする必要がある場合は、別のスキーマ内のオブジェクト をポイントするシノニムの定義を変更します。 したがって、シノニムに基づくアプリケーションは、SQL ステートメントに変更なしで機能し続けます。  
  
     たとえば、テスト環境や実稼働環境の 2 つのと同じスキーマがある場合:"Test"、"Prod"。 使用する必要があります"Test"スキーマの"Employee"をという名前のテーブルにアクセスする`Test.Employee`または`Employee`("Test"が既定のスキーマの場合)、SQL ステートメントでします。 今すぐに使用する必要がある実稼働スキーマの"Employee"表を使用する場合は、`Prod.Employee`または`Employee`("Prod"を既定のスキーマを変更する) SQL ステートメントでします。 この問題を回避するには (たとえば"")、EMP"Test.Employee"テーブルに対してシノニムを作成でき、SQL ステートメントで使用できます。 "Prod.Employee"テーブルの操作を実行する必要がある場合は、"Prod.Employee"テーブルをポイントする"EMP"シノニムの定義を変更します。 これにより、さまざまなスキーマでオブジェクトで操作を実行する、SQL ステートメントを変更する必要はありません。  
  
-   **基になるオブジェクトの変更**: シノニムの名前または操作を実行して、基になるオブジェクトの場所を変更から分離します。 名前または基になるオブジェクトの場所で任意の変化に対応するシノニムの定義を変更できます。  
  
     たとえば、ストアド プロシージャのいずれかで、テーブルを使用するいるとします。 ここで、テーブル名の変更、またはテーブルが他の場所に移動した場合、ストアド プロシージャ動作が停止します。 この問題を回避するには、ストアド プロシージャ内のテーブルのシノニムを使用し、名またはテーブルの場所に変更がある場合は、シノニムの定義を更新することができます。  
  
-   **簡略化し、セキュリティで保護されたアクセス**: 分散環境では、適切なオブジェクトにアクセスすることを確認するオブジェクト名と共にスキーマ名を使用する必要があります。 さらに、ユーザーが、ターゲット オブジェクトで権限を必要なことを確認する必要があります。 これを簡略化、オブジェクトへの完全修飾パスであるシノニムを作成することで、オブジェクトの簡易名を割り当てるし、シノニムに対する適切な特権を付与できます。  
  
## <a name="working-with-synonyms-in-the-adapter"></a>アダプターでシノニムを扱ってください。  
 [!INCLUDE[adapteroracle_short](../../includes/adapteroracle-short-md.md)]の Oracle でシノニムを公開します。  
  
-   テーブル  
  
-   ビュー  
  
-   ストアド プロシージャ  
  
-   関数  
  
-   パッケージ  
  
 内のそれぞれの基になるアーティファクトと共にこれらの成果物の各シノニムが公開されている、 [!INCLUDE[consumeadapterservshort](../../includes/consumeadapterservshort-md.md)]、 [!INCLUDE[addadapterwiz](../../includes/addadapterwiz-md.md)]、および[!INCLUDE[addadapterservrefshort](../../includes/addadapterservrefshort-md.md)]です。 たとえば、**テーブル**ノードの下のスキーマはスキーマで、データベース テーブルとテーブルのすべてのシノニムを表示、**ビュー**に沿ってビューのすべてのシノニムをスキーマの下のノードが表示されますスキーマでデータベース ビュー。  
  
-   シノニムはテーブルおよびビューの作成を同じ操作は、基になるテーブル、ビューそれぞれ公開されます。 たとえば、基になるテーブルとビューの LOB 列を含める場合はでも、それらのテーブルとビューの類義語、ReadLOB および UpdateLOB 操作も公開します。  
  
-   ストアド プロシージャ、関数、およびパッケージで作成されたシノニムのシノニムは、それぞれの基になるストアド プロシージャ、関数、およびスキーマ内のパッケージと共に操作として公開されます。  
  
> [!NOTE]
>  [!INCLUDE[adapteroracle_short](../../includes/adapteroracle-short-md.md)]ローカル シノニムだけをサポートしています。 これは、それらのシノニムだけは、ローカル サーバー上のアイテムをターゲットとするアダプターでサポートされていることを意味します。  
  
 さらに、シノニムのメッセージ アクションは、アクションが実行される成果物の名前を除いて、基になるオブジェクトと同じです。 たとえば、メッセージ アクション、**選択**SCOTT スキーマ内のテーブルでの操作が:`http://Microsoft.LobServices.OracleDB/2007/03/SCOTT/Table/[TABLE_NAME]/Select`です。 メッセージのアクションになる SCOTT スキーマで、同じテーブルに対してシノニムの選択操作を実行するかどうか:`http://Microsoft.LobServices.OracleDB/2007/03/SCOTT/Table/[SYNONYM_NAME]/Select`です。  
  
 で、アダプターでシノニムに対して操作を呼び出すとき、アダプターは、操作を実行する Oracle データベースでシノニムを呼び出します。 ただし、アダプターは、メタデータをフェッチするのにシノニムの定義で、基になるオブジェクト名を使用します。  
  
 シノニムは、通常の送信操作、複合操作、およびポーリングで使用できます。  
  
> [!NOTE]
>  シノニムを検索できます[!INCLUDE[consumeadapterservshort](../../includes/consumeadapterservshort-md.md)]または[!INCLUDE[addadapterservrefshort](../../includes/addadapterservrefshort-md.md)]他のオブジェクトと同じようにします。 ただし、パッケージ内の手順で行うことができます、スキップするレベルのノードからシノニム パッケージ内のプロシージャの検索することはできません。 アダプターでの操作の検索方法については、次を参照してください。[参照、検索、および Oracle データベースの操作のメタデータを取得](../../adapters-and-accelerators/adapter-oracle-database/browse-search-and-get-metadata-for-oracle-database-operations.md)です。  
  
## <a name="see-also"></a>参照  
 [どのような操作をアダプターであるを使用して実行しますか?](https://msdn.microsoft.com/library/cc185219(v=bts.10).aspx)