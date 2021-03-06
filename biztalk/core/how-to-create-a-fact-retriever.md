---
title: ファクト取得コンポーネントを作成する方法 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- IFactRetriever interface
- Business Rules Framework, bindings
- factsHandleIn object
- Business Rules Framework, code samples
- Business Rules Framework, fact retrievers
- UpdateFacts method
- Business Rules Framework, programming
ms.assetid: 503dc769-3ada-4099-a5fe-4dd03d995600
caps.latest.revision: 10
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 3157eca412123556a6e9637e1ffa28a8da7daa19
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "37012323"
---
# <a name="how-to-create-a-fact-retriever"></a>ファクト取得コンポーネントを作成する方法
ファクト取得コンポーネントは、ポリシーの実行時に、長期間のファクトのインスタンスをポリシーとしてアサートする際に使用されるコンポーネントです。 実装することができます、 **IFactRetriever**インターフェイスし、長期間のファクトのインスタンスで実行時にこの実装を使用するポリシーのバージョンを構成します。 ポリシーのバージョンを呼び出す、 **UpdateFacts**ファクト取得コンポーネントが特定のバージョン用に構成されている場合、すべての実行サイクルでファクト取得コンポーネントの実装のメソッド。  
  
 必要に応じて実装することができます、 **IFactRemover**ファクト取得コンポーネントのインターフェイス。 ルール エンジンは、 **UpdateFactsAfterExecution**のメソッド、 **IFactRemover**ポリシーが破棄されるときのインターフェイスします。 これをデータベースの変更をコミットするか、ルール エンジンの作業メモリから任意のオブジェクト インスタンスの取り消しなどの実行後の作業を行うことに、機会を提供します。  
  
## <a name="to-specify-a-fact-retriever-for-a-policy"></a>ポリシーに対してファクト取得コンポーネントを指定するには  
 ファクト取得コンポーネントとして、"MyAssembly" アセンブリの "Retriever" というクラスを使用するようにルール セットを構成するには、次のようなコードを使用します。  
  
```  
RuleEngineComponentConfiguration fr = new RuleEngineComponentConfiguration("MyAssembly", "Retriever");  
RuleSet rs = new RuleSet("ruleset");  
// associate the execution configuration with a ruleset  
RuleSetExecutionConfiguration rsCfg = rs.ExecutionConfiguration;  
rsCfg.FactRetriever = factRetriever;  
```  
  
> [!NOTE]
>  RuleEngineComponentConfiguration コンストラクターの最初のパラメーターとして MyAssembly のような単純なアセンブリ名を指定した場合、BizTalk ルール エンジンではプライベート アセンブリと認識され、ユーザーのアプリケーション フォルダー内のアセンブリが検索されます。 完全修飾アセンブリ名を指定する場合**MyAssembly, Version 1.0.0.0、カルチャを = = neutral, PublicKeyToken = a310908b42c024fe**、ルール エンジンでは、共有アセンブリとグローバル アセンブリが検索されますアセンブリ キャッシュ (GAC)。 シンプルで完全修飾アセンブリ名の定義を検索する[ http://go.microsoft.com/fwlink/?LinkId=64535](http://go.microsoft.com/fwlink/?LinkId=64535)します。  
  
 特定のデータ ソースに接続するためのアプリケーション固有のロジックを備えたファクト取得コンポーネントを設計し、そのデータをエンジンに対する長期間のファクトとしてアサートして、新しいファクトのインスタンスをエンジンに対して更新またはアサートするためのロジックを指定できます。 後続の実行サイクルでは、値が更新されるまで、最初にエンジンに対してアサートされ、キャッシュされた値が使用されます。 ファクト取得コンポーネントの実装は、トークンに似ていますオブジェクトを返しますおよびと組み合わせて使用することができます、 **factsHandleIn**オブジェクトを既存のファクトを更新または新しいファクトをアサートするかどうかを判断します。 ポリシーのバージョンは、最初に、そのファクト取得コンポーネントを呼び出すときに、 **factsHandleIn**オブジェクトは常に null とし、ファクト取得コンポーネントの実行後に、返されたオブジェクトの値を取得します。  
  
 長期間のファクトをアサートするのは、同じルール エンジンのインスタンスに対して 1 回だけでかまいません。 たとえば、使用、**ルールの呼び出し**ポリシー インスタンス、オーケストレーションの図形が内部キャッシュに移動します。 このとき、短期間のファクトはすべて取り消され、長期間のファクトが維持されます。 同じオーケストレーション インスタンスまたは同じホストの別のオーケストレーション インスタンスによって同じポリシーが再び呼び出された場合、このポリシー インスタンスがキャッシュから取得され再利用されます。 バッチ処理のシナリオによっては、同じポリシーのインスタンスが複数作成される場合があります。 新しいポリシー インスタンスが作成された場合は、適切な長期間のファクトがアサートされるように配慮する必要があります。  
  
 また、次のような処理を実現するカスタム コードを作成することもできます。  
  
- 長期間のファクトが更新されたタイミングを確認する。  
  
- どのルール エンジンのインスタンスが、どの長期間のファクトによって使用されたかを追跡する。  
  
  次のコード例は、ファクト取得コンポーネントの実装例です。ファクト取得コンポーネントを MyPolicy に関連付け、各種のバインディング方法を使って MyTableInstance を長期間のファクトとしてアサートします。  
  
## <a name="datatable-binding"></a>DataTable バインド  
  
```  
using System;  
using System.Xml;  
using System.Collections;  
using Microsoft.RuleEngine;  
using System.IO;  
using System.Data;  
using System.Data.SqlClient;  
namespace MyBizTalkApplication.FactRetriever  
{  
   public class myFactRetriever:IFactRetriever  
   {  
      public object UpdateFacts(RuleSetInfo rulesetInfo, Microsoft.RuleEngine.RuleEngine engine, object factsHandleIn)  
      {  
         object factsHandleOut;  
         if (factsHandleIn == null)   
  
         {  
            SqlDataAdapter dAdapt = new SqlDataAdapter();  
            dAdapt.TableMappings.Add("Table", "CustInfo");  
            SqlConnection conn = new SqlConnection("Initial Catalog=Northwind;Data Source=(local);Integrated Security=SSPI;");  
            conn.Open();  
            SqlCommand myCommand = new SqlCommand("SELECT * FROM CustInfo", conn);  
            myCommand.CommandType = CommandType.Text;  
            dAdapt.SelectCommand = myCommand;  
            DataSet ds = new DataSet("Northwind");  
            dAdapt.Fill(ds);  
            TypedDataTable tdt = new TypedDataTable(ds.Tables["CustInfo"]);  
            engine.Assert(tdt);  
            factsHandleOut = tdt;  
         }  
  
         else  
            factsHandleOut = factsHandleIn;  
         return factsHandleOut;  
      }  
   }  
}  
```  
  
## <a name="datarow-binding"></a>DataRow バインド  
  
```  
using System;  
using System.Xml;  
using System.Collections;  
using Microsoft.RuleEngine;  
using System.IO;  
using System.Data;  
using System.Data.SqlClient;  
namespace MyBizTalkApplication.FactRetriever  
{  
   public class myFactRetriever:IFactRetriever  
   {  
  
      public object UpdateFacts(RuleSetInfo rulesetInfo, Microsoft.RuleEngine.RuleEngine engine, object factsHandleIn)  
      {  
         object factsHandleOut;  
         if (factsHandleIn == null)   
  
         {  
            SqlDataAdapter dAdapt = new SqlDataAdapter();  
            dAdapt.TableMappings.Add("Table", "CustInfo");  
            SqlConnection conn = new SqlConnection("Initial Catalog=Northwind;Data Source=(local);Integrated Security=SSPI;");  
            conn.Open();  
            SqlCommand myCommand = new SqlCommand("SELECT * FROM CustInfo", conn);  
            myCommand.CommandType = CommandType.Text;  
            dAdapt.SelectCommand = myCommand;  
            DataSet ds = new DataSet("Northwind");  
            dAdapt.Fill(ds);  
            TypedDataTable tdt = new TypedDataTable(ds.Tables["CustInfo"]);  
  
            // binding to the first row of CustInfo table  
            TypedDataRow tdr = new TypedDataRow(ds.Tables["CustInfo"].Rows[0],tdt);  
            engine.Assert(tdr);  
            factsHandleOut = tdr;     
         }  
         else  
            factsHandleOut = factsHandleIn;  
         return factsHandleOut;  
      }  
   }   
}  
```  
  
 次のコード例は、ファクト取得コンポーネントを実装することにより、.NET および XML のファクトをアサートする方法を示しています。  
  
```  
using System;  
using System.Xml;  
using System.Collections;  
using Microsoft.RuleEngine;  
using System.IO;  
using System.Data;  
using System.Data.SqlClient;  
namespace MyBizTalkApplication.FactRetriever  
{  
   public class myFactRetriever:IFactRetriever  
   {  
      public object UpdateFacts(RuleSetInfo rulesetInfo, Microsoft.RuleEngine.RuleEngine engine, object factsHandleIn)  
      {  
         object factsHandleOut;  
         if (factsHandleIn == null)   
         {  
            //create .NET object instances  
            bookInstance = new Book();  
            magazineInstance = new Magazine();              
  
            //create an instance of the XML object  
            XmlDocument xd = new XmlDocument();  
  
            //load the document  
            xd.Load(@"..\myXMLInstance.xml");  
  
            //create and instantiate an instance of TXD  
            TypedXmlDocument doc = new TypedXmlDocument("mySchema",xd1);  
  
            engine.Assert(bookInstance);  
            engine.Assert(magazineInstance);  
            engine.Assert(doc);  
            factsHandleOut = doc;  
         }  
         else  
            factsHandleOut = factsHandleIn;  
         return factsHandleOut;  
      }  
   }  
}  
```  
  
## <a name="dataconnection-binding"></a>DataConnection バインド  
  
```  
using System;  
using System.Xml;  
using System.Collections;  
using Microsoft.RuleEngine;  
using System.IO;  
using System.Data;  
using System.Data.SqlClient;  
namespace MyBizTalkApplication.FactRetriever  
{  
   public class myFactRetriever:IFactRetriever  
   {  
      public object UpdateFacts(RuleSetInfo rulesetInfo, Microsoft.RuleEngine.RuleEngine engine, object factsHandleIn)  
      {  
         object factsHandleOut;  
  
         {   
            string strCmd = "Initial Catalog=Northwind;Data Source=(local);Integrated Security=SSPI;";  
            SqlConnection conn = new SqlConnection(strCmd);  
            DataConnection dc = new DataConnection("Northwind", "CustInfo", conn);  
  
            engine.Assert(dc);  
            factsHandleOut = dc;           
         }  
         return factsHandleOut;  
      }  
   }  
}  
```  
  
 なお**DataConnection**s は、上記のコード サンプルで示すように、ファクト取得コンポーネントから提供されている場合は、アサート常にする必要があります。 エンジンのインスタンスを使用して、 **DataConnection** 、ルールの条件に基づいて、データベース クエリを実行して、クエリによって返される行がように、エンジンの作業メモリにアサート**TypedDataRow**秒。 DataConnection を再により、エンジンの前回の実行からの行がメモリからクリアされます。  
  
 実際には、アサートするほとんどのメリットがある、 **DataConnection**ファクトを使用する点の取得元はデータ ソースを外部化する方法を提供します。