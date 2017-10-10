---
title: "シングル サインオン: イベント 10520 |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 91662072-d87c-4290-8afb-2143143ee858
caps.latest.revision: "14"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 9349452d99518f210237c5e8dd0f945d1f92aa46
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="single-sign-on-event-10520"></a>シングル サインオン: イベント 10520
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|エンタープライズ シングル サインオン|  
|製品バージョン|[!INCLUDE[btsSSOVersion](../includes/btsssoversion-md.md)]|  
|イベント ID|10520|  
|イベント ソース|ENTSSO|  
|コンポーネント|N\A|  
|シンボル名|SSO_WARN_NO_SECRETS|  
|メッセージ テキスト|マスター シークレット サーバーのレジストリでシークレットが見つかりませんでした。 構成ツールを使用して、マスター シークレットを生成または復元してください。|  
  
## <a name="explanation"></a>説明  
 この警告イベントは、マスター シークレット サーバーのレジストリでシークレットが見つからなかったことを示します。 SSO マスター シークレットは、SSO マスター シークレット サーバーのレジストリに暗号化されて格納されます。 通常、現在のマスター シークレットと以前のマスター シークレットの 2 つのシークレットがレジストリに格納されています。 シークレットは、GUID (マスター シークレット ID) を使用して識別されます。 要求されたときに指定されたマスター シークレットがレジストリ内に見つからなかった場合、このエラー コードが返されます。  
  
## <a name="user-action"></a>ユーザーの操作  
 この警告を解決するには、次のいずれかの操作 (あるいは複数の操作) を行います。  
  
-   マスター シークレット サーバー名が正しく、想定どおりであることを確認します。  
  
-   マスター シークレット サーバー名が正しい場合は、マスター シークレットがマスター シークレット サーバーのレジストリ内に存在することを確認します。 マスター シークレットは、HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ENTSSO\SSOSS にあります (このキーは SSO マスター シークレット サーバー上にのみ存在します)。  
  
-   このキーがない場合、マスター シークレットは存在しません。 SSOSS の下に GUID という名前の 1 つまたは複数のキーに暗号化されたキーが含まれています。 これらのキーが存在しない場合、マスター シークレットは存在していません。 マスター シークレットは GUID (マスター シークレット ID) によって識別されるので、これらの GUID (存在する場合) は要求されたシークレットのマスター シークレット ID と一致している必要があります。 GUID という名前のキーが存在していても、要求されたマスター シークレット ID と一致しない場合は、レジストリ内のマスター シークレットと、SSO データベース (SSODB) 内のデータを暗号化するために使用されたシークレットが混同されています。 この場合は別のマスター シークレットを復元することが必要になる、つまり下位レベルのバックアップから SSODB が復元されている可能性があります。 マスター シークレットがまったく存在しない場合は、SSO 構成ツール (コマンド ラインまたは MMC) を使用してバックアップから復元するか、新しいシークレットを生成することができます。 これが新しいインストールであり、SSO データベース内に既存の暗号化されたデータが存在しない場合は、通常、新しいマスター シークレットを生成するだけで済みます。 マスター シークレットは、通常、最初の構成を行うときに初めて生成されます。  
  
 詳細については、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] ヘルプの次の情報を参照してください:   
  
-   [マスター シークレット サーバー](../core/master-secret-server.md)  
  
-   [マスタ シークレットの管理](../core/managing-the-master-secret.md)  
  
-   [SSO を構成します。](../core/configuring-sso.md)