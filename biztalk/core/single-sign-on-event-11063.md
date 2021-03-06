---
title: 'シングル サインオン: イベント 11063 |Microsoft Docs'
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c84f91de-221d-43c4-8d23-3d1b7fd29cf7
caps.latest.revision: 7
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 5a653b8c5cf27925c65d8922a5a561855fdb6a4c
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36975571"
---
# <a name="single-sign-on-event-11063"></a>シングル サインオン: イベント 11063
## <a name="details"></a>詳細  
  
|                 |                                                            |
|-----------------|------------------------------------------------------------|
|  製品名   |                 エンタープライズ シングル サインオン                  |
| 製品バージョン | [!INCLUDE[btsSSOVersion](../includes/btsssoversion-md.md)] |
|    イベント ID     |                           11063                            |
|  イベント ソース   |                           ENTSSO                           |
|    コンポーネント    |                            なし                             |
|  シンボル名  |          SSO_ERROR_PS_MIIS_CALLBACK_ACCESS_DENIED          |
|  メッセージ テキスト   |      (MIIS に対する) パスワード同期サーバーのアクセスが拒否されました。%r      |
  
## <a name="explanation"></a>説明  
 MIIS コールバックのアクセスが拒否されました。 このエラーの原因として最も可能性が高いのは、ENTSSO システムと MIIS の間での Kerberos 認証の使用の失敗です。  
  
## <a name="user-action"></a>ユーザーの操作  
 ENTSSO システムが Kerberos 認証を使用していることを確認します。 詳細については、次を参照してください。 [SSO のセキュリティに関する推奨事項](../core/sso-security-recommendations.md)します。