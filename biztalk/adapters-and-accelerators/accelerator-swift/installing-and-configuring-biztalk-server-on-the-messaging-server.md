---
title: インストールして、メッセージング サーバーで BizTalk Server の構成 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- BizTalk Server, installing on BizTalk Messaging servers
- BizTalk Server, configuring
- BizTalk Messaging servers, configuring BizTalk Server
- BizTalk Messaging servers, installing BizTalk Server
ms.assetid: 8aaa1b97-90f0-4317-9403-ac8b5b9f80e3
caps.latest.revision: 10
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: b5f4013c1fe315646ea7a2ff34772169a03a2d66
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36989571"
---
# <a name="installing-and-configuring-biztalk-server-on-the-messaging-server"></a>インストールして、メッセージング サーバーで BizTalk Server の構成
このセクションでは、インストールを行う SWIFT ネットワークに接続するため、メッセージング サーバーとして使用する BizTalk Server を構成する方法について説明します。  

### <a name="to-install-and-configure-biztalk-server-on-the-messaging-server"></a>インストールして、メッセージング サーバーに BizTalk Server を構成するには  

1. カスタム インストール実行[!INCLUDE[btsBizTalkServerNoVersion](../../includes/btsbiztalkservernoversion-md.md)]他のアプリケーションで必要な場合は、EDI、ヒューマン ワークフロー サービス (HWS) および MRSR サイト以外のすべての機能を選択します。  

   > [!NOTE]
   >  1 台のコンピューターの展開でこのコンピューターは、HTTP フロント エンド サービスを実行しているものと同じコンピューターに注意してください。  

2. 構成を行う[!INCLUDE[btsBizTalkServerNoVersion](../../includes/btsbiztalkservernoversion-md.md)]します。  

   > [!NOTE]
   >  インストールしないメッセージがキューをインストールするため、 [!INCLUDE[btsBizTalkServerNoVersion](../../includes/btsbiztalkservernoversion-md.md)] MSMQT と呼ばれる MSMQ のバージョン。 MSMQT の詳細については、MSDN Web サイトで BizTalk メッセージ キュー アダプター (MSMQT) 構成を参照してください。 [ http://go.microsoft.com/fwlink/?LinkID=48875](http://go.microsoft.com/fwlink/?LinkID=48875)します。  

3. 必要な他の修正プログラムをインストール[!INCLUDE[A4SWIFT_CurrentVersion_abbrev](../../includes/a4swift-currentversion-abbrev-md.md)]インストール ガイドで利用可能な。 このパブリケーションの時に、必要な修正プログラムはありません。
