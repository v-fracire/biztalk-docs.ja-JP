---
title: ファイルをプログラムで作成する受信場所または送信ポート |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 558a414c-60bc-4f62-9397-a023ed4937fb
caps.latest.revision: 3
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 424c2c61655da599c4f437d3fdbf200df29d4e13
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "37013715"
---
# <a name="programmatically-create-the-file-receive-location-or-send-port"></a>ファイルをプログラムで作成する受信場所または送信ポート
ファイルを作成する方法は、受信ポートと送信ポートをプログラムを使用します。 使用する、[!INCLUDE[btsBizTalkServerAdminConsoleui](../includes/btsbiztalkserveradminconsoleui-md.md)]に移動して、[ファイル アダプターを構成する](../core/configure-the-file-adapter.md)します。

ファイル アダプターは、その構成情報を SSO データベースに格納します。 受信場所を構成し、オブジェクト モデルをプログラムで、BizTalk エクスプ ローラーを使用してポートに送信できます。 
 
## <a name="create-the-receive-location"></a>受信場所を作成します。

BizTalk エクスプローラ オブジェクト モデルを公開、**という**構成インターフェイスを含む、 **TransportTypeData**読み取り/書き込みプロパティ。 このプロパティでは、名前と値の組の XML 文字列の形式で、ファイルの受信場所の構成プロパティ バッグを指定できます。  
  
**TransportTypeData**のプロパティ、**という**インターフェイスを設定する必要はありません。 このプロパティを設定しない場合、ファイルの受信場所の構成の既定値が使用されます。  
  
 次の表に、ファイルの受信場所をプログラムから設定できる構成プロパティを示します。  
  
|プロパティ名|型|説明|制限|コメント|  
|-------------------|----------|-----------------|------------------|--------------|  
|**FileNetFailRetryCount**|Long|ネットワーク共有上の受信場所が一時的に使用できない場合に、アクセスを試行する回数。|Integer<br /><br /> 最小値: 0<br /><br /> 最大値: max_long です|値を指定しない場合は、既定値 5 回が使用されます。|  
|**FileNetFailRetryInterval**|Long|ネットワーク共有上の受信場所が一時的に使用できない場合に、アクセスを再試行する分単位の時間間隔。|Integer<br /><br /> Minimumvalue: 0<br /><br /> 最大値: max_long です|値を指定しない場合は、既定値 5 分が使用されます。|  
|**BatchSize**|Long|この受信場所がサーバーに一度に送信できるファイルの数。|Integer<br /><br /> 最小値: 1<br /><br /> 最大値: 256|値を指定しない場合は、既定値 20 ファイルが使用されます。|  
|**FileMask**|String|受信場所で使用するファイル マスク。|String<br /><br /> FilePath と FileMask を組み合わせた長さは 256 文字以下にしてください。|値を指定しない場合は、既定値 *.xml が使用されます。|  
|**ファイル パス**|String|受信場所で監視するフォルダーのパス。|String<br /><br /> 必須<br /><br /> FilePath と FileMask を組み合わせた長さは 256 文字以下にしてください。|指定する必要があります**重要:** ファイル フォルダーは、受信場所で構成された受信ハンドラー資格情報の書き込みアクセス許可がある必要と受信場所を作成します。|  
|**ユーザー名**|String|フォルダーへのアクセスに使用するアカウントのユーザー名。|最小の長さ: 0<br /><br /> 最大長: 256|ユーザー名とパスワードをどちらも指定しない場合、ホストの資格情報が使用されます。<br /><br /> Null (vt="1") の場合、構成データベースに格納された値が使用されます。|  
|**Password**|String|フォルダーへのアクセスに使用するアカウントのパスワード。|最小の長さ: 0<br /><br /> 最大長: 256|ユーザー名とパスワードをどちらも指定しない場合、ホストの資格情報が使用されます。<br /><br /> Null (vt="1") の場合、構成データベースに格納された値が使用されます。|  
  
 次のコード例は、プロパティの設定に使用する XML 文字列の形式を示しています。  
  
```  
<CustomProps>  
   <FilePath vt="8">C:\Temp</FilePath>  
   <BatchSize vt="19">20</BatchSize>  
   <FileMask vt="8">*.xml</FileMask>  
   <FileNetFailRetryCount vt="19">5</FileNetFailRetryCount>  
   <FileNetFailRetryInterval vt="19">5</FileNetFailRetryInterval>  
   <Username vt=”8”>MyDomain\MyUsername</Username>  
   <Password vt=”8”>PASSWORD</Password>  
</CustomProps>  
  
```  

## <a name="create-the-send-port"></a>送信ポートを作成します。

構成情報はカスタム XML プロパティ バッグに保存されます。 `bts_file_properties.xsd`ファイル送信ハンドラのプロパティ スキーマ ファイル アダプターに固有のプロパティを定義します。 これらのプロパティは、サーバー内のアダプタ固有の情報を渡すためだけでなく、ファイル送信ポートを構成する場合にも使用します。  
  
BizTalk エクスプローラ オブジェクト モデルを公開、 **ITransportInfo**が含まれているファイル送信ポートのアダプターの構成インターフェイス、 **TransportTypeData**読み取り/書き込みプロパティ。 このプロパティでは、名前と値の組の XML 文字列の形式でファイル送信ハンドラの構成プロパティ バッグを指定できます。  
  
 設定、 **TransportTypeData**のプロパティ、 **ITransportInfo**インターフェイスは必要ありません。 このプロパティを設定しない場合、ファイル送信ハンドラの構成の既定値が使用されます。  
  
 次の表に、BizTalk エクスプローラ オブジェクト モデルでファイル送信ハンドラの場所をプログラムから設定できる構成プロパティを示します。  
  
|プロパティ名|型|説明|  
|-------------------|----------|-----------------|  
|**CopyMode**|Long|ファイルにメッセージを書き込むときに使用するコピー モードを定義します。 有効な値は、<br /><br /> **(0) を追加します。** ファイルが存在する場合は、ファイル送信ハンドラがファイルを開き、ファイルの末尾にメッセージを追加します。 ファイルが存在しない場合は、ファイル送信ハンドラが新しいファイルを作成します。<br /><br /> **新しい (1) を作成します。** : ファイルが存在しない場合は、ファイル送信ハンドラが新しいファイルを作成し、そのファイルにメッセージを書き込みます。 ファイルが存在する場合は、ファイル送信ハンドラがエラーを報告し、送信ポートの通常のアダプタ再試行ロジックに従ってメッセージを処理します。 これはファイル送信ハンドラの既定のコピー モードです。<br /><br /> **(2) を上書きします。** ファイルが存在する場合は、ファイル送信ハンドラがファイルを開き、ファイルの内容を上書きします。 ファイルが存在しない場合は、ファイル送信ハンドラが新しいファイルを作成します。|  
|**AllowCacheOnWrite**|ブール値|ファイルにメッセージを書き込む際にファイル アダプタでファイル システム キャッシュを使用するかどうかを定義します。<br /><br /> 有効な値は、<br /><br /> **True (-1)** : ファイル アダプタは、出力ファイルに書き込むときにファイル システムのキャッシュを使用します。<br /><br /> **False (0)** ファイル送信ハンドラは出力ファイルに書き込むときにファイル システムのキャッシュを使用していません。|  
|**書き込み中に一時ファイルの使用**|ブール値|最初に一時ファイルに出力ファイルの書き込みし、書き込み操作が完了したらファイルを変更するかどうかを定義します。 このオプションが有効になっているかどうかは、一時ファイルは、拡張機能の作成は**BTS-WIP**します。<br /><br /> 有効な値は、<br /><br /> **True (-1)** : ファイル アダプタはターゲット フォルダに書き込むときに一時ファイルを作成します。<br /><br /> **False (0)** : ファイル アダプタはターゲット フォルダに書き込むときに一時ファイルを作成できません。 **注:** ときにこのオプションは使用可能なのみ、 **CopyMode**の値に設定されて**新しい (1) を作成する**します。|  
  
 いずれの構成プロパティもメッセージ コンテキストに値がない場合は、ファイル送信ハンドラでは、既定値が使用されます。  
  
 構成プロパティは、メッセージ コンテキストでプログラムによって設定できます。 これらのプロパティは、オーケストレーションまたはカスタム パイプライン コンポーネントで設定できます。 プロパティを使用するときは、次の規則が適用されます。  
  
- 構成プロパティがオーケストレーション、または受信パイプラインのカスタム パイプライン コンポーネントで設定されているとき  
  
  -   メッセージを送信する場合は、静的な送信ポート、プロパティの値は、その送信ポート用に構成された値で上書きされます。  
  
  -   動的送信ポートにメッセージを送信する場合、プロパティの値は上書きされません。  
  
- 構成プロパティは、送信パイプラインでカスタム パイプライン コンポーネントで設定されます。 場合、  
  
  -   メッセージを送信する送信ポートが静的か動的かにかかわらず、プロパティ値は上書きされません。  
  
  次のコード例は、プロパティの設定に使用できる XML 文字列の形式を示しています。  
  
```  
<CustomProps>  
   <CopyMode vt="19">0</CopyMode>  
   <AllowCacheOnWrite vt="11">-1</AllowCacheOnWrite>  
   <UseTempFileOnWrite vt="11">-1</UseTempFileOnWrite>  
</CustomProps>  
```  


