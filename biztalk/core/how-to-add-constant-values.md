---
title: "定数値を追加する方法 |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f46bf66e-caf2-4352-930f-c3c43a5717c3
caps.latest.revision: "8"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 398e2f4d176fdfab866cc8c87ce19aaf523a1b03
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="how-to-add-constant-values"></a>定数値を追加する方法
マップをテストする際、テスト中に使用する定数値を設定する場合があります。  
  
## <a name="set-constant-values-for-nodes-in-the-source-or-destination-schema-trees"></a>ソースまたは変換先のスキーマ ツリー ノードの定数値を設定します。  
  
1.  送信元スキーマ ツリーまたは送信先スキーマ ツリーのレコードまたはフィールドを選択します。  
  
2.  [プロパティ] ウィンドウで、**全般**カテゴリを使用して、**値**プロパティを選択しているレコードまたはフィールドの値を入力します。  
  
    > [!NOTE]
    >  関連付けることができますのみ値を持つレコード、**コンテンツ**プロパティに設定**テキストのみ**または**Mixed**です。  
  
 設定した場合、送信元スキーマ内のノードに対して、**値**プロパティを**\<空 >**、送信元スキーマの生成されたインスタンス メッセージには、それぞれのノードに空の値が含まれています。  
  
 送信先スキーマのフィールドをすべては使用しないことがあります。つまり、送信先スキーマのフィールドには、受信リンクが指定されないものもあります。 このような場合、マップのテスト操作によってスローされるエラーを提供する、 **TestMap 入力の検証**または**TestMap 出力の検証**プロパティに設定されます**True**です。 このような場合はマップのテスト エラーを避けるためには、次のように設定します。、**値**いずれかの定数値にノードのプロパティまたは**\<空 >**です。 使用して**\<空 >**未使用の送信先スキーマのフィールドの任意のデータを設定したくない場合。  
  
## <a name="see-also"></a>参照  
[検証し、マップのテスト](../core/how-to-configure-map-validation-and-test-parameters.md)