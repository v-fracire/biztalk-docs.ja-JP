---
title: "カスタム アダプター プロバイダーの作成 |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: bb93acf8-fd9d-4315-8690-f0c152a954b5
caps.latest.revision: "2"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: feb9efa5ad879e86f32ca1963313dadc7e6a9d7e
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="creating-a-custom-adapter-provider"></a>カスタム アダプター プロバイダーの作成
前のセクションで説明されていると、競合回避モジュールの実行、後に、動的な解決サービスは、結果は、エンドポイント (変換ではない) かどうかをチェックします。 サービスのインスタンスであるアダプター マネージャー インスタンスを作成、エンドポイントである場合の**AdapterMgr**クラスです。  
  
 アダプター マネージャーは、検証し、トランスポートの種類および送信トランスポートの場所を修正します。 トランスポートの種類がまだない解決された場合、および URL が"http"または"https"で始まる場合は、アダプター マネージャーは、トランスポートの種類を"Wcf-wshttp"を設定します。  
  
 次に、アダプター マネージャーは、トランスポートの種類が、有効な Microsoft BizTalk Server アダプターに相当し、そのプロパティの名前空間が返されますことを確認します。 このプロセスは、すべてのアダプターの 1 回だけ実行し、同じアダプターを使用するその他の受信メッセージのクエリを繰り返しを避けるために、キャッシュに結果を格納します。  
  
 アダプター マネージャーが、トランスポートの種類を使用して (なし、"**://**"サフィックス) を適切なアダプター プロバイダーを確認します。 アダプター プロバイダーは、カスタム アセンブリを実装する必要がありますが、 **IAdapterProvider**インターフェイスです。 アダプター プロバイダーのプロパティを使用して、**解決**構造体、**ディクショナリ**を有効にするメッセージのすべてのプロトコル固有のプロパティを設定する競合回避モジュールによって生成されたインスタンス、Microsoft BizTalk Server ランタイム エンジンを動的な解決を実行します。  
  
 同様に (前のセクションで説明)、競合回避モジュールで動的解決メカニズムを使用してエントリ Esb.config 構成ファイルで見つけますアダプター プロバイダーです。 次の XML は、構成ファイルのセクションを示しています。  
  
```xml  
<adapterProviders cacheManager= "Adapter Providers Cache Manager"  absoluteExpiration="3600">  
     <adapterProvider name="WCF-WSHttp" type="Microsoft.Practices.ESB.Adapter.WcfWSHttp.AdapterProvider, Microsoft.Practices.ESB.Adapter.WcfWSHttp, Version=2.0.0.0, Culture=neutral, PublicKeyToken=c62dd63c784d6e22" moniker="Http,Https" />  
     <adapterProvider name="WCF-BasicHttp" type="Microsoft.Practices.ESB.Adapter.WcfBasicHttp.AdapterProvider, Microsoft.Practices.ESB.Adapter.WcfBasicHttp, Version=2.0.0.0, Culture=neutral, PublicKeyToken=c62dd63c784d6e22" moniker="Http,Https" />  
     <adapterProvider name="WCF-Custom" type="Microsoft.Practices.ESB.Adapter.WcfCustom.AdapterProvider, Microsoft.Practices.ESB.Adapter.WcfCustom, Version=2.0.0.0, Culture=neutral, PublicKeyToken=c62dd63c784d6e22" moniker="mssql" />  
     <adapterProvider name="SMTP" type="Microsoft.Practices.ESB.Adapter.SMTP.AdapterProvider, Microsoft.Practices.ESB.Adapter.SMTP, Version=2.0.0.0, Culture=neutral, PublicKeyToken=c62dd63c784d6e22" moniker="smtp" />  
     <adapterProvider name="FTP" type="Microsoft.Practices.ESB.Adapter.FTP.AdapterProvider, Microsoft.Practices.ESB.Adapter.FTP, Version=2.0.0.0, Culture=neutral, PublicKeyToken=c62dd63c784d6e22">  
          <adapterConfig>  
               <add name="DefaultUsername" value="anonymous" />  
               <add name="DefaultPassword" value="" />  
          </adapterConfig>  
     </adapterProvider>  
     <adapterProvider name="MQSeries" type="Microsoft.Practices.ESB.Adapter.MQSeries.AdapterProvider, Microsoft.Practices.ESB.Adapter.MQSeries, Version=2.0.0.0, Culture=neutral, PublicKeyToken=c62dd63c784d6e22" moniker="MQS" adapterAssembly="MQSeries, Version=3.0.1.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35" />  
     <adapterProvider name="FILE" type="Microsoft.Practices.ESB.Adapter.FILE.AdapterProvider, Microsoft.Practices.ESB.Adapter.FILE, Version=2.0.0.0, Culture=neutral, PublicKeyToken=c62dd63c784d6e22" moniker="File" />  
</adapterProviders>  
```  
  
## <a name="creating-a-custom-adapter-provider"></a>カスタム アダプター プロバイダーの作成  
 アダプター マネージャー (のインスタンス、 **AdapterMgr**クラス) は構成ファイルにアダプター プロバイダーを検索し、適切なアセンブリを読み込みます。 動的解決メカニズムの具象実装が読み込まれているすべてのキャッシュ、 **IAdapterProvider**インターフェイスの構成情報とアセンブリの読み込み時に、いくつかの受信メッセージを使用して繰り返される読み取りを回避するのには同じアダプター プロバイダーです。  
  
 アダプター マネージャーが最後に、実行、 **SetEndPoint**の具象実装のメソッド、 **IAdapterProvider**インターフェイス、およびパイプライン コンポーネントは、BizTalk にメッセージを返しますメッセージ ボックス データベースです。  
  
 **カスタム アダプター プロバイダーを作成するには**  
  
1.  派生するアセンブリを作成、 **BaseAdapterProvider**基底クラスとが含まれています、 **SetEndPoint**エンドポイントにメッセージのコンテキスト プロパティを設定するメソッド。  
  
2.  使用して Esb.config 構成ファイルに追加して、アダプターのプロバイダーを登録、  **\<adapterProvider >**としてアダプターの名前を持つ要素、**名前**属性を完全にクラスの修飾名、**型**属性、モニカーとして、**モニカー**属性 (複数の値は、コンマで区切る必要があります)、および実際のアダプターのアセンブリでは必要に応じてとして、 **adapterAssembly**属性。  
  
3.  グローバル アセンブリ キャッシュに新しいアセンブリを登録します。