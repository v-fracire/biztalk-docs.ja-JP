---
title: Siebel アダプターのクラスを DbDataReader |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Data Provider for Siebel, DbDataReader
- DbDataReader
ms.assetid: 7673cd10-ec1e-4cb0-93c2-f11928d00ca2
caps.latest.revision: 4
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 9ad584571f7ef746a43032935e42e377ceb6cd70
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "37012619"
---
# <a name="dbdatareader-class-in-the-siebel-adapter"></a>Siebel アダプターの DbDataReader クラス
[!INCLUDE[adoprovidersiebelshort](../../includes/adoprovidersiebelshort-md.md)]提供、 `DbDataReader` XML データ リーダーを活用することです。 これは、Siebel データ ソースのコンシューマーに、行の順方向専用ストリームを読み取る機能を提供します。  

## <a name="supported-properties"></a>サポートされているプロパティ  
 [!INCLUDE[adoprovidersiebelshort](../../includes/adoprovidersiebelshort-md.md)]は、次をサポート`DbDataReader`プロパティ。  

|名前|取得/設定|説明|  
|----------|--------------|-----------------|  
|**HasRows**|取得|このプロパティはサポートされていません、アクセスする場合は例外がスローされます。|  
|**IsClosed**|取得|示す値を取得するかどうか、`DbDataReader`が閉じられました。|  
|**RecordsAffected**|取得|示す値を取得するかどうか、 `DbDataReader` 1 つまたは複数の行が含まれています。|  
|**Item(Int32)**|取得|オブジェクトのインスタンスとして指定された列の値を取得します。 このインデクサーを呼び出すときに、必要な列の序数を使用します。|  
|**Item(String)**|取得|オブジェクトのインスタンスとして指定された列の値を取得します。 このインデクサーを呼び出すときに、必要な列の名前を使用します。|  

## <a name="supported-methods"></a>サポートされているメソッド  
 [!INCLUDE[adoprovidersiebelshort](../../includes/adoprovidersiebelshort-md.md)]は、次をサポート`DbDataReader`メソッド。  


|        名前        |                                                                                                                                                                                                                            説明                                                                                                                                                                                                                             |
|--------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **GetSchemaTable** | `DbDataReader` の列メタデータを表す `DataTable` を返します。 によってサポートされるスキーマの列属性、[!INCLUDE[adoprovidersiebelshort](../../includes/adoprovidersiebelshort-md.md)]は。<br /><br /> -ColumnName<br />-ColumnOrdinal<br />.NET データ型<br />長さ<br />-有効桁数 (該当する場合)<br />-スケール (該当する場合)<br />-AllowDBNull<br />-LocalName<br />-拡張 LocalName<br />-Namespace |
|   **GetString**    |                                                                                                                                                                                                 指定した列の値を `String` のインスタンスとして取得します。                                                                                                                                                                                                 |
|    **GetValue**    |                                                                                                                                                                                                 指定した列の値を `String` のインスタンスとして取得します。                                                                                                                                                                                                 |
|    **データ型**    |                                                                                                                                                                                       列に存在しないか、不足している値が含まれるかどうかを示す値を取得します。                                                                                                                                                                                       |
|   **NextResult**   |                                                                                                                                                           Siebel データ プロバイダーは常に、1 つの結果セットを返しますそのためこの呼び出しは、現在の結果セットを返す前に完全を達した**false**します。                                                                                                                                                           |
|      **読み取り**      |                                                                                                                                                         リーダーを結果セットの次のレコードに進めます。  返されます**true**成功した場合と**false**左レコードを持つ読者場合。                                                                                                                                                         |
|     **Close**      |                                                                                                         閉じる、`DbDataReader`オブジェクト。 **注意:** したらを使用して、`DbDataReader`オブジェクト、Siebel の COM ライブラリのオブジェクトを解放するために、それを閉じる必要があります。 それ以外の場合、クライアント アプリケーションのメモリやハンドルの使用状況参照してください。                                                                                                          |

## <a name="see-also"></a>参照  
 [Siebel アダプターを使用した ADO.NET インターフェイスを拡張します。](../../adapters-and-accelerators/adapter-siebel/extend-ado-net-interfaces-with-the-siebel-adapter.md)