---
title: 'シングル サインオン: イベント 10603 |Microsoft Docs'
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 139d1eb5-af88-4216-9604-c052f3db13c9
caps.latest.revision: 7
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 5416ae8a2dcfdf5a3da6d8c1d00eb5a556fc3599
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36970067"
---
# <a name="single-sign-on-event-10603"></a>シングル サインオン: イベント 10603
## <a name="details"></a>詳細  
  
|                 |                                                                                                                                                    |
|-----------------|----------------------------------------------------------------------------------------------------------------------------------------------------|
|  製品名   |                                                             エンタープライズ シングル サインオン                                                              |
| 製品バージョン |                                             [!INCLUDE[btsSSOVersion](../includes/btsssoversion-md.md)]                                             |
|    イベント ID     |                                                                       10603                                                                        |
|  イベント ソース   |                                                                       ENTSSO                                                                       |
|    コンポーネント    |                                                                        なし                                                                         |
|  シンボル名  |                                                                 SSO_WARN_DB_ACCESS                                                                 |
|  メッセージ テキスト   | SSO データベースにアクセスできませんでした。 この状況が継続すると、SSO サービスはオフラインになります。%r<br /><br /> %1.%r<br /><br /> SQL エラー コード: %2 |
  
## <a name="explanation"></a>説明  
 SSO データベースを利用できません。  
  
## <a name="user-action"></a>ユーザーの操作  
 警告に含まれる SQL エラー コードを確認します。 これによってガイダンスが示される場合があります。 ガイダンスが示されない場合は、マイクロソフト製品サポート サービスにお問い合わせください。