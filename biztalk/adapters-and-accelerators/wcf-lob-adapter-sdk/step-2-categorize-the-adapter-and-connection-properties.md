---
title: '手順 2: 分類、アダプターとの接続プロパティ |Microsoft ドキュメント'
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 45b3dc64-2078-4008-878b-501f727f4a11
caps.latest.revision: 19
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 6e9d49323695b1070a8065cf7a5e548e61fc5db9
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
ms.locfileid: "22226826"
---
# <a name="step-2-categorize-the-adapter-and-connection-properties"></a>手順 2: 分類、アダプターと接続のプロパティ
![手順 2 の 9](../../adapters-and-accelerators/wcf-lob-adapter-sdk/media/step-2of9.gif "Step_2of9")  
  
 **所要時間:** 30 分  
  
 この手順では更新、 **EchoAdapterBindingElement**と**EchoAdapterBindingElementExtensionElement**アダプターと接続のプロパティをカテゴリに分類するクラス。 これにより、プロパティは、論理的にグループ化のカテゴリによって、[!INCLUDE[addadapterservrefshort](../../includes/addadapterservrefshort-md.md)]と[!INCLUDE[consumeadapterservshort](../../includes/consumeadapterservshort-md.md)]ツールです。 たとえば、する場合は、**アプリケーション**、 **EnableAuthentication**、および**ホスト名**下に表示されるプロパティ、**接続**次のように、カテゴリの各アプリケーション、EnableAuthentication、およびホスト名のプロパティを接続カテゴリを割り当てる必要があります。  
  
 ![](../../adapters-and-accelerators/wcf-lob-adapter-sdk/media/c7c0c013-6651-4c32-9f8b-b546a68a0267.gif "c7c0c013-6651-4c32-9f8b-b546a68a0267")  
  
 同様に、する場合は、 **InboundFileFilter**と**InboundFleSystemWatcherFolder**下に表示されるプロパティ、**受信**カテゴリで次のように、する必要があります各受信のカテゴリを割り当てます。 場合は**カウント**と**EnableConnectionPooling**下に表示される、**その他**カテゴリで、それぞれに、その他のカテゴリを割り当てる必要があります。  
  
 ![](../../adapters-and-accelerators/wcf-lob-adapter-sdk/media/2acb7677-8b50-4e45-96a3-42d0e2011f19.gif "2acb7677-8b50-4e45-96a3-42d0e2011f19")  
  
 選択した任意のカテゴリ名を持つプロパティを割り当てることができることに留意してください。 この例では EnableConnnectionPooling プロパティは、他のカテゴリに属していませんのでおを分類、その他 (その他)。 InboundFileFilter プロパティについての例では、受信処理中に使用されているため方が適切です [その他] ではなく、プロパティに受信を割り当てる。 エコー アダプターのカスタム プロパティの完全な分類を次に示します。  
  
|**プロパティ**|**カテゴリ**|  
|------------------|------------------|  
|InboundFileFilter|受信|  
|InboundFileSystemWatcherFolder|受信|  
|Count|その他|  
|EnableConnectionPooling|その他|  
|アプリケーション|接続|  
|EnableAuthentication|接続|  
|hostname|接続|  
|EchoInUpperCase|Format|  
  
 Dispose メソッドの変更もこれらの変更だけでなく**EchoAdapterHandlerBase**です。  
  
 エコー アダプターによって公開されているアダプターのプロパティは、アダプターのプロパティ セクションを参照してください、[チュートリアル 1: エコー アダプターを開発](../../adapters-and-accelerators/wcf-lob-adapter-sdk/tutorial-1-develop-the-echo-adapter.md)です。  
  
## <a name="prerequisites"></a>前提条件  
 この手順を開始する前に行う必要があります[手順 1: エコー アダプター プロジェクトを作成する WCF LOB アダプター開発ウィザードを使用して](../../adapters-and-accelerators/wcf-lob-adapter-sdk/step-1-use-the-wcf-lob-adapter-development-wizard-to-create-the-echo-adapter.md)です。 必要がありますもよく理解すると、`System.ServiceModel.Configuration.BindingElementExtensionElement`と`System.ServiceModel.Configuration.StandardBindingElement`クラスです。  
  
## <a name="update-the-echoadapterhandlerbase-dispose-method"></a>Update EchoAdapterHandlerBase Dispose メソッド  
  
1.  **ソリューション エクスプ ローラー**をダブルクリックして、 **EchoAdapterHandlerBase.cs**ファイル。  
  
2.  次のステートメントを削除、 **Dispose**メソッド。  
  
    ```csharp  
    throw new NotImplementedException("The method or operation is not implemented.");  
    ```  
  
     変更後のメソッドは、次のようになります。  
  
    ```csharp  
    protected virtual void Dispose(bool disposing)  
    {  
       //  
       //TODO: Implement Dispose. Override this method in respective Handler classes  
       //  
    }  
    ```  
  
## <a name="update-the-adapter-properties-class"></a>更新アダプター プロパティ クラス  
  
1.  **ソリューション エクスプ ローラー**をダブルクリックして、 **EchoAdapterBindingElement.cs**ファイル。  
  
2.  Visual Studio エディターで、展開、**カスタム生成プロパティ**領域。  
  
3.  割り当てる、**その他**カテゴリを**カウント**プロパティの先頭に次の 1 つのステートメントを追加、**カウント**実装します。  
  
    ```csharp  
    [System.ComponentModel.Category("")]  
    ```  
  
     **カウント**実装が次と一致する必要がありますようになりました。  
  
    ```csharp  
    [System.ComponentModel.Category("")]  
    [System.Configuration.ConfigurationProperty("count", DefaultValue = 5)]  
    public int Count  
    {  
        get  
        {  
            return ((int)(base["Count"]));  
        }  
        set  
        {  
            base["Count"] = value;  
        }  
    }  
    ```  
  
4.  割り当てる、**その他**カテゴリ、 **EnableConnectionPooling**プロパティの先頭に次の 1 つのステートメントを追加、 **EnableConnectionPooling**実装です。  
  
    ```csharp  
    [System.ComponentModel.Category("")]  
    ```  
  
5.  割り当てる、**受信**カテゴリ、 **InboundFileFilter**プロパティの先頭に次の 1 つのステートメントを追加、 **InboundFileFilter**実装します。  
  
    ```csharp  
    [System.ComponentModel.Category("Inbound")]  
    ```  
  
6.  割り当てる、**受信**categoryto **inboundFleSystemWatcherFolder**プロパティの先頭に次の 1 つのステートメントを追加、 **inboundFleSystemWatcherFolder**実装します。  
  
    ```csharp  
    [System.ComponentModel.Category("Inbound")]  
    ```  
  
7.  内のコードを確認してください、**カスタム生成プロパティ**地域、次の一致します。  
  
    ```csharp  
    [System.ComponentModel.Category("")]  
    [System.Configuration.ConfigurationProperty("count", DefaultValue = 5)]  
    public int Count  
    {  
        get  
        {  
            return ((int)(base["Count"]));  
        }  
        set  
        {  
            base["Count"] = value;  
        }  
    }  
  
    [System.ComponentModel.Category("")]  
    [System.Configuration.ConfigurationProperty("enableConnectionPooling", DefaultValue = true)]  
    public bool EnableConnectionPooling  
    {  
        get  
        {  
            return ((bool)(base["EnableConnectionPooling"]));  
        }  
        set  
        {  
            base["EnableConnectionPooling"] = value;  
        }  
    }  
  
    [System.ComponentModel.Category("Inbound")]  
    [System.Configuration.ConfigurationProperty("inboundFileFilter", DefaultValue = "*.txt")]  
    public string InboundFileFilter  
    {  
        get  
        {  
            return ((string)(base["InboundFileFilter"]));  
        }  
        set  
        {  
            base["InboundFileFilter"] = value;  
        }  
    }  
  
    [System.ComponentModel.Category("Inbound")]  
    [System.Configuration.ConfigurationProperty("inboundFileSystemWatcherFolder", DefaultValue = "{InboundFileSystemWatcherFolder}")]  
    public string InboundFileSystemWatcherFolder  
    {  
        get  
        {  
            return ((string)(base["InboundFileSystemWatcherFolder"]));  
        }  
        set  
        {  
            base["InboundFileSystemWatcherFolder"] = value;  
        }  
    }  
  
    #endregion Custom Generated Properties  
    ```  
  
## <a name="update-the-connection-properties"></a>接続プロパティを更新します。  
  
1.  **ソリューション エクスプ ローラー**をダブルクリックして、 **EchoAdapterConnectionUri.cs**ファイル。  
  
2.  Visual Studio エディターで、展開、**カスタム生成プロパティ**領域。  
  
3.  割り当てる、**形式**カテゴリ、 **EchoInUpperCase**プロパティの先頭に次の 1 つのステートメントを追加、 **EchoInUpperCase**実装します。  
  
    ```csharp  
    [System.ComponentModel.Category("Format")]  
    ```  
  
4.  割り当てる、**接続**カテゴリを**ホスト名**プロパティの先頭に次の 1 つのステートメントを追加、**ホスト名**実装します。  
  
    ```csharp  
    [System.ComponentModel.Category("Connection")]  
    ```  
  
5.  割り当てる、**接続**カテゴリ、**アプリケーション**プロパティの先頭に次の 1 つのステートメントを追加、**アプリケーション**実装します。  
  
    ```csharp  
    [System.ComponentModel.Category("Connection")]  
    ```  
  
6.  割り当てる、**接続**categoryto **EnableAuthentication**プロパティの先頭に次の 1 つのステートメントを追加、 **EnableAuthentication**実装です。  
  
    ```csharp  
    [System.ComponentModel.Category("Connection")]  
    ```  
  
7.  内のコードを確認してください、**カスタム生成プロパティ**地域、次の一致します。  
  
    ```csharp  
    #region Custom Generated Properties  
            [System.ComponentModel.Category("Format")]  
            public bool EchoInUpperCase  
            {  
                get  
                {  
                    return this.echoInUpperCase;  
                }  
                set  
                {  
                    this.echoInUpperCase = value;  
                }  
            }  
  
            [System.ComponentModel.Category("Connection")]  
            public string Hostname  
            {  
                get  
                {  
                    return this.hostname;  
                }  
                set  
                {  
                    this.hostname = value;  
                }  
            }  
  
            [System.ComponentModel.Category("Connection")]  
            public string Application  
            {  
                get  
                {  
                    return this.application;  
                }  
                set  
                {  
                    this.application = value;  
                }  
            }  
  
            [System.ComponentModel.Category("Connection")]  
            public bool EnableAuthentication  
            {  
                get  
                {  
                    return this.enableAuthentication;  
                }  
                set  
                {  
                    this.enableAuthentication = value;  
                }  
            }  
            #endregion Custom Generated Properties  
    ```  
  
8.  Visual Studio から、**ファイル** メニューのをクリックして**すべて保存**です。  
  
> [!NOTE]
>  これで作業が保存されました。 安全にこの時点で Visual Studio を終了したり、次の手順に進みます[手順 3: エコー アダプターの接続を実装](../../adapters-and-accelerators/wcf-lob-adapter-sdk/step-3-implement-the-connection-for-the-echo-adapter.md)です。  
  
## <a name="what-did-i-just-do"></a>でしただけは何ですか。  
 エコー アダプターによって公開される各アダプターと接続プロパティをカテゴリに分類するクラスが更新されました。  
  
## <a name="next-steps"></a>次の手順  
 接続、メタデータの参照、検索、および機能、および送信メッセージ交換の解決を実装するとします。 最後に、ビルドおよび展開するエコー アダプター。  
  
## <a name="see-also"></a>参照  
 [手順 3: エコー アダプターの接続を実装します。](../../adapters-and-accelerators/wcf-lob-adapter-sdk/step-3-implement-the-connection-for-the-echo-adapter.md)   
 [チュートリアル 1: エコー アダプターを開発します。](../../adapters-and-accelerators/wcf-lob-adapter-sdk/tutorial-1-develop-the-echo-adapter.md)