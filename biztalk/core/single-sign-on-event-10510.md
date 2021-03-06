---
title: 'シングル サインオン: イベント 10510 |Microsoft Docs'
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 4553ad4c-9553-4b8b-b3a3-72aed2a61202
caps.latest.revision: 15
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 6043dabf397bb987b58707885cbf91d36de50eab
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "37011347"
---
# <a name="single-sign-on-event-10510"></a>シングル サインオン: イベント 10510
## <a name="details"></a>詳細  

|                 |                                                            |
|-----------------|------------------------------------------------------------|
|  製品名   |                 エンタープライズ シングル サインオン                  |
| 製品バージョン | [!INCLUDE[btsSSOVersion](../includes/btsssoversion-md.md)] |
|    イベント ID     |                           10510                            |
|  イベント ソース   |                           ENTSSO                           |
|    コンポーネント    |                            N\A                             |
|  シンボル名  |                  SSO_INFO_DLL_LOAD_FAILED                  |
|  メッセージ テキスト   |   %1 を読み込めませんでした。 このファイルは使用可能なことを確認します。    |

## <a name="explanation"></a>説明  
 この情報イベントは、SSO サービスが DLL を読み込めなかったことを示します。  

## <a name="user-action"></a>ユーザーの操作  
 このイベントを解決するには、次のいずれかの操作 (あるいは複数の操作) を行います。  

- DLL が SSO インストール ディレクトリ (通常、C:\Program Files\Common Files\Enterprise Single Sign-On) にあることを確認します。 SSO インストール ディレクトリが違う可能性があります。  

- 1 つの DLL が不足または破損している場合は、DLL の置き換えを試みてからサービスを再起動してください。  

  詳細については、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] ヘルプの次の情報を参照してください:   

- [Enterprise Single Sign-On の実装](../core/implementing-enterprise-single-sign-on.md)
