---
title: SOAP ヘッダーで Web サービスの使用 |Microsoft ドキュメント
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SOAP headers, consuming
- Web services, consuming
- Web services, SOAP headers
- SOAP headers, Web services
ms.assetid: c2dfe7d8-e2f0-4bc6-b79c-354d06a7ffd6
caps.latest.revision: 8
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 45a3efa628e435092505fdc3884704baa15be34c
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
ms.locfileid: "22237810"
---
# <a name="consuming-web-services-with-soap-headers"></a>SOAP ヘッダーで Web サービスの使用
定義済み SOAP ヘッダーで Web サービスを使用した後、これらのヘッダーは、コンテキスト プロパティとしてオーケストレーションおよびパイプライン コンポーネントで使用できるようになります。 これらのコンテキスト プロパティには、SOAP ヘッダーの文字列表現が含まれています。 Web サービスの定義済み SOAP ヘッダーごとに、SOAP ヘッダーのルート要素に対応する名前を使用してコンテキスト プロパティを作成できます。 定義済みのすべての SOAP ヘッダー コンテキスト プロパティが、 **http://schemas.microsoft.com/BizTalk/2003/SOAPHeader**名前空間。  
  
 次の例は、SOAP ヘッダー コンテキスト プロパティを作成する方法を示しています**OrigDest**例を使用して、SOAP ヘッダーで[消費される Web サービスでの SOAP ヘッダー](../core/soap-headers-with-consumed-web-services.md):。  
  
```  
<?xml version="1.0" encoding="utf-16"?>  
<OrigDest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns=" http://SOAPHeaderWS.ItemAvailability">  
   <Origination xmlns="">Home</Origination>  
      <Destination xmlns="">Work</Destination>  
</OrigDest>  
```  
  
 応答 SOAP ヘッダーにも定義済み SOAP ヘッダーの文字列表現が含まれます。 その値は、要求 SOAP ヘッダーを作成するときの値と似ています。  
  
## <a name="see-also"></a>参照  
 [使用する Web サービスでの SOAP ヘッダー](../core/soap-headers-with-consumed-web-services.md)