---
title: インスタンス化し、送信アダプターの初期化 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f10e6507-3351-4173-95f5-48546ca5f5c4
caps.latest.revision: 12
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: b91bb59d974d68595e53c563311c74f590d33b3d
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36978923"
---
# <a name="instantiating-and-initializing-a-send-adapter"></a>送信アダプターのインスタンス化と初期化
既定では、送信アダプターは、最初のメッセージが配信されるまでインスタンス化されません。これは "レイジー作成" と呼ばれるプロセスです。 レイジー作成による既定のアプローチは、システム リソースの節約に役立ちます。 作成された送信アダプターはキャッシュされ、BizTalk Server サービスが停止されるまで有効になります。  
  
 **InitTransmitterOnServiceStart**のメンバー、**機能**列挙型の既定のレイジー作成を使用するのではなく、サービスの開始、送信アダプターを作成するメッセージング エンジンに指示これが必要な場合。  
  
 メッセージの送信は、メッセージのバッチ処理の点でメッセージの受信とは異なるモデルです。 受信の場合、アダプターには、メッセージング エンジンから取得したバッチに挿入する受信メッセージがあります。 送信の場合は、メッセージング エンジンがアダプターからバッチを取得し、送信先のアダプターにメッセージを送信します。 どちらの場合も、トランスポート プロキシを使用してメッセージ バッチ オブジェクトが取得されます。  
  
## <a name="how-a-send-adapter-is-initialized"></a>送信アダプターの初期化  
 構成およびトランスポート プロキシへのバインドを有効にするには、アダプターに次の構成インターフェイスを実装する必要があります。  
  
- **IBTTransport**  
  
- **IBaseComponent**  
  
- **IBTTransportControl**  
  
- **IPersistPropertyBag**  
  
  送信アダプターの初期化に関連する一連のイベントを次に示します。  
  
1. まず実行、メッセージング エンジンでは、送信アダプターの初期化、 **QueryInterface**の**IPersistPropertyBag**、これは省略可能なインターフェイスです。 ハンドラーの構成がアダプターに渡されるアダプターは、インターフェイスを実装する場合、**ロード**メソッドの呼び出し。 アダプターは、この情報を使用して適切に構成されます。  
  
2. メッセージング エンジンの実行、 **QueryInterface**の**IBTTransportControl**、必須インターフェイスであります。  
  
3. エンジンの呼び出し**IBTTransportControl.Initialize**アダプターのトランスポート プロキシに渡します。  
  
4. メッセージング エンジンの実行、 **QueryInterface**の**IBTTransmitter**します。  
  
    このインターフェイスが検出された場合、アダプターはバッチ非対応の送信元として扱われます。  
  
    メッセージング エンジンが実行する場合は、メッセージング エンジンは、このインターフェイスを検出されず、 **QueryInterface**の**IBTBatchTransmitter**、検出するは、アダプターがバッチ対応であることを示します送信元。  
  
    これらのどちらのインターフェイスも検出されなかった場合、エラー状態となり、初期化が失敗します。 必須のインターフェイスのうち 1 つでも検出されないものがあると、初期化は失敗します。  
  
   この API の呼び出しの順序は、次の図のようになります。アダプターは、青色で示されるインターフェイスを実装します。  
  
   ![](../core/media/transmit-adapter-init.gif "Transmit_adapter_init")  
  
   アダプターは初期化して構成された時点で、すぐにメッセージを送信できるようになります。  
  
   送信アダプターを初期化するときの、オブジェクト間の対話処理を次に示します。  
  
   ![](../core/media/ebiz-sdk-devadapter10.gif "ebiz_sdk_devadapter10")  
   送信アダプターの初期化のワークフロー  
  
> [!NOTE]
>  アダプターがなど呼び出しにおいてメッセージング エンジンをブロックしないでください**IBTTransportControl.Initialize**と**IPersistPropertyBag.Load**します。 これらの呼び出しで過度な処理を実行した場合、サービスの開始が遅れる可能性があります。