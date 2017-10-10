---
title: "プログラミングのシングル サインオンの概要 |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2a0a3978-cdbf-4703-9d1d-23e0f4923c9c
caps.latest.revision: "7"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: c5f8ffa7463e4c1fbdd7231cf87abea751fea3d3
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="programming-single-sign-on-overview"></a>プログラミングのシングル サインオンの概要
複数の異なるアプリケーションに依存するビジネス プロセスでは、場合によっては、複数の異なるセキュリティ ドメインの操作が必要になります。 たとえば、Microsoft Windows オペレーティング システムのアプリケーションにアクセスするときは、それに応じたセキュリティ資格情報のセットを使用する必要があり、IBM メインフレームのアプリケーションにアクセスするときは、別の資格情報を使用する必要があります。 このような多くの資格情報を操作することは、ユーザーにとって困難です。このため、プロセスを自動化する必要性が高まっています。 この問題に対処するために、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] では、エンタープライズ シングル サインオン (SSO) が提供されます。 SSO では、Windows ユーザー ID を Windows 以外のユーザー資格情報にマップすることができます。 このサービスによって、さまざまなシステムのアプリケーションを使用するビジネス プロセスの作業を単純化できます。  
  
 SSO を使用する場合、管理者は、関連アプリケーションを定義します。各関連アプリケーションは、Windows 以外のシステムまたはアプリケーションを表します。 関連アプリケーションには、IBM メインフレームで実行されている CICS (Customer Information Control System) アプリケーション、UNIX で実行されている SAP ERP システム、またはその他の種類のソフトウェアがあります。 これらの各アプリケーションには、認証用の独自のメカニズムがあるので、各アプリケーションには一意の資格情報が必要です。  
  
 SSO は、ユーザーの Windows ユーザー ID と、1 つ以上の関連アプリケーションに関連付けられている資格情報との間の暗号化されたマッピングを格納します。 これらのリンク ペアは、SSO データベースに格納されます。 SSO は、2 つの方法で SSO データベースを使用します。 最初の方法と呼ばれる*Windows 側開始シングル サインオンが*、する関連アプリケーションをユーザーがアクセスを決定するユーザーの ID を使用します。 たとえば、Windows ユーザー アカウントを、リモート AS/400 サーバーで実行されている DB2 データベースにアクセスするための資格情報にリンクできます。 呼ばれる 2 番目の方法は、*ホスト側開始シングル サインオン*、逆の順序では機能: どのようなリモート アプリケーションが、指定したユーザー ID、およびそのアカウントに対応する権限へのアクセスを持つを特定します。 たとえば、リモート アプリケーションを、Windows ネットワークの管理者権限を持つユーザー アカウントにアクセスするための資格情報にリンクできます。  
  
 また、SSO には、さまざまな操作を実行する管理ツールも含まれています。 SSO データベースで実行されるすべての操作は、監査されます。たとえば、管理者がこれらの操作を監視してさまざまな監査レベルを設定できるツールが提供されています。 管理者が特定の関連アプリケーションを無効にできるツールもあります。また、ユーザーに対して個別のマッピングの有効化や無効化を行うなど、さまざまな機能を持つツールが用意されています。 エンド ユーザーが独自の資格情報とマッピングを構成できるクライアント プログラムもあります。  
  
 ローカル システムはリモート システムへのログオンに必要な資格情報を認識しなければならない、というシングル サインオンの管理要件があります。 同様に、リモート システムは、ローカル システムの資格情報を認識する必要があります。 このため、資格情報を更新する場合 (ローカル コンピューターのパスワードを更新する場合など)、更新した内容をリモート システムに通知する必要もあります。 エンタープライズ全体のパスワードを同期するコンポーネントをデザインすると呼びます、*パスワード同期アダプター*です。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [シングル サインオン インターフェイス](../core/single-sign-on-interface.md)  
  
 [シングル サインオン アプリケーション](../core/single-sign-on-applications.md)  
  
 [シングル サインオンをプログラミングする前に知っておく必要があります。](../core/what-you-should-know-before-programming-single-sign-on.md)  
  
 [シングル サインオンのサポートされているプラットフォーム](../core/supported-platforms-for-single-sign-on.md)