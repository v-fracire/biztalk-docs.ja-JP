---
title: '手順 2: ロード テスト コント ローラーとエージェント コンピューターの構成 |Microsoft Docs'
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e9d937ac-55d8-48fa-bba2-3efe151587b8
caps.latest.revision: 5
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 4b03a191269936311d04f7b773ed3159db66e34f
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36972451"
---
# <a name="step-2-configure-load-test-controller-and-agent-computers"></a>手順 2: ロード テスト コント ローラーとエージェント コンピューターを構成します。

## <a name="overview"></a>概要
Visual Studio では、ローカルのロード テストの実行に最大 250 個の仮想ユーザーをシミュレートする負荷を生成できます。 250 を超える仮想ユーザーをシミュレートするために、またはリモートからテストを開始するコンピューターには、Visual Studio ロード テスト仮想ユーザーが必要です。  
  
 すべてのロード テストに実行されるこのガイドは、2 台のコンピューターから開始されました。  
  
- ロード テスト コント ローラーと Test Load Agent の両方として実行されている 1 台のコンピューター。  
  
- 別のコンピューターのみロード テスト エージェントとして実行されています。  
  
  テストの結果は、SQL Server データベースにリモートでロード テストの結果リポジトリに保存されていました。  
  
  テスト コント ローラーとテスト エージェントを使用して、複数のテスト コンピューターにロード テストを配布する方法の詳細については、次を参照してください。[分散ロード テスト間で複数テスト マシンを使用してテスト コント ローラーとテスト エージェント](https://msdn.microsoft.com/library/dd728093.aspx)します。  
  
## <a name="install-and-configure-the-load-test-controller-and-load-test-agents"></a>インストールし、構成、ロード テスト コント ローラーとロード テスト エージェント  
 インストールして、ロード テスト コント ローラーを構成してテスト エージェントを読み込む、次を参照してください。[のインストールとテスト エージェントを構成](https://docs.microsoft.com/visualstudio/test/lab-management/install-configure-test-agents)します。
