---
title: "バッチ処理オーケストレーションでバッチ送信中に永続化例外が発生しました |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: cf6e832f-9d01-46e7-aaf5-2b402d509fac
caps.latest.revision: "9"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 7eae4f48209dc4f5afefbc69c40706a31f2b00b7
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="a-persistence-exception-has-occurred-during-the-batch-submission-in-the-batching-orchestration"></a>バッチ処理オーケストレーションでのバッチ送信中に永続化例外が発生しました
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]|  
|製品バージョン|[!INCLUDE[btsEDIVersion](../includes/btsediversion-md.md)]|  
|イベント ID|-|  
|イベント ソース|[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] EDI|  
|コンポーネント|バッチ処理エンジン|  
|シンボル名|PersistenceExceptionOccured|  
|メッセージ テキスト|バッチ処理オーケストレーションでのバッチ送信中に永続化例外が発生しました。 バッチ Id = {0}、ErrorMessage {1} を = です。 送信ポートのサブスクリプションを確認して修正してください。|  
  
## <a name="explanation"></a>説明  
 このエラー/警告/情報イベントは、インターチェンジをサブスクライブした送信ポートがなかったため、BizTalk Server が、バッチ化されたインターチェンジを送信できなかったことを示します。  
  
## <a name="user-action"></a>ユーザーの操作  
 このエラーを解決するには、送信ポートの次のフィルターのプロパティを設定して、送信ポートがサブスクライブをバッチにことを確認します。 EDI です。DestinationPartyName = \<PartyName >、EDI です。BatchEncodingType = EDIFACT または X12、および EDI です。ToBeBatched = False。