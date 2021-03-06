---
title: シングル サインオンと BizTalk Adapter TIBCO Rendezvous for |Microsoft ドキュメント
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 52e698bb-38ba-4a12-b15a-d1581061d62f
caps.latest.revision: 6
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 310a3448acd8bd70e617a9a5af650b55a12c9007
ms.sourcegitcommit: dd7c54feab783ae2f8fe75873363fe9ffc77cd66
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2017
ms.locfileid: "24013442"
---
# <a name="single-sign-on-and-biztalk-adapter-for-tibco-rendezvous"></a>シングル サインオンと BizTalk Adapter for TIBCO Rendezvous

## <a name="overview"></a>概要
シングル サインオン (SSO) を Microsoft BizTalk Adapter for TIBCO Rendezvous を使用するときに、アダプターは SSO 資格情報データベースから資格情報を取得します。そのためでサーバー システムのログオン資格情報を入力する必要はありません、**トランスポートのプロパティ**ウィンドウです。  
  
 デザイン時には、アダプターが、BizTalk Server プロジェクトを開始したユーザーのコンテキストで (指定された関連アプリケーションの) システムの資格情報を取得します。 このユーザーは、アプリケーション ユーザーである必要があります。 実行時には、SSO を使用するときにパススルーのシナリオで受信場所として [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] HTTP 受信アダプターを使用してください。  
  
## <a name="processing-requests"></a>要求の処理  
 インターネット インフォメーション サービス (IIS) は、Web クライアントから HTTP 要求を受信すると、ユーザーを認証します。 ISAPI 拡張機能では、Windows ユーザーを偽装し、ストアを呼び出して、SSO 資格情報を暗号化されたチケットを取得します。 このチケットは、SSOTicket プロパティとしてメッセージのコンテキストに保存されます。  
  
 次に、メッセージがメッセージ ボックス データベースに転送されます。 BizTalk Adapter for TIBCO Rendezvous は、メッセージ ボックス データベースからメッセージを受信すると、暗号化されたチケットと関連アプリケーション名を指定して `ValidateAndRedeemTicket` を呼び出し、ログオン資格情報を SSO ストアから取得します。 その後、外部の資格情報を使用してシステムに接続し、要求が処理されます。  
  
> [!NOTE]
>  SSO の構成は BizTalk Server のセットアップの一部として行います。 SSO エラーが発生した場合は、ときに使用したドメイン アカウント BizTalk Server を構成したように、エンタープライズ SSO サービスの機能に影響を確認します。 SSO はドメイン アカウントでのみ機能します。  
  
## <a name="see-also"></a>参照  
 [関連アプリケーションの作成](../core/creating-affiliate-applications1.md)   
[セキュリティ](../core/security-in-biztalk-adapter-for-tibco-rendezvous.md)