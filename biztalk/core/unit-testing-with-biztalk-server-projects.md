---
title: BizTalk Server プロジェクトを使用した単体テスト |Microsoft ドキュメント
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f2594f29-fc34-4dda-9316-2afd4e0056d7
caps.latest.revision: 12
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: da7147f4c2500946fb97c47592a2a4a35d3dcf62
ms.sourcegitcommit: 3fc338e52d5dbca2c3ea1685a2faafc7582fe23a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/01/2017
ms.locfileid: "26008123"
---
# <a name="unit-testing-with-biztalk-server-projects"></a>BizTalk Server プロジェクトを使用した単体テスト
BizTalk Server には、単体テストを有効にできる機能が導入された、**展開**BizTalk プロジェクトのプロパティ ページ。 次のスクリーン ショットは、このプロジェクトのプロジェクトを右クリックすると、プロジェクト デザイナーからアクセス設定を示しています。、**プロパティ**です。  
  
 ![](../core/media/projectdesignerenableunittesting.gif "ProjectDesignerEnableUnitTesting")  
  
 **単体テスト プロジェクトのプロパティを公開するプロジェクト デザイナーの 展開 タブのスクリーン ショット。**  
  
 この機能により、スキーマ、マップ、パイプラインの単体テストを作成できます。 このセクションのトピックでは、単体テスト機能を使用するアプローチの例をいくつか紹介します。 この機能を有効にしてプロジェクトを再構築すると、次の基本クラスから、単体テストをサポートするためのアイテム クラスが派生します。  
  
|アイテムの種類|基本クラス|  
|-------------------|----------------|  
|スキーマ|**Microsoft.BizTalk.TestTools.Schema.TestableSchemaBase**|  
|マップ|**Microsoft.BizTalk.TestTools.Mapper.TestableMapBase**|  
|パイプライン|**Microsoft.BizTalk.TestTools.Pipeline.TestablePipelineBase**|  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [単体テストのスキーマおよびマップを持つ機能の使用](../core/using-the-unit-testing-feature-with-schemas-and-maps.md)  
  
-   [単体テストのパイプラインを持つ機能の使用](../core/using-the-unit-testing-feature-with-pipelines.md)  
  
## <a name="related-sections"></a>関連項目  
 [単体テスト (Visual Studio) の操作](http://go.microsoft.com/fwlink/?LinkId=128890)