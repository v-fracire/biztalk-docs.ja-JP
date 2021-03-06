---
title: パイプライン コンポーネントでの SOAP ヘッダーへのアクセス |Microsoft ドキュメント
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SOAP headers, pipelines
- SOAP headers, properties
- pipelines, SOAP headers
ms.assetid: a2fb074e-0fde-487e-a6ec-7e2b543b7c8b
caps.latest.revision: 8
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: e484b221df54f00b02f20ef89466fed6b99cd69d
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
ms.locfileid: "22225098"
---
# <a name="accessing-soap-headers-in-pipeline-components"></a>パイプライン コンポーネントでの SOAP ヘッダーへのアクセス
パイプライン コンポーネントでは、SOAP ヘッダーのコンテキスト プロパティにアクセスできます。 コンテキスト プロパティ名とターゲットの名前空間の組み合わせを使用する**http://schemas.microsoft.com/BizTalk/2003/SOAPHeader**です。  
  
 次のコード例は、要求 SOAP ヘッダーを受信パイプライン コンポーネントのプロパティの取得**OrigDest**:  
  
```  
public IBaseMessage Execute(IPipelineContext pc, IBaseMessage inmsg)  
{  
   try  
   {  
   string stringVar = inmsg.Context.Read("OrigDest",    "http://schemas.microsoft.com/BizTalk/2003/SOAPHeader").ToString();  
   }  
   catch (Exception ex)  
   {  
   throw new Exception("Pipeline component exception - " + ex.Message);  
   }  
return inmsg;  
}  
```  
  
 パイプライン コンポーネントの詳細については、次を参照してください。[カスタム パイプライン コンポーネントの開発](../core/developing-custom-pipeline-components.md)です。  
  
## <a name="see-also"></a>参照  
 [公開済み Web サービスでの SOAP ヘッダー](../core/soap-headers-with-published-web-services.md)