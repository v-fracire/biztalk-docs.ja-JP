---
title: "SOAP 送信ポートを構成する方法 |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SOAP adapters, send ports
- SOAP adapters, code samples
- code samples, SOAP adapters
- configuring [SOAP adapters], code samples
- configuring [SOAP adapters], send ports
- send ports, SOAP adapters
ms.assetid: 3a0622f4-d25d-4449-a063-d8ba217e9729
caps.latest.revision: "11"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 3cb290feb7b61cf3d2ccdeffb6c795d88c537b4e
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="how-to-configure-a-soap-send-port"></a>SOAP 送信ポートを構成する方法
SOAP 送信ポートは、プログラムから、または [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 管理コンソールを使用して構成できます。  
  
 **プログラムから SOAP 送信ポートを構成する方法**  
  
 BizTalk エクスプローラ オブジェクト モデルがという名前の送信ポートのアダプターに固有のインターフェイスを公開する**ITransportInfo**を持つ、 **TransportTypeData**読み取り/書き込みプロパティです。 このプロパティでは、名前と値の組の XML 文字列の形式で SOAP 送信ポートの構成プロパティ バッグを指定できます。 注ことを設定するこのプロパティで、BizTalk エクスプローラ オブジェクト モデルを設定する必要があります、 **OutboundTransportLocation**のプロパティ、 **ITransportInfo**最初のインターフェイスです。  
  
 **TransportTypeData**のプロパティ、 **ITransportInfo**インターフェイスは必要ありません。 このプロパティを設定しない場合、アダプタでは、次の表に記載されている SOAP 送信ポートの構成の既定値が使用されます。  
  
 次の表は、送信ポートを SOAP 用 BizTalk エクスプローラ オブジェクト モデルに設定できる構成プロパティ。  
  
|プロパティ名|型|Description|  
|-------------------|----------|-----------------|  
|**URI**|文字列|展開サーバーの Web サービスを含んでいる仮想ディレクトリです。|  
|**ユーザー名**|文字列|対象の Web サービスにアクセスするために指定するユーザー名です。<br /><br /> 既定値: 空白|  
|**Password**|文字列|サーバーでの認証に使用するユーザーのパスワード。<br /><br /> 既定値: 空白|  
|**ClientCertificate**|文字列|SSL クライアント証明書の拇印です。<br /><br /> 既定値: 空白|  
|**AffiliateApplicationName**|文字列|チケットをクライアントの資格情報と引き換えるために使用する SSO アプリケーションの名前です。<br /><br /> **AffiliateApplicationName**は相互に排他的、 **Username**と**パスワード**ペア。<br /><br /> 既定値: 空白|  
|**UseProxy**|ブール値|SOAP 送信ポートで、対象の Web サービスへのアクセスにプロキシ サーバーを使用するかどうかを示します。 プロキシ サーバーはすべての SOAP 送信ポートで共有できます。<br /><br /> 既定値: False|  
|**ProxyAddress**|文字列|Web サービスの呼び出しに使用する HTTP プロキシのアドレスです。<br /><br /> 既定値: 空白|  
|**ProxyPort**|Integer|Web サービスの呼び出しに使用する HTTP プロキシのポートです。<br /><br /> 既定値: 空白|  
|**ProxyUsername**|文字列|プロキシに使用するユーザー名です。<br /><br /> 既定値: 空白|  
|**ProxyPassword**|文字列|プロキシに使用するパスワードです。<br /><br /> 既定値: 空白|  
  
 次のコード例は、上記のプロパティの設定に使用する形式を示しています。  
  
```  
<CustomProps>  
   <URI vt="8"/>  
   <ClientCertificate vt="8"/>  
   <Password vt="8">Encrypted</Password>  
   <ProxyAddress vt="8"/>  
   <ProxyPassword vt="8">Encrypted</ProxyPassword>  
   <ProxyPort vt="3"/>  
   <ProxyUsername vt="8"/>  
   <UseProxy vt="11"/>  
   <Username vt="8"/>  
   <AffiliateApplicationName vt="8"/>  
</CustomProps>  
```  
  
 **BizTalk Server 管理コンソールを使用して SOAP 送信ポートを構成する方法**  
  
 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 管理コンソールで、SOAP 送信ポート アダプターの変数を設定できます。 プロパティが送信ポートに設定されていない場合は、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 管理コンソールで設定されている既定の送信ハンドラーの値が使用されます。  
  
### <a name="to-configure-variables-for-a-soap-send-port"></a>SOAP 送信ポートの変数を構成するには  
  
1.  [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 管理コンソールで、新しい送信ポートを作成するか、既存の送信ポートをダブルクリックして変更します。 詳細については、次を参照してください。[送信ポートを作成する方法](../core/how-to-create-a-send-port2.md)です。 すべての送信ポートのオプションを構成し、指定**SOAP**の**型**オプション、**トランスポート**のセクションで、**全般**タブです。  
  
2.  **全般** タブの 、**トランスポート**横**型**、 をクリックして**構成**です。  
  
3.  **SOAP トランスポートのプロパティ** ダイアログ ボックスで、**全般** タブで、次の操作します。  
  
    |プロパティ|目的|  
    |--------------|----------------|  
    |**Web サービス URL**|呼び出す Web サービスのアドレスを指定します。 **注:**の URI を送信ポートまたは受信場所は、256 文字を超えることはできません。|  
    |**[認証]**|呼び出している Web サービスで使用される認証方法を示します。<br /><br /> オプション：<br /><br /> -   **匿名です。** 既定の設定です。<br />-   **基本的な。** SOAP 接続で、プレーンテキストでユーザー名とパスワードを送信します。<br />-   **ダイジェストします。** SOAP 接続で、パスワードを暗号化形式で送信します。<br />-   **NTLM。** ユーザー名もパスワードも、SOAP 接続経由では送信されません。 SOAP アダプタは常に、SOAP 送信アダプタがこの認証の種類に対して実行するプロセスの資格情報を使用します。|  
    |**資格情報**|使用する資格情報の種類を指定します。<br /><br /> 場合にのみ使用可能な**認証の種類**は**基本**または**ダイジェスト**です。<br /><br /> オプション：<br /><br /> -   **シングル サインオンを使用しないでください。**<br />     **ユーザー名**<br />     移行先サーバーで認証に使用するユーザー名。 場合、**認証の種類**プロパティは**匿名**または**NTLM**、このオプションは無効です。 場合、このプロパティが値を必要と**基本**または**ダイジェスト**が選択されているエンタープライズ シングル サインオンは使用されません。<br />     最小長: 0<br />     最大長: 256<br />     **Password**<br />     接続先のサーバーで認証に使用するパスワードを指定します。 場合、**認証の種類**プロパティは**匿名**または**NTLM**、このオプションは無効です。 場合、このプロパティが値を必要と**基本**または**ダイジェスト**が選択されているとシングル サインオンでは使用されません。<br />     最小長: 0<br />     最大長: 256<br />-   **シングル サインオンを使用します。**<br />     接続先のサーバーでの認証でクライアントの資格情報を取得する際に、シングル サインオンを使用するかどうかを指定します。<br />     **関連アプリケーション**<br />     シングル サインオンを使用する関連アプリケーションを指定します。 この一覧を設定する方法については、次を参照してください。 [SSO 関連アプリケーション](../core/sso-affiliate-applications.md)です。<br />     最小長: 0<br />     最大長: 256|  
    |**クライアント証明書の拇印**|接続の確立に使用するクライアント証明書の拇印を指定します。<br /><br /> 例: 01 23 45 67 89 AB CD EF 01 23 45 67 89 AB CD EF 01 23 45 67<br /><br /> 最小長: 0<br /><br /> 最大長: 59|  
  
4.  **SOAP トランスポートのプロパティ** ダイアログ ボックスで、**プロキシ** タブで、次の操作します。  
  
    |プロパティ|目的|  
    |--------------|----------------|  
    |**ハンドラーの既定のプロキシ構成を使用します。**|送信ポートのプロキシ ハンドラの構成を指定します。 True の場合、ポートはハンドラ レベルで指定したプロキシ設定を使用します。 False に設定されている場合、送信アダプタが送信ポートで指定されたプロキシ情報を使用します。<br /><br /> 既定値の設定は true です。|  
    |**プロキシを使用しません。**|SOAP 送信ハンドラーがプロキシ サーバーを使用するかどうかを示します。|  
    |**[プロキシを使用する]**|SOAP 送信ハンドラーがプロキシ サーバーを使用するかどうかを示します。 プロキシ サーバーはすべての SOAP 送信ポートで共有できます。|  
    |**[サーバー]**|プロキシ サーバーの名前を指定します。<br /><br /> 場合にこのプロパティが値にのみ必要と**プロキシを使用して**が選択されています。<br /><br /> 型:文字列<br /><br /> 最小長: 0<br /><br /> 最大長: 256|  
    |**[ポート]**|SOAP 送信ハンドラーが使用するポートを指定します。<br /><br /> 場合にこのプロパティが値にのみ必要と**プロキシを使用して**が選択されています。<br /><br /> 既定値: 80<br /><br /> 型: 長整数<br /><br /> 最小値: 0<br /><br /> 最大値: 65535**注:** 0 の値を指定するポート 80 が既定値を使用することを示します。|  
    |**ユーザー名**|認証に使用するユーザー名を指定します。 ユーザー名には Windows 統合認証を使用する場合、ドメインが含まれています**domain \username**です。 Basic を使用する場合、ダイジェスト認証ユーザー名が含まれない**ドメイン\\**です。<br /><br /> 場合にこのプロパティが値にのみ必要と**プロキシを使用して**が選択されています。<br /><br /> 型:文字列<br /><br /> 最小長: 0<br /><br /> 最大長: 256|  
    |**Password**|認証に使用するパスワードを指定します。<br /><br /> 場合にこのプロパティが値にのみ必要と**プロキシを使用して**が選択されています。<br /><br /> 型:文字列<br /><br /> 最小長: 0<br /><br /> 最大長: 256|  
  
5.  **SOAP トランスポートのプロパティ** ダイアログ ボックスで、 **Web サービス** タブで、次の操作します。  
  
    |プロパティ|目的|  
    |--------------|----------------|  
    |**オーケストレーション Web ポート**|記載されている Web サービス URL で公開される Web サービスを使用するように指定、**全般**タブです。<br /><br /> これが既定の設定です。|  
    |**アセンブリ名**|Web サービスのプロキシを含んでいるアセンブリの名前を指定します。 アセンブリを検索する参照ボタンをクリックして、このフィールドを設定できます。 アセンブリを選択すると、このボックスにアセンブリの完全修飾名が設定されます。 **注:**指定したアセンブリがすべて存在する必要があります[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]実行時にします。|  
    |**型名**|呼び出す Web メソッドを含むクラスの名前を指定します。 このクラスは、アセンブリに含まれている型の一覧から選択できます。|  
    |**メソッド名**|リスト ボックスに表示されているいずれかのメソッドを指定するか、[後で指定する] を選択します。 [後で指定する] を選択した場合は、パイプライン コンポーネントなど、他の方法で Web メソッドを設定する必要があります。 このシナリオでは、web メソッドを Soap アダプターを記述する必要があります**MethodName**コンテキスト プロパティです。|  
    |**SOAP 1.2**|SOAP 1.2 プロトコルをサポートするプロキシ コードを生成する場合に指定します。 このオプションをオフのままにした場合は、SOAP 1.1 準拠のプロキシ コードが生成されます。<br /><br /> 既定値: オフ|  
  
6.  をクリックして**[ok]**と**OK**もう一度設定を保存します。  
  
## <a name="see-also"></a>参照  
 [Web サービスの公開](../core/publishing-web-services.md)