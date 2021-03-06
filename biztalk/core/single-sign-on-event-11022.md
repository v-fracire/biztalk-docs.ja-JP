---
title: 'シングル サインオン: イベント 11022 |Microsoft Docs'
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c65ca12b-dda8-408b-9512-39df6f8e035b
caps.latest.revision: 6
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 5c21128bb7804eae88eacc87cffb0fd0d2c0490c
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36966787"
---
# <a name="single-sign-on-event-11022"></a>シングル サインオン: イベント 11022
## <a name="details"></a>詳細  
  
|                 |                                                                                                                                                                                                                                                                                                                                                                                                |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  製品名   |                                                                                                                                                                                   エンタープライズ シングル サインオン                                                                                                                                                                                    |
| 製品バージョン |                                                                                                                                                                   [!INCLUDE[btsSSOVersion](../includes/btsssoversion-md.md)]                                                                                                                                                                   |
|    イベント ID     |                                                                                                                                                                                             11022                                                                                                                                                                                              |
|  イベント ソース   |                                                                                                                                                                                             ENTSSO                                                                                                                                                                                             |
|    コンポーネント    |                                                                                                                                                                                              なし                                                                                                                                                                                               |
|  シンボル名  |                                                                                                                                                                   SSO_WARN_EXTERNAL_TO_EXTERNAL_MAPPING_CONFLICT_NOT_ALLOWED                                                                                                                                                                   |
|  メッセージ テキスト   | 外部パスワード変更により、異なる外部アカウントが変更される可能性がありました。%r<br /><br /> この外部システムのアダプターは、マッピングの競合を許可しないよう構成されているため、実行できません。%r<br /><br /> 追跡 ID: %1 %r<br /><br /> アダプター: % 2 %r<br /><br /> Windows アカウント: % 3 %r<br /><br /> 外部アカウント 1: % 4 %r<br /><br /> 外部アカウント 2: %5 |
  
## <a name="explanation"></a>説明  
 これは、別の外部アカウントを変更する可能性があった外部パスワード変更の失敗を通知する情報メッセージです。  
  
## <a name="user-action"></a>ユーザーの操作  
 変更は行われませんでしたが (このシステムはマッピングの競合を許可しないように構成されているため)、この試みが事前にわかっていて承認したものであることを直ちに確認する必要があります。 そうである場合は、何もする必要はありません。 そうでなかった場合は、この変更がどこで行われたのかを調べ、システム内の安全な場所であることを確認してください。