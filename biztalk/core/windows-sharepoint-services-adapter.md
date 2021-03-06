---
title: Windows SharePoint Services アダプター |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Windows SharePoint Services adapters
ms.assetid: cbfc9bf3-912d-4849-ba8c-07a116888bbd
caps.latest.revision: 14
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 06135b2897cb492905c331e72cf087b867c69304
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36998827"
---
# <a name="windows-sharepoint-services-adapter"></a>Windows SharePoint Services アダプタ
Microsoft Windows SharePoint Services 用 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] アダプターを使用すると、BizTalk Server を Windows SharePoint Services および Microsoft Office InfoPath と密接に統合できます。 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] ソリューションで Windows SharePoint Services アダプターを使用した場合、次の機能が提供されます。  
  
- Windows SharePoint Services 経由の入力メッセージと出力メッセージへの簡単なアクセス。  
  
- Microsoft Office InfoPath などの Office アプリケーションを使用した XML メッセージの編集機能。  
  
- InfoPath との XML メッセージの双方向の変換。  
  
  [!INCLUDE[btsSharePointSvcsNoVersion](../includes/btssharepointsvcsnoversion-md.md)] アダプターは、次のコンポーネントで構成されます。  
  
|                                                                                                       |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
|-------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   CSOM [!INCLUDE[btsSharePointSvcsNoVersion](../includes/btssharepointsvcsnoversion-md.md)] アダプター   |                                                       [!INCLUDE[btsSharePointSvcsNoVersion](../includes/btssharepointsvcsnoversion-md.md)] クライアント側オブジェクト モデル (CSOM) を使用します。 このアダプターは、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] のインストール時にインストールされます。 追加のインストール手順はありません。<br /><br /> [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]インストール***自動的に***インストール、SharePoint クライアント オブジェクト モデル再頒布可能パッケージはも[ http://go.microsoft.com/fwlink/p/?LinkId=263482](http://go.microsoft.com/fwlink/p/?LinkId=263482)します。                                                        |
| SSOM [!INCLUDE[btsSharePointSvcsNoVersion](../includes/btssharepointsvcsnoversion-md.md)] Web サービス | **非推奨**。 [!INCLUDE[btsSharePointSvcsNoVersion](../includes/btssharepointsvcsnoversion-md.md)] サービス側オブジェクト モデル (SSOM) を使用します。<br /><br /> Web サービスがインストールされている、 [!INCLUDE[btsSharePointSvcsNoVersion](../includes/btssharepointsvcsnoversion-md.md)] 、コンピューターと同じコンピューター上にあることができます[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]または別のコンピューター。<br /><br /> Web サービスをインストールするには、実行、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]へのインストール、[!INCLUDE[btsSharePointSvcsNoVersion](../includes/btssharepointsvcsnoversion-md.md)]コンピューターとチェック**Windows SharePoint Services アダプター**します。 |
  
 [付録 b: Microsoft SharePoint アダプターのインストール](../install-and-config-guides/appendix-b-install-the-microsoft-sharepoint-adapter.md)について詳しく説明します、[!INCLUDE[btsSharePointSvcsNoVersion](../includes/btssharepointsvcsnoversion-md.md)]インストールします。  
  
> [!NOTE]
>  現時点では、フェデレーション認証はサポートされていません。 ユーザー名とパスワードのみがサポートされています。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [CSOM: SharePoint Services アダプター](../core/csom-sharepoint-services-adapter.md)  
  
-   [SSOM: SharePoint Services アダプター Web サービス](../core/ssom-sharepoint-services-adapter-web-service.md)  
  
## <a name="see-also"></a>参照  
 [アダプターを使用します。](../core/using-adapters.md)   
 [BizTalk Server アプリケーションの開発](../core/developing-biztalk-server-applications.md)