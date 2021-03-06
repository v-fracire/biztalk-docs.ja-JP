---
title: '手順 2: サーバー上の NLB の構成 |Microsoft ドキュメント'
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Network Load Balancing
- configuring, NLB
- NLB
ms.assetid: 30b2f645-b495-49a5-852b-cf89d25fd2b7
caps.latest.revision: 6
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: a6d174ba336a94d44aaffdb2605542035304d9ff
ms.sourcegitcommit: 3fc338e52d5dbca2c3ea1685a2faafc7582fe23a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/01/2017
ms.locfileid: "26006523"
---
# <a name="step-2-configuring-nlb-on-the-servers"></a>手順 2: サーバーで NLB を構成します。
リストにログインをベース プラットフォームをインストールして、適切なネットワークの設定で、サーバーを構成した後 (を参照してください[手順 1: 基本プラットフォームをインストールする](../../adapters-and-accelerators/accelerator-swift/step-1-installing-the-base-platform.md))、BizTalk HTTP フロント エンド サーバーと、BizTalk で負荷分散を有効にする必要がありますメッセージング サーバー。 1 つまたは複数 BizTalk HTTP フロント エンド サーバー 1 台以上の BizTalk メッセージのサーバーから別のコンピューターにインストールされている場合にのみ、この手順が必要です。  
  
 クライアント コンピューター (Internet Explorer のユーザーが MRSR サイトを参照) と MRSR サーバー間および MRSR サーバーおよびメッセージング サーバーとの間の高可用性通信を保証する負荷分散します。  
  
 負荷分散、**パブリック**イントラネット ユーザーがこれらのコンピューター上の IIS Web サーバーに接続できるようにする HTTP フロント エンド サーバーのインターフェイスが必要です。 負荷分散、**プライベート**メッセージング サーバーがこれらのコンピューターで web サービスにお問い合わせを有効にする HTTP フロント エンド サーバーのインターフェイスが必要です。  
  
 メッセージングのサーバーで次の 2 つのサーバーがあると仮定すると負荷分散の構成で、**プライベート**ネットワーク アダプター。  
  
 詳細については、BizTalk Server の展開ガイドを参照してください。