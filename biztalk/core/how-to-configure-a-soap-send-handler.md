---
title: SOAP 送信ハンドラーを構成する方法 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- send handlers, SOAP adapters
- SOAP adapters, denial of service
- denital of service, HTTP adapters
- configuring [SOAP adapters], send handlers
- configuring [SOAP adapters], denial of service
- SOAP adapters, send handlers
- denial of service, SOAP adapters
ms.assetid: fd610a3f-ca10-42e0-b81e-219e07e33830
caps.latest.revision: 12
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: c4bcbe39861c37db348e1e37752fbad6d9616033
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "37005483"
---
# <a name="how-to-configure-a-soap-send-handler"></a>SOAP 送信ハンドラーを構成する方法
次の手順を実行して、SOAP 送信ハンドラーを構成します。  

> [!CAUTION]
>  HTTP または SOAP アダプタ ハンドラを使用する場合は、Microsoft では、これらのハンドラーのホスト インスタンスをインストールすることをお勧め[!INCLUDE[btsWinSvr2k8](../includes/btswinsvr2k8-md.md)]または[!INCLUDE[btsWinSvr2k8R2](../includes/btswinsvr2k8r2-md.md)]コンピューター。  

### <a name="to-change-global-variables-for-a-soap-send-handler"></a>SOAP 送信ハンドラーのグローバル変数を変更するには  

1. [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]管理コンソールで、 [!INCLUDE[btsBizTalkServer2006r3ui](../includes/btsbiztalkserver2006r3ui-md.md)] **管理**、展開**BizTalk グループ**、展開**プラットフォームの設定**、順に展開**アダプター**します。  

2. 展開したアダプターの一覧でクリックして**SOAP**、右側のウィンドウで、構成する送信ハンドラーを右クリックし をクリック、**プロパティ**します。  

3. **アダプター ハンドラーのプロパティ** ダイアログ ボックスの 、**全般** タブで、**ホスト名**一覧で、受信ハンドラーが関連付けられているが、ホストを選択します。  

4. **プロキシ** タブで、次の操作を行います。  


   |   プロパティ    |                                                                                                                  目的                                                                                                                   |
   |---------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   | **[プロキシを使用する]** |                                                                                          SOAP 送信ハンドラーがプロキシ サーバーを使用するかどうかを示します。                                                                                          |
   |  **[サーバー]**   |                  プロキシ サーバーの名前を指定します。<br /><br /> 場合にこのプロパティが値にのみ必要と**プロキシを使用して、** が選択されています。<br /><br /> 型:文字列<br /><br /> 最小長: 0<br /><br /> 最大長: 256                   |
   |   **[ポート]**    | SOAP 送信ハンドラーが使用するポートを指定します。<br /><br /> 場合にこのプロパティが値にのみ必要と**プロキシを使用して、** が選択されています。<br /><br /> 既定値: 80<br /><br /> 型: 長整数<br /><br /> 最小値: 0<br /><br /> 最大値: 65535 |
   | **ユーザー名** |             認証に使用するユーザー名を指定します。<br /><br /> 場合にこのプロパティが値にのみ必要と**プロキシを使用して、** が選択されています。<br /><br /> 型:文字列<br /><br /> 最小長: 0<br /><br /> 最大長: 256             |
   | **Password**  |             認証に使用するパスワードを指定します。<br /><br /> 場合にこのプロパティが値にのみ必要と**プロキシを使用して、** が選択されています。<br /><br /> 型:文字列<br /><br /> 最小長: 0<br /><br /> 最大長: 256              |


5. **[OK]** をクリックします。  

## <a name="see-also"></a>参照  
 [SOAP アダプターの構成](../core/configuring-the-soap-adapter.md)   
 [Web サービスの公開](../core/publishing-web-services.md)