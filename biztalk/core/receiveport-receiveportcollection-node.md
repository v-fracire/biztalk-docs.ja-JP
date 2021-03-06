---
title: ReceivePort (ReceivePortCollection ノード) |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 30ae9cef-4e0f-42ca-ac45-fe1fabdfc7c5
caps.latest.revision: 13
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 6b8e30a789327f872e384152d64a2edbebb4b9dd
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "37023160"
---
# <a name="receiveport-receiveportcollection-node"></a>ReceivePort (ReceivePortCollection ノード)
バインド ファイルの ReceivePortCollection ノードの ReceivePort ノードには、バインド ファイルと共にエクスポートされる受信ポートに関する情報が含まれます。  

## <a name="nodes-in-the-receiveport-node"></a>ReceivePort ノード内のノード  
 次の表に、バインド ファイルのこのノードに設定できるプロパティを示します。  


|                                      **名前**                                       | **ノードの種類** |            **[データ型]**             |                                               **[説明]**                                               | **制限** |                                                                                                 **コメント**                                                                                                  |
|-------------------------------------------------------------------------------------|---------------|--------------------------------------|-------------------------------------------------------------------------------------------------------------|------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                                        名前                                         |   属性   |              xs:string               |                                   受信ポートの名前を指定します。                                   |   任意   |                                                                                             既定値: 空                                                                                              |
|                                      IsTwoWay                                       |   属性   |              xs:boolean              |               受信ポートが一方向か、要求 - 応答 (双方向) かを指定します。               |     必須     |      既定値: なし<br /><br /> 使用できる値は、 **MSBTS_SendPort.IsTwoWay プロパティ (WMI)** [!INCLUDE[ui-guidance-developers-reference](../includes/ui-guidance-developers-reference.md)]      |
|                                    BindingOption                                    |   属性   |                xs:int                |                          オーケストレーション ポートのバインドの種類を指定します。                          |     必須     |                                             既定値: なし<br /><br /> 使用できる値は、 **Microsoft.BizTalk.ExplorerOM.BindingType**列挙体。                                              |
|                                     説明                                     |    要素    |              xs:string               |                                受信ポートの説明を指定します。                                |     必須     |                                                                                             既定値: 空                                                                                              |
|          [ReceiveLocations](../core/receivelocations-receiveport-node.md)           |    レコード     | ArrayOfReceiveLocation (ComplexType) |                 この受信ポートに関連付けられている受信場所のコンテナー ノードです。                 |  任意   |                                                                                              既定値: なし                                                                                              |
| [TransmitPipeline (ReceivePort ノード)](../core/transmitpipeline-receiveport-node.md) |    レコード     |      PipelineRef (ComplexType)       | 受信ポートが双方向受信ポートである場合に、受信ポートに関連付けられている送信パイプラインを指定します。 |   任意   |                                                                                              既定値: なし                                                                                              |
|                                  SendPipelineData                                   |    要素    |              xs:string               |         パイプラインの使用で、このインスタンスに固有のカスタム構成を指定します。          |   任意   |                                                                                             既定値: 空です。                                                                                             |
|                                   [認証]                                    |    要素    |                xs:int                |      この受信ポートで認証が必要かどうかを示す列挙値を指定します。       |     必須     |                                          既定値: なし<br /><br /> 使用できる値は、 **Microsoft.BizTalk.ExplorerOM.AuthenticationType**列挙体。                                          |
|                                      Tracking                                       |    要素    |                xs:int                |                        受信ポートのドキュメント追跡のレベルを指定します。                        |     必須     |                                            既定値: なし<br /><br /> 使用できる値は、 **Microsoft.BizTalk.ExplorerOM.TrackingTypes**列挙体。                                             |
|       [Transforms (ReceivePort ノード)](../core/transforms-receiveport-node.md)       |    レコード     |    ArrayOfTransform (ComplexType)    |                  一方向受信ポートの受信変換のコレクションを指定します。                  |   任意   |                                                                                              既定値: なし                                                                                              |
|        [OutboundTransforms](../core/outboundtransforms-receiveport-node.md)         |    レコード     |    ArrayOfTransform (ComplexType)    |       双方向受信ポートのドキュメントに適用する送信変換のコレクションを指定します。       |   任意   |                                                                                              既定値: なし                                                                                              |
|                                 RouteFailedMessage                                  |    要素    |              xs:boolean              |             失敗したメッセージを失敗したメッセージのサブスクライバーにルーティングするかどうかを指定します。              |     必須     | 既定値: なし<br /><br /> 使用できる値は、 **MSBTS_SendPort.RouteFailedMessage プロパティ (WMI)** [!INCLUDE[ui-guidance-developers-reference](../includes/ui-guidance-developers-reference.md)] |
|                                   ApplicationName                                   |    要素    |              xs:string               |                   受信ポートに関連付けられているアプリケーションの名前を指定します。                   |     必須     |           既定値: 空<br /><br /> 使用できる値は、 **ISSOMapping インターフェイス (COM)** [!INCLUDE[ui-guidance-developers-reference](../includes/ui-guidance-developers-reference.md)]           |

