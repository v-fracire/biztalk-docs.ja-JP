---
title: ポリシーの管理 |Microsoft ドキュメント
description: リンクをインポートするには、発行、追加、配置、削除、または BizTalk Server でポリシーをエクスポート
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f7b3bf92-8868-4c35-953f-61a7f2edff9c
caps.latest.revision: 19
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 6dd482c2f7a226a15fe730d2b75b470a54ff27e9
ms.sourcegitcommit: 5abd0ed3f9e4858ffaaec5481bfa8878595e95f7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2017
ms.locfileid: "25971168"
---
# <a name="manage-policies"></a>ポリシーを管理します。

## <a name="overview"></a>概要
このセクションのトピックでは、BizTalk Server 管理コンソールまたは BTSTask コマンド ライン ツールを使用してポリシーを管理する方法について説明します。 ポリシーは、ビジネス ルールの論理グループです。 ポリシーの基礎知識については、次を参照してください。[ポリシー](../core/policies.md)です。  
  
## <a name="import-publish-deploy-and-remove-policies"></a>インポート、公開、展開、およびポリシーの削除
 ソリューション開発者が作成および」の説明に従って、ビジネス ルール作成ツールを使用して、ポリシーの表示[ビジネス ルール作成ツールを使用して作成するビジネス ルール](../core/creating-business-rules-using-the-business-rule-composer.md)です。 開発者と IT 管理者は、BizTalk グループおよびアプリケーションでポリシーを展開して管理するために、このセクションのトピックで説明する次のタスクを実行できます。  
  
-   **BizTalk グループにポリシーをインポートします。** これを行うと、ポリシーがグループのルール エンジン データベースに追加され、BizTalk Server 管理コンソールでに表示されます、\<すべての成果物\>BizTalk グループのノードです。 これによって、ポリシーが特定のアプリケーションで有効になるわけではありません。 このセクションの他のトピックで説明するように、最初にポリシーを公開し、アプリケーションに追加してから展開する必要があります。 ルール エンジン データベースは、BizTalk グループ内のすべてのポリシーを含むデータベースです。  
  
-   **ポリシーを公開します。** これにより、ポリシーを BizTalk アプリケーション内で使用できるようになります。  
  
-   **ポリシーを BizTalk アプリケーションを追加します。** これにより、アプリケーションからポリシーを使用できますが、ポリシーが有効になるわけではありません。 ポリシーは、展開された後で有効になります。  
  
    > [!IMPORTANT]
    >  複数のアプリケーションでポリシーを共有するには、ポリシーを格納する独立したアプリケーションを作成した後、そのポリシーを使用する別のアプリケーションからポリシーを格納するアプリケーションへの参照を作成する必要があります。 これは、ポリシーを含むアプリケーションを停止すると、ポリシーが自動的に展開解除され、ポリシーを使用するアプリケーションで機能しなくなるためです。  
  
-   **ポリシーを展開します。** これにより、ポリシーの運用が開始されます (これは、オーケストレーションを開始するのと同様です。)ポリシーは手動で展開および展開解除できます。 また、アプリケーションを開始すると、そのポリシーが自動的に展開され、アプリケーションを停止すると自動的に展開解除されます。  
  
    > [!NOTE]
    >  ポリシーを展開した後で、変更することはできません。 展開済みのポリシーを変更するには、展開解除するか、ビジネス ルール作成ツールで再作成して新しいバージョン番号を付与する必要があります。  
  
-   **BizTalk アプリケーションと BizTalk グループからポリシーを削除します。** これにより、ポリシーが展開解除され、アプリケーションからだけでなくグループのルール エンジン データベースからも削除されます。  
  
-   **ポリシーをエクスポートします。** その後、ポリシーを別の BizTalk グループにインポートして使用できます。  
  
> [!NOTE]
>  Microsoft Windows Management Instrumentation (WMI) のオブジェクト モデルを使用して、管理タスクを自動化するスクリプトを作成および実行できます。 WMI の使用については、次を参照してください。、 **WMI クラス参照**[!INCLUDE[ui-guidance-developers-reference](../includes/ui-guidance-developers-reference.md)]です。
  
## <a name="next-steps"></a>次の手順
  
-   [ポリシーのインポート](../core/how-to-import-a-policy.md)  
  
-   [ポリシーの公開](../core/how-to-publish-a-policy.md)  
  
-   [ポリシーをアプリケーションに追加する](../core/how-to-add-a-policy-to-an-application.md)  
  
-   [ポリシーを展開または展開解除する](../core/how-to-deploy-or-undeploy-a-policy.md)  
  
-   [ポリシーの追跡を構成する](../core/how-to-configure-tracking-for-a-policy.md)  
  
-   [アプリケーションおよび BizTalk グループからポリシーを削除する](../core/how-to-remove-a-policy-from-an-application-and-the-biztalk-group.md)  
  
-   [ポリシーをエクスポートする](../core/how-to-export-a-policy.md)