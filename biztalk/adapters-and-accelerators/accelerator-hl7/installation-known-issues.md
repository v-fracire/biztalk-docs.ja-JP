---
title: インストールの既知の問題 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b2f80ff9-b37c-49f8-8250-fcf3cec4c0fc
caps.latest.revision: 2
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 4f017fa273d91d1c40727ba34c6d047383054d52
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "37000923"
---
# <a name="installation-known-issues"></a>インストールの既知の問題
役立つ有用な情報は、インストールの問題を回避します。  
  
## <a name="prerequisites-for-installing-btahl7"></a>BTAHL7 のインストールの前提条件  
 インストールの前提条件[!INCLUDE[btaBTAHL7NoNumber](../../includes/btabtahl7nonumber-md.md)]次に示します。  
  
- 基本コンポーネント[!INCLUDE[btsBizTalkServerNoVersion](../../includes/btsbiztalkservernoversion-md.md)]、エンタープライズ シングル サインオン (SSO)、グループ、およびランタイムを含む、構成する必要があります。  
  
- インストールと構成 BTAHL7 のユーザーは、BizTalk 管理者グループのメンバーと BTAHL7 データが格納されている SQL Server の Administrators グループのメンバーである必要があります。
  
## <a name="sql-server-mixed-mode-not-supported"></a>SQL Server 混在モードがサポートされていません  
[!INCLUDE[btaBTAHL7NoNumber](../../includes/btabtahl7nonumber-md.md)]混在モードで SQL Server をサポートしていません。  
  
## <a name="repair-does-not-work-from-uninstallchange"></a>修復はアンインストールと変更からは機能しません  
ユーザー アクセス制御 (UAC) が有効になっているし、コントロール パネルを使用して、インストールを修復しようとする、修復は失敗します。 

Microsoft では、UAC を有効にしておくことをお勧めします。

 **解決方法**  
  
 実行、 [!INCLUDE[btaBTAHL7NoNumber](../../includes/btabtahl7nonumber-md.md)] setup.exe、および選択**修復**します。  
  
## <a name="see-also"></a>参照  
[Microsoft BizTalk Accelerator for HL7 のインストールまたはアップグレード](../../adapters-and-accelerators/accelerator-hl7/install-or-upgrade-microsoft-biztalk-accelerator-for-hl7.md)