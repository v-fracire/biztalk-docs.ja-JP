---
title: "使用してスクリプトのサンプル例外管理をインストールする |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8ba65a4b-5fe1-4e17-b979-c3d380b526d6
caps.latest.revision: "3"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 1a8ec57671051f15107449fedb4803380a635cf9
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="installing-the-exception-management-samples-using-install-scripts"></a>インストール スクリプトを使用して例外管理のサンプルをインストールします。
このセクションで提供するインストール スクリプトから例外管理のサンプルをインストールする方法について説明します、[!INCLUDE[esbToolkit](../includes/esbtoolkit-md.md)]です。  
  
 **インストール スクリプトから ESB 例外管理のサンプルをインストールするには**  
  
1.  **[スタート]** メニューの **[ファイル名を指定して実行]**をクリックします。  
  
2.  **実行** ダイアログ ボックスで、「 **cmd**、し、enter キーを押してコマンド プロンプトを開きます。  
  
3.  次のコマンド実行交換、 *\<パス >*をインストールする .cmd ファイルへの完全パスを持つパラメーター (このリリースでは名前と既定のパスは \Source\Samples\Exception Handling\Install\Scripts\\):  
  
    ```  
    <path>\Setup_bin.cmd  
    ```