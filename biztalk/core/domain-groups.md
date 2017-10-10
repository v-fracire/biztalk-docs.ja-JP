---
title: "ドメイン グループ |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: domain groups
ms.assetid: 9adc090e-e18c-46b6-b985-49b200d42966
caps.latest.revision: "11"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 52fc5cc05718aa6d9e0ca89bc48467052fb916a5
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="domain-groups"></a>ドメイン グループ
また、ドメイン グループ アカウントとドメイン ユーザー アカウントは、単一および複数の両方のコンピュータ構成でサポートされます。 複数コンピュータ構成の場合、このセクション、およびインストール ガイドの「マルチサーバー環境に関する注意点 (Considerations for Multiserver Environments)」で示す要件を満たす必要があります。 詳細については、次を参照してください。 [BizTalk Server 2013 および 2013 R2 のインストールの概要](http://msdn.microsoft.com/library/8041926c-cfc9-4eaf-9c28-a2c6e8015bc5)です。  
  
-   BizTalk Server の構成にドメイン グループを使用する場合は、BizTalk Server を構成する前に、グループを手動で作成しておく必要があります。 構成マネージャーでは、ドメイン グループを作成できません。  
  
-   ドメイン グループやユーザー アカウントを作成した後でグループ関連に従って、適切なグループにユーザー アカウントを追加[Windows グループと BizTalk Server でのユーザー アカウント](../core/windows-groups-and-user-accounts-in-biztalk-server.md)です。  
  
-   使用して **\<DomainName >\\< ユーザー名\>** Configuration Manager のドメイン アカウント情報を指定する場合。  
  
-   BizTalk Server では、すべてのクラスタリング シナリオに対応するドメイン アカウントが必要です。 クラスタ化された SQL Server やクラスタ化された SSO サーバー (マスタ シークレット サーバー) で、ローカル アカウントを使用することはできません。  
  
-   BizTalk Server をインストールおよび構成する管理者は、SSO 管理者 (マスタ シークレット サーバーを構成する場合のみ)、ローカル管理者、sysadmin SQL Server ロール、OLAP 管理者といったグループのメンバである必要があります。  
  
> [!NOTE]
>  SSO 管理者と SSO 関連管理者の構成中にドメイン グループを指定し、その操作を行うための十分な権限がある場合、ドメイン グループは自動的に作成されます。 十分な権限がない場合は、これらのドメイン グループが既に存在することを確認します。  
  
## <a name="see-also"></a>参照  
 [ローカル グループ](../core/local-groups.md)   
 [BizTalk Server 2013 および 2013 R2 のインストール概要](http://msdn.microsoft.com/library/8041926c-cfc9-4eaf-9c28-a2c6e8015bc5)   
 [BizTalk Server の Windows グループ アカウントとユーザー アカウント](../core/windows-groups-and-user-accounts-in-biztalk-server.md)