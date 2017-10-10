---
title: "ReceiveLocation (ReceiveLocations ノード) |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: ReceiveLocation node [binding file]
ms.assetid: 706ec5b2-c26f-428a-ad56-1c01b34aa8f8
caps.latest.revision: "9"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: f959dfc9aadfbf317d3843fb0ed174a2a0f22ea3
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="receivelocation-receivelocations-node"></a>ReceiveLocation (ReceiveLocations ノード)
バインド ファイルの ReceiveLocations ノードの ReceiveLocation ノードには、バインド ファイルと共にエクスポートされる受信場所に関する特定の情報が含まれます。  
  
## <a name="nodes-in-the-receivelocation-node"></a>ReceiveLocation ノード内のノード  
 次の表に、バインド ファイルのこのノードに設定できるプロパティを示します。  
  
|**名前**|**ノード型**|**データ型**|**Description**|**制限**|**コメント**|  
|--------------|-------------------|-------------------|---------------------|----------------------|------------------|  
|名前|属性|xs:string|受信場所の名前を指定します。|任意|既定値: 空|  
|Description|要素|xs:string|受信場所の説明を指定します。|必須|既定値: 空|  
|Address|要素|xs:string|受信場所のアドレスを指定します。|必須|既定値: 空|  
|PublicAddress|要素|xs:string|受信場所のパブリック アドレスを指定します。|任意|既定値: 空|  
|プライマリ|要素|xs:boolean|受信場所がプライマリかどうかを指定します。|必須|既定値: なし|  
|ReceiveLocationServiceWindowEnabled|要素|xs:boolean|サービス時間帯が有効であるかどうかを指定します。|必須|既定値: なし<br /><br /> 指定**true**サービス時間帯が有効である場合はそれ以外の場合、指定**false を指定します。**|  
|ReceiveLocationFromTime|要素|xs:dateTime|サービス時間帯の開始時刻を指定します。|必須|既定値: なし|  
|ReceiveLocationToTime|要素|xs:dateTime|サービス時間帯の終了時刻を指定します。|必須|既定値: なし|  
|ReceiveLocationStartDateEnabled|要素|xs:boolean|サービス時間帯の開始日が有効かどうかを指定します。|必須|既定値: なし|  
|ReceiveLocationStartDate|要素|xs:dateTime|サービス時間帯の開始日を指定します。|必須|既定値: なし|  
|ReceiveLocationEndDateEnabled|要素|xs:boolean|サービス時間帯の終了日が有効かどうかを指定します。|必須|既定値: なし|  
|ReceiveLocationEndDate|要素|xs:dateTime|サービス時間帯の終了日を指定します。|必須|既定値: なし|  
|[ReceiveLocationTransportType](../core/receivelocationtransporttype-receivelocation-node.md)|レコード|ProtocolType (ComplexType)|この受信場所のトランスポートの種類を指定します。|必須|既定値: なし|  
|ReceiveLocationTransportTypeData|要素|xs:string|受信場所のトランスポートの種類のプロパティを指定します。|任意|既定値: 空<br /><br /> 参照してください[統合 BizTalk アダプターの構成プロパティ](../core/configuration-properties-for-integrated-biztalk-adapters.md)アダプター特定プロパティについては、この文字列に格納できます。|  
|[ReceivePipeline](../core/receivepipeline-receivelocation-node.md)|レコード|PipelineRef (ComplexType)|受信場所の受信パイプラインを指定します。|必須|既定値: なし|  
|ReceivePipelineData|要素|xs:string|この受信場所に使用する受信パイプラインに固有のカスタム構成を指定します。|必須|既定値: 空|  
|[送信パイプライン](../core/sendpipeline-receivelocation-node.md)|レコード|PipelineRef (ComplexType)|双方向受信場所の送信パイプラインを指定します。 **注:**で[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]パイプライン双方向受信用は指定された受信場所ではなく、受信ポートに送信します。 バインド ファイルで指定されていない場合、受信場所は、属する受信ポートの送信パイプラインを自動的に継承します。|必須|既定値: なし|  
|SendPipelineData|要素|xs:string|この受信場所に使用する送信パイプラインに固有のカスタム構成を指定します。|必須|既定値: 空|  
|[EncryptionCert](../core/encryptioncert-receivelocation-node.md)|レコード|CertificateInfo (ComplexType)|この受信場所に関連付けられた暗号化証明書を指定します。|任意|既定値: なし|  
|[有効化]|要素|xs:boolean|受信場所が有効かどうかを指定します。|必須|既定値: なし|  
|[ReceiveHandler](../core/receivehandler-receivelocation-node.md)|レコード|ReceiveHandlerRef (ComplexType)|この受信場所で使用する受信ハンドラーを指定します。|任意|既定値: なし|