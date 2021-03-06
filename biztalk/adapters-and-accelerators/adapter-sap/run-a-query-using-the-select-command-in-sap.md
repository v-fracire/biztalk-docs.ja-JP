---
title: SELECT コマンドを使用して sap クエリの実行 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SELECT command, performing a query
- query, performing by using the SELECT command
ms.assetid: 6f03243c-ef50-4a4a-8fe6-4e525bd7efe3
caps.latest.revision: 4
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: e5e4edb19c3f69b14dd55219f504a6a3d0cc1688
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36971083"
---
# <a name="run-a-query-using-the-select-command-in-sap"></a>SELECT コマンドを使用して sap クエリを実行します。
[!INCLUDE[adoprovidersaplong](../../includes/adoprovidersaplong-md.md)] ADO.NET データ ソースとしての SAP システムを公開します。 [!INCLUDE[adoprovidersaplong](../../includes/adoprovidersaplong-md.md)]、SELECT ステートメントを実行することによって、SAP アイテムをクエリできます。  
  
## <a name="how-to-perform-a-query-by-using-the-select-command"></a>SELECT コマンドを使用して、クエリを実行する方法  
 使用してクエリ SAP アイテムを[!INCLUDE[adoprovidersapshort](../../includes/adoprovidersapshort-md.md)]、次の手順に従います。  
  
#### <a name="to-perform-a-query"></a>クエリを実行するには  
  
1. 参照を含める (と、コードでステートメントを使用) に**Microsoft.Data.SAPClient**します。  
  
2. 作成、 **SAPConnection** SAP 接続文字列のデータ プロバイダーを使用してオブジェクト。 接続文字列の詳細については、次を参照してください。 [SAP 接続文字列のデータ プロバイダーの種類について](../../adapters-and-accelerators/adapter-sap/read-about-data-provider-types-for-the-sap-connection-string.md)します。  
  
3. 呼び出すことによって、SAP システムへの接続を開く**オープン**上、 **SAPConnection**します。  
  
4. 作成、 **SAPCommand**オブジェクトから、 **SAPConnection**します。  
  
5. SELECT ステートメントの指定、 **CommandText**のプロパティ、 **SAPCommand**します。 かどうか、必要に応じてパラメーターを指定できますを使用して**SAPParameter**オブジェクト。 SELECT ステートメントを使用して SAP アイテムを照会する方法の詳細については、次を参照してください。 [SAP で SELECT ステートメントの構文](../../adapters-and-accelerators/adapter-sap/syntax-for-a-select-statement-in-sap.md)します。 RFC または BAPI を指定する方法の例については、次を参照してください。 [SELECT ステートメントの例](../../adapters-and-accelerators/adapter-sap/examples-for-select-statement.md)します。  
  
6. クエリを実行しで結果を取得するコマンドを実行する**SAPDataReader**します。  
  
7. 結果を読み取り、 **SAPDataReader**します。  
  
8. それらの使用が終了したら、閉じる (または dispose)、 **SAPConnection**と**SAPDataReader**します。  
  
   [!INCLUDE[adoprovidersapshort](../../includes/adoprovidersapshort-md.md)]も公開、 **SAPClientFactory**クラスで、作成に使用できる**SAPConnection**、 **SAPCommand**と**SAPConnection**オブジェクト。 拡張によって、ADO.NET のクラスの詳細については、[!INCLUDE[adoprovidersapshort](../../includes/adoprovidersapshort-md.md)]を参照してください[SAP アダプターを使用した ADO.NET インターフェイスの拡張](../../adapters-and-accelerators/adapter-sap/extend-ado-net-interfaces-with-the-sap-adapter.md)します。  
  
## <a name="example"></a>例  
 次の例では、コンソールに内部結合をパラメーター化されたステートメントの select の結果を書き込みます。  
  
```  
using System;  
using System.Collections.Generic;  
using System.Text;  
  
using Microsoft.Data.SAPClient;  
  
namespace SapAdoSelect  
{  
    class Program  
    {  
        static void Main(string[] args)  
        {  
        /// <summary>  
        /// select top 1 * from sflight inner join spfli on sflight.connid = spfli.connid where spfli.connid = @connid  
        /// </summary>  
  
        string connstr = "TYPE=A; ASHOST=YourSapHost; SYSNR=00; CLIENT=800; LANG=EN; USER=YourUserName; PASSWD=YourPassword;";  
  
           using (SAPConnection conn = new SAPConnection(connstr))  
            {  
                conn.Open();  
                using (SAPCommand cmd = conn.CreateCommand())  
                {  
                    cmd.CommandText = "select top 1 * from sflight inner join spfli on sflight.connid = spfli.connid where spfli.connid = @connid";  
                    cmd.Parameters.Add(new SAPParameter("@connid", 17));                      
                    using (SAPDataReader dr = cmd.ExecuteReader())  
                    {  
                        do  
                        {  
                            int rows = 0;  
                            while (dr.Read())  
                            {  
                                rows++;  
                                StringBuilder b = new StringBuilder();  
                                for (int i = 0; i < dr.FieldCount; i++)  
                                {  
                                    b.Append(dr[i].ToString()+" ");  
                                }  
                                Console.WriteLine("row {0}: {1} ", rows, b.ToString());  
                            }  
                            Console.WriteLine("Number of rows:{0}", rows);  
  
                        } while (dr.NextResult());  
                    }  
                }  
            }  
        }  
    }  
}  
```  
  
## <a name="see-also"></a>参照  
 [使用して、.NET Framework Data Provider for mySAP Business Suite](../../adapters-and-accelerators/adapter-sap/use-the-net-framework-data-provider-for-mysap-business-suite.md)   
 [サンプル](../../adapters-and-accelerators/accelerator-rosettanet/adapter-samples.md)