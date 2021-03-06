---
title: 'シングル サインオン: イベント 10512 |Microsoft Docs'
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 4edf0512-112d-40b8-9e29-7dd67f999b6d
caps.latest.revision: 15
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 54ba5a340a1a7590dae72016a3e747726ea68125
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36980963"
---
# <a name="single-sign-on-event-10512"></a>シングル サインオン: イベント 10512
## <a name="details"></a>詳細  

|                 |                                                            |
|-----------------|------------------------------------------------------------|
|  製品名   |                 エンタープライズ シングル サインオン                  |
| 製品バージョン | [!INCLUDE[btsSSOVersion](../includes/btsssoversion-md.md)] |
|    イベント ID     |                           10512                            |
|  イベント ソース   |                           ENTSSO                           |
|    コンポーネント    |                            N\A                             |
|  シンボル名  |                   SSO_ERROR_LOADLIBRARY                    |
|  メッセージ テキスト   |      %1 を読み込めませんでした。%r<br /><br /> エラー コード: %2。       |

## <a name="explanation"></a>説明  
 このエラー イベントは、指定されたダイナミック リンク ライブラリ (DLL) を SSO サーバー プロセスに読み込めなかったことを示します。 DLL が SSO インストール ディレクトリ (通常、C:\Program Files\Common Files\Enterprise Single Sign-On) に存在しない場合、セットアップが正常に完了していないか、セットアップ完了後に DLL が削除されたを示している可能性があります。 DLL が存在する場合は、SSO サービスで DLL への適切なパスを解決できないという問題が発生している可能性があります。 さらに、DLL 自体が壊れている可能性もあります。  

## <a name="user-action"></a>ユーザーの操作  
 このエラーを解決するには、以下の 1 つ以上の操作を実行します。  

- 広い範囲でセットアップの失敗が疑われる場合は、製品のアンインストールと再インストールが必要になることがあります。  

- 1 つの DLL が不足または破損している場合は、DLL の置き換えを試みてからサービスを再起動してください。  

  詳細については、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] ヘルプの次の情報を参照してください:   

- [Enterprise Single Sign-On の実装](../core/implementing-enterprise-single-sign-on.md)
