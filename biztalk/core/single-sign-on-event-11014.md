---
title: 'シングル サインオン: イベント 11014 |Microsoft Docs'
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 71e4c9bd-8bda-46ca-9e76-f7b4fa033167
caps.latest.revision: 6
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 8e86642a7f62b53d45f20e140131d6a12d0771ec
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "37001137"
---
# <a name="single-sign-on-event-11014"></a>シングル サインオン: イベント 11014
## <a name="details"></a>詳細  
  
|                 |                                                                                                                                                          |
|-----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
|  製品名   |                                                                エンタープライズ シングル サインオン                                                                 |
| 製品バージョン |                                                [!INCLUDE[btsSSOVersion](../includes/btsssoversion-md.md)]                                                |
|    イベント ID     |                                                                          11014                                                                           |
|  イベント ソース   |                                                                          ENTSSO                                                                          |
|    コンポーネント    |                                                                           なし                                                                            |
|  シンボル名  |                                                                  SSO_ERROR_ACCESS_CHECK                                                                  |
|  メッセージ テキスト   | アクセス確認が失敗しました。%r<br /><br /> クライアント ユーザー: %1\\% 2 %r<br /><br /> アプリケーション名: % 3 %r<br /><br /> 追加データ: % 4 %r<br /><br /> エラー コード: %5 |
  
## <a name="explanation"></a>説明  
 表示されたクライアントおよびアプリケーションについてアクセス確認が失敗しました。  
  
## <a name="user-action"></a>ユーザーの操作  
 追加情報によって、問題を解決できるようになります。 今後、このエラーを回避するために、監査レベルを低くすることもできます。