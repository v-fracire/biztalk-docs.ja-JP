---
title: "競合回避モジュールとアダプターのプロバイダー フレームワーク |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fb7ea42e-b32c-40a8-b36b-c349f56f6edd
caps.latest.revision: "4"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 717e7919b3f822ba582ea3c1e50f251eea18a06b
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="the-resolver-and-adapter-provider-framework"></a>競合回避モジュールとアダプターのプロバイダー フレームワーク
競合回避モジュールとアダプターのプロバイダー フレームワークは、行程、変換、およびエンドポイントの解像度とルーティングをサポートします。 フレームワークを動的にエンドポイントを解決および送信アダプターのプロパティを設定します。 コンポーネントが、エンドポイントを解決する競合回避モジュールの後に、アダプター プロバイダーのコンポーネント セットの特定のプロパティが登録されている (たとえば、送信の Web サービス エンドポイントを検索する Universal Description, Discovery, and Integration [UDDI] を使用して)、 [!INCLUDE[prague](../includes/prague-md.md)]アダプター。 たとえば、Wcf-basichttp アダプター プロバイダーは、BizTalk 固有のメッセージに、エンドポイント、特定の BizTalk アダプターを使用する URI のコンテキスト プロパティを設定します。FTP アダプター プロバイダーは、FTP アダプターに固有のプロパティを設定します。  
  
 競合回避モジュールとアダプターのプロバイダー フレームワークの 1 つの目標は、解像度と、メッセージ レベルでの BizTalk オーケストレーションの使用を必要とせず、またはオーケストレーション レベルのルーティングをサポートします。 どちらの場合は、プラグ可能なフレームワークは、容易に開発、配置、および新しい競合回避モジュールとアダプター プロバイダーの登録を提供します。 すべての競合回避モジュールとアダプター プロバイダー適切に定義されたインターフェイスを実装および要求時に読み込まれた構成ファイルに登録を介して実行時にします。  
  
 ESB ディスパッチャーおよび ESB ディスパッチャーの逆アセンブル パイプライン コンポーネントは、競合回避モジュール マネージャーに行程 SOAP ヘッダーまたはパイプラインの構成のいずれかから接続文字列を渡すことによって、競合回避モジュールとアダプターのプロバイダー フレームワークを使用します。  
  
 [!INCLUDE[esbToolkit](../includes/esbtoolkit-md.md)]構成に登録されているすべての競合回避モジュールとアダプター プロバイダーの詳細情報が含まれています。 実行時、競合回避モジュールのマネージャー、およびアダプター マネージャーの構成ファイルから、登録されている競合回避モジュールとアダプター プロバイダーの詳細を読みで、適切なアセンブリを読み込んで BizTalk ホスト レベルのキャッシュに格納します。 このキャッシュの手法では、繰り返しの構成ファイルの読み取りおよび送信されたメッセージごとにアセンブリの読み込みを行う必要があります。  
  
 競合回避モジュールおよびアダプター プロバイダーのフレームワークの動作の仕組みとカスタム競合回避モジュールと、アダプターのプロバイダーを作成して拡張する方法を表示する方法の詳細については[変更および拡張 BizTalk ESB Toolkit](../esb-toolkit/modifying-and-extending-the-biztalk-esb-toolkit.md)です。  
  
## <a name="supported-resolution-mechanisms-resolvers"></a>サポートされている解決メカニズム (競合回避モジュール)  
 BizTalk ESB Toolkit には、次の競合回避モジュールが含まれています:**静的、UDDI、UDDI3、XPATH、BRE、BRI、行程、行程静的**と**LDAP**です。  
  
 競合回避モジュールの接続文字列が常に構成される、**モニカー** (など**BRE**) 後に":\\\\"との接続や処理の詳細。 モニカーでは、構成ファイルに関連付けられている競合回避モジュールの定義と一致します。 各接続文字列に関連付けられているプロパティは、一意、およびすべてのプロパティが必要です。 競合回避モジュールの各スキーマは、ESB に含まれています。Resolvers.Schemas プロジェクトです。  
  
 接続文字列の例を次に示します。  
  
-   **静的**  
  
     静的:\\\TransportType= です。  
  
     TransportLocation http://localhost/ESB.CanadianServices/SubmitPOService.asmx; を =  
  
     アクション = です。  
  
     EndPointConfig = です。  
  
     JaxRpcResponse = false。  
  
     MessageExchangePattern = です。  
  
     TargetNamespace = http://globalbank.esb.dynamicresolution.com/canadianservices/;  
  
     TransformType = です。  
  
-   **UDDI**  
  
     UDDI:\\\serverUrl= http://localhost: 9901/rmengine です。  
  
     serviceName = OrderPurchaseWebService です。  
  
     serviceProvider Microsoft プラクティス ESB を =  
  
-   **[XPath]**  
  
     \\\TransportType= です。  
  
     TransportLocation =/*[ローカル名 () 'OrderDoc' and namespace-uri() = = 'http://globalbank.esb.dynamicresolution.com/northamericanservices/']/*[ローカル名 () 'ID' and namespace-uri() = = 'http://globalbank.esb.dynamicresolution.com/northamericanservices/']。  
  
     アクション = です。  
  
     EndPointConfig = です。  
  
     JaxRpcResponse = です。  
  
     MessageExchangePattern = です。  
  
     TargetNamespace =/*[ローカル名 () = 'OrderDoc' and namespace-uri() = 'http://globalbank.esb.dynamicresolution.com/northamericanservices/']/*[ローカル名 () 'customerName' と名前空間 uri () = ='http://globalbank.esb.dynamicresolution.com/northamericanservices/']。  
  
     TransformType = です。  
  
-   **BRE**  
  
     BRE:\\\policy=GetCanadaEndPoint です。  
  
     バージョン = です。  
  
     useMsg = です。  
  
-   **BRI**  
  
     BRI:\\\policy=ResolveItinerary です。  
  
     バージョン = です。  
  
     useMsg = です。  
  
-   **行程**  
  
     行程:\\\name=TwoWayTestItinerary です。  
  
     バージョン = です。  
  
-   **行程静的**  
  
     行程静的:\\\name=TwoWayTestItinerary です。  
  
     バージョン = です。  
  
-   **LDAP**  
  
     LDAP:\\\TransportType=SMTP です。  
  
     TransportLocation = {メール}  
  
     フィルター = (&amp;(objectClass = ユーザー) (&#124; (userPrincipalName =yourname@domain.com))) です。  
  
     SearchRoot = です。  
  
     SearchScope サブツリー; を =  
  
     EndpointConfig サブジェクトを = {メール} 行程テスト メッセージを =&amp;  
  
     SMTPAuthenticate 0 を =&amp;  
  
     Smtphost の各 127.0.0.1 を =&amp;  
  
     From =test@globalbank.com&amp;  
  
     DeliveryReceipt = false&amp;  
  
     MessagePartsAttachments 0 を =&amp;  
  
     ReadReceipt = false。  
  
     ThrowErrorIfNotFound = false。  
  
     アクション = です。  
  
     JaxRpcResponse = false。  
  
     MessageExchangePattern = です。  
  
     TargetNamespace = です。  
  
     TransformType = です。  
  
 接続文字列内のすべての属性が必須です。 さらに、 **EndPointConfig**任意リゾルバーの設定し、を返すことができますを特別な属性です。 必要に応じて、競合回避モジュールは、BizTalk メッセージのコンテキストには書き込み可能にすると、さらに、特定の BizTalk アダプター コンテキスト プロパティに対応する名前/値ペアを格納できます。  
  
 ここで、 **ResolverDictionary**アダプター マネージャーにし、解決プロセス、パスから解決済みのすべてのプロパティを格納するインスタンスが返されます。 アダプター マネージャーは、すべてのアダプター特有であり、エンドポイント固有 BizTalk コンテキストにメッセージのプロパティを設定する特定のアダプター プロバイダー ディクショナリを渡します。 競合回避モジュールを探して、 **EndPointConfig**プロパティは、それぞれのアダプター プロパティに対応する名前/値ペアを抽出し、メッセージにこれらの値を設定します。  
  
## <a name="supported-adapter-providers"></a>サポートされているアダプター プロバイダー  
 [!INCLUDE[esbToolkit](../includes/esbtoolkit-md.md)]は、次の組み込みアダプター プロバイダーが含まれています:**ファイル、FTP、SMTP、MQSeries、Wcf-basichttp、Wcf-wshttp、**と**Wcf-custom**です。 各アダプター プロバイダーの名前は、BizTalk Server では、関連付けられたアダプター (トランスポートの種類) の名前と同じです。  
  
 競合回避モジュールとアダプターのプロバイダー フレームワークの主要な利点を拡張することによって作成、およびエンドポイント情報と登録済みの BizTalk アダプターの特定のプロパティを設定するプロバイダーをカスタム アダプターを解決するのには、独自のカスタム リゾルバーを登録します。 詳細については、次を参照してください。[変更および拡張 BizTalk ESB Toolkit](../esb-toolkit/modifying-and-extending-the-biztalk-esb-toolkit.md)です。