---
title: クライアント ユーティリティを使用して SSO サーバーを設定する方法 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- applications [SSO], selecting servers
- managing [SSO applications], selecting servers
- SSOClient [SSO], selecting servers
ms.assetid: a0f1038c-60c9-4e9d-a730-1ecfa036743b
caps.latest.revision: 8
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 8f212bb5e6601274a473c6f9854d5e23af9715cd
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "37008867"
---
# <a name="how-to-set-the-sso-server-using-the-client-utility"></a>クライアント ユーティリティを使用して SSO サーバーを設定する方法
ssoclient を使用するたびに、まず、ユーザーが構成情報を含む正しいシングル サインオン サーバーを参照するように設定する必要があります。  
  
### <a name="to-set-the-sso-server-for-a-user-using-the-client-utility"></a>クライアント ユーティリティを使用してユーザーに対して SSO サーバーを設定するには  
  
1. **開始** メニューのをクリックして**実行**、し、入力**cmd**します。  
  
2. コマンド ラインで、エンタープライズ シングル サインオンのインストール ディレクトリに移動します。 既定のインストール ディレクトリは*\<ドライブ\>*: \Program Files\Common \enterprise シングル サインオンします。  
  
3. 型<strong>ssoclient – サーバー *\<シングル サインオン サーバー\></strong><em>ここで、 \<</em>シングル サインオン サーバー\>* が、ユーザー シングル サインオン サーバーの名前に接続しようとします。  
  
   > [!NOTE]
   >  ユーザー アカウント制御 (UAC) をサポートするシステムでは、管理者特権を使用してこのツールを実行することが必要な場合があります。  
  
## <a name="see-also"></a>参照  
 [SSO 関連アプリケーション](../core/sso-affiliate-applications.md)   
 [関連アプリケーションの管理](../core/managing-affiliate-applications.md)