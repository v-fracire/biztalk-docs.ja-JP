---
title: 'シングル サインオン: イベント 10539 |Microsoft Docs'
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a67f5719-da7c-4ae0-a6fe-ff7b653a184d
caps.latest.revision: 12
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: f7934b3011af2656f413270b4d249ca4f7f96bae
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "37006284"
---
# <a name="single-sign-on-event-10539"></a>シングル サインオン: イベント 10539
## <a name="details"></a>詳細  

|                 |                                                            |
|-----------------|------------------------------------------------------------|
|  製品名   |                 エンタープライズ シングル サインオン                  |
| 製品バージョン | [!INCLUDE[btsSSOVersion](../includes/btsssoversion-md.md)] |
|    イベント ID     |                           10539                            |
|  イベント ソース   |                           ENTSSO                           |
|    コンポーネント    |                             CO                             |
|  シンボル名  |              SSO_WARN_SSO_TICKETS_NOT_ALLOWED              |
|  メッセージ テキスト   |        SSO システムに対してチケットが有効になっていません。         |

## <a name="explanation"></a>説明  
 この警告イベントは、SSO チケットの使用が有効になっていないことを示します。 SSO チケットの使用の許可は、SSO システムのオプション機能です。 この機能が SSO システムで有効になっていませんでした。  

## <a name="user-action"></a>ユーザーの操作  
 この警告を解決するには、次の操作を行います:   

- SSO 管理者に問い合わせて、SSO システムのチケットを有効にします。 SSO 管理ツール (GUI またはコマンド ライン) を使用して行うことができます。  

  詳細については、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] ヘルプの次の情報を参照してください:   

- [SSO チケットを構成する方法](../core/how-to-configure-the-sso-tickets.md)  

- [SSO の使用](../core/using-sso.md)
