---
title: '手順 4: HeaderHelper プロジェクトの作成 |Microsoft Docs'
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- projects, helper projects
- private process tutorial, creating helper projects
ms.assetid: 82413537-032a-4368-8d77-d024a7c83b0b
caps.latest.revision: 7
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: a01323dba6fba4673e4bcd2886df53d408421f9f
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36970795"
---
# <a name="step-4-creating-the-headerhelper-project"></a>手順 4: HeaderHelper プロジェクトの作成
ここでは、[!INCLUDE[btsDotNet](../../includes/btsdotnet-md.md)] クラス ライブラリを作成します。 プライベート プロセス オーケストレーションが受信メッセージを受信すると、HeaderHelper ライブラリは、ドキュメントの変換が必要かどうかを判断し、変換が必要な場合は変換を実行します。 これにより、オーケストレーションは別のバージョンの RNIF (RosettaNet Implementation Framework) ドキュメントでも使用できます。 また、3A2 応答メッセージを送信する際には、HeaderHelper ライブラリはメッセージを送信する前に追加のドキュメント変換を実行します。  
  
### <a name="to-create-the-headerhelper-project"></a>HeaderHelper プロジェクトを作成するには  
  
1. [!INCLUDE[btsVStudioNoVersion](../../includes/btsvstudionoversion-md.md)]、ソリューション エクスプ ローラーでは、Contoso ソリューションを右クリックし、] をポイント**追加**、] をクリックし、**新しいプロジェクト**します。  
  
2. 新しいプロジェクトの追加 ダイアログ ボックスで、プロジェクトの種類 ペインで、次のように選択します。 **Visual c#** します。  
  
3. [テンプレート] ペインで、選択、**クラス ライブラリ**テンプレート。  
  
4. **名前**ボックスに「 **HeaderHelper**、順にクリックします**OK**プロジェクトを作成します。  
  
5. ソリューション エクスプ ローラーで右クリックし、 **Class1.cs**ファイル、 **HeaderHelper**プロジェクトで、をクリックして**の名前を変更**、型**HeaderHelper.cs**、キーを押しますと**Enter**します。  
  
### <a name="to-create-the-helper-class"></a>ヘルパー クラスを作成するには  
  
1.  ソリューション エクスプ ローラーで、 **HeaderHelper**プロジェクト、し、ダブルクリック、 **HeaderHelper.cs** node を HeaderHelper ソース ファイルを開きます。  
  
2.  ソース ファイルに次のコードを入力し、既存のすべてのコードを上書きします。  
  
    ```  
    using System;  
    using System.Xml;  
  
    namespace ContosoPriceAndAvailability  
    {  
        public class Helper  
        {  
            static public XmlDocument NormalizeHeader( XmlDocument curPip )  
            {  
                string strInput = curPip.OuterXml;  
                try  
                {  
                    XmlDocument xDoc = new XmlDocument();  
  
                    strInput = strInput.Replace("<!DOCTYPE Pip3A2PriceAndAvailabilityQuery SYSTEM \"3A2PriceAndAvailabilityQueryMessageGuideline_v1_3.dtd\"[]>",String.Empty);  
                    strInput = strInput.Replace("<Pip3A2PriceAndAvailabilityQuery>","<Pip3A2PriceAndAvailabilityQuery xmlns=\"http://schemas.microsoft.com/biztalk/btarn/2004/3A2PriceAndAvailabilityQueryMessageGuideline_v1_3.dtd\">");  
                    strInput = strInput.Replace("xml:",String.Empty);  
                    strInput = strInput.Replace("b:",String.Empty);  
                    strInput = strInput.Replace("lang:",String.Empty);  
                    strInput = strInput.Replace("ns1:",String.Empty);  
  
                    xDoc.LoadXml(strInput);  
  
                    return xDoc;  
                }  
                catch(Exception ex)  
                {  
                    System.Diagnostics.Debug.Write( ex.Message );  
                    throw ex;  
                }  
            }  
  
            static public string ReturnSCWithDocType( XmlDocument xmlDoc )  
            {  
                try  
                {  
                    string sResponse = xmlDoc.InnerXml;  
                    sResponse=sResponse.Replace("ns0:",String.Empty);  
                    xmlDoc.LoadXml(sResponse);  
                    xmlDoc.DocumentElement.RemoveAllAttributes();  
                    sResponse = xmlDoc.InnerXml;  
  
                    sResponse = sResponse.Insert(0,"<!DOCTYPE Pip3A2PriceAndAvailabilityResponse SYSTEM \"3A2PriceAndAvailabilityResponseMessageGuideline_v1_3.dtd\">");  
                    sResponse = sResponse.Replace("ns0:",String.Empty);  
                    sResponse = sResponse.Replace("b:",String.Empty);  
                    sResponse = sResponse.Replace("lang:",String.Empty);  
                    sResponse = sResponse.Replace("ns1:",String.Empty);  
  
                    return sResponse;  
                }  
                catch(Exception ex)  
                {  
                    throw ex;  
                }  
            }  
        }  
    }  
    ```  
  
3.  **[ファイル]** メニューの **[すべてを保存]** をクリックします。  
  
### <a name="to-create-a-strong-named-assembly-for-the-headerhelper-project"></a>HeaderHelper プロジェクトの厳密な名前のアセンブリを作成するには  
  
1.  ソリューション エクスプ ローラーで右クリックし、 **HeaderHelper**プロジェクトをクリックして**プロパティ**します。  
  
2.  HeaderHelper のプロパティ ページ ダイアログ ボックスで、**署名**HeaderHelp プロパティ ペインの左側のウィンドウにします。  
  
3.  右側のウィンドウで次のようにクリックします。**アセンブリに署名**します。  
  
4.  をクリックして、**厳密な名前キー ファイルを選択して**クリックしてテキスト ボックスに、 **\<参照\>** ドロップダウン リストから。  
  
5.  ファイルの選択 ダイアログ ボックスで、Contoso アセンブリの場所に移動し、ダブルクリックして**FabConPriceAvail.snk**します。  
  
6.  **[ファイル]** メニューの **[すべてを保存]** をクリックします。  
  
7.  ソリューション エクスプ ローラーで、 **HeaderHelper**プロジェクトで、展開、**プロパティ**ノードをクリックして、 **AssemblyInfo.cs**ノード、AssemblyInfo.csソース ファイルです。  
  
8.  AssemblyInfo.cs ソース ファイルの AssemblyCulture 属性の後の行に、次のコードを入力します。  
  
    ```  
    [assembly: AssemblyKeyFile("../../../FabConPriceAvail.snk")]  
    ```  
  
9. **[ファイル]** メニューの **[すべてを保存]** をクリックします。  
  
### <a name="to-build-and-deploy-the-headerhelper-project"></a>HeaderHelper プロジェクトを構築および展開するには  
  
1.  ソリューション エクスプ ローラーで右クリックし、 **HeaderHelper**プロジェクトをクリックして**ビルド**します。  
  
2.  開始**Visual Studio 2012 のコマンド プロンプト**します。  
  
3.  コマンド プロンプトでの場所に移動、 **HeaderHelper**プロジェクト出力ディレクトリ (\Bin\Debug フォルダー)。  
  
4.  コマンド プロンプトで「 **gacutil/if HeaderHelper.dll**キーを押します**Enter**をインストールする、 **HeaderHelper**アセンブリを、**グローバル アセンブリ キャッシュ**.  
  
## <a name="see-also"></a>参照  
 [手順 5: Contoso プライベート プロセス オーケストレーションの変更](../../adapters-and-accelerators/accelerator-rosettanet/step-5-modifying-the-contoso-private-process-orchestration.md)