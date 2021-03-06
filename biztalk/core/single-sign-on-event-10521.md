---
title: 'シングル サインオン: イベント 10521 |Microsoft Docs'
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 00d427ff-74d0-45f5-bb55-ab12b564d767
caps.latest.revision: 13
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 8af1b2ac8d2ac3645db6a6a80146832378aececf
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "37008571"
---
# <a name="single-sign-on-event-10521"></a>シングル サインオン: イベント 10521
## <a name="details"></a>詳細  

|                 |                                                                       |
|-----------------|-----------------------------------------------------------------------|
|  製品名   |                       エンタープライズ シングル サインオン                       |
| 製品バージョン |      [!INCLUDE[btsSSOVersion](../includes/btsssoversion-md.md)]       |
|    イベント ID     |                                 10521                                 |
|  イベント ソース   |                                ENTSSO                                 |
|    コンポーネント    |                                  N\A                                  |
|  シンボル名  |                     SSO_ERROR_SECRETS_NOT_LOADED                      |
|  メッセージ テキスト   | マスター シークレット サーバーのレジストリからシークレットを読み込めませんでした。 |

## <a name="explanation"></a>説明  
 このエラー イベントは、マスター シークレットをレジストリから取得できない場合にマスター シークレット サーバーで発生します。 イベント ログに詳細を示す関連エラー メッセージが記録されている場合があります。 このエラーの最も大きな原因は、SSO サービスがレジストリにアクセスしようとしたときに、アクセス許可エラーまたは暗号化エラーが発生していることです。 これは、SSO サービス アカウントが変更されたときに発生する可能性があります。 マスター シークレットは、SSO サービス アカウントの ID に基づくキーで暗号化されています。 このアカウントが変更されると、レジストリ内にある既存のマスター シークレットの暗号化を解除できなくなります。  

## <a name="user-action"></a>ユーザーの操作  
 このエラーを解決するには、次の操作を行います。  

- SSO サービス アカウントを変更する場合は、マスター シークレットをバックアップし、SSO サービス アカウントを変更した後、マスター シークレットを復元します。 これによって、マスター シークレットを復元することができ、このエラーが修正されます。  

  詳細については、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] ヘルプの次の情報を参照してください:   

- [マスター シークレット サーバー](../core/master-secret-server.md)  

- [マスター シークレットの管理](../core/managing-the-master-secret.md)  

- [SSO の構成](../core/configuring-sso.md)  

- [SSO のセキュリティに関する推奨事項](../core/sso-security-recommendations.md)
