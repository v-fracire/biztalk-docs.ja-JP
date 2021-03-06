---
title: HTTP アダプター サンプル |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- HTTP adapters, examples
- examples, HTTP adapters
ms.assetid: 6796ea39-2947-45df-b228-1ecdb23a7ab8
caps.latest.revision: 9
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: f7682a16bd298ed58cf55e5122603bb2b3af9003
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36977971"
---
# <a name="http-adapter-samples"></a>HTTP アダプター サンプル
このセクションでは、BizTalk HTTP アダプターを使用するときの高度な機能を示すサンプルについて説明します。  
  
> [!NOTE]
>  このサンプルを実行する前に、次の手順を実行する必要があります。  
> 
> 1. IIS を開き、ISAPI および CGI の制限を追加します。  
> 
>    左側のパネルでコンピューター名をクリックし、右側のパネルで [ISAPI および CGI の制限] をクリックして、次の ISAPI または CGI パスを追加します。  
> 
>    64 ビット コンピューター上の追加: C:\Program Files (x86) \Microsoft BizTalk Server\<バージョン\>\HttpReceive64\BTSHTTPReceive.dll  
> 
>    32 ビット コンピューターを追加します C:\Program Files (x86) \Microsoft BizTalk Server\<バージョン\>\HttpReceive\BTSHTTPReceive.dll。  
> 
>    許可された拡張パスを確認するか、または実行します。  
>    2.  左側のパネルで [HTTPRequestResponseSample] をクリックし、中央のパネルで [ハンドラー マッピング] をクリックし、[スクリプト マップの追加] をクリックして、次のように設定します。  
> 
>    要求パス: BTSHTTPReceive.dll  
> 
>    実行可能ファイル:  
> 
>    64 ビット コンピューター: C:\Program Files (x86) \Microsoft BizTalk Server\<バージョン\>\HttpReceive64\  
> 
>    32 ビット コンピューター: C:\Program Files (x86) \Microsoft BizTalk Server\<バージョン\>\HttpReceive\  
> 
>    要求の制限:  
> 
>    動詞: POST  
> 
>    アクセス: スクリプト  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [HTTPSolicitResponse](../core/httpsolicitresponse.md)  
  
-   [HTTPRequestResponse](../core/httprequestresponse.md)