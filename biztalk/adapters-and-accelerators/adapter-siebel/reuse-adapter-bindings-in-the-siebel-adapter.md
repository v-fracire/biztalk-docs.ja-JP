---
title: "Siebel アダプターのアダプターのバインドを再利用 |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- binding file, definition
- adapter bindings, reusing
ms.assetid: 1dc17b7a-5397-43f4-b19e-9c50fb0e97ff
caps.latest.revision: "7"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 6bff4d1f4566f758b7cc6d1d37efcb30f651d9d7
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="reuse-adapter-bindings-in-the-siebel-adapter"></a>Siebel アダプターのアダプターのバインドを再利用します。
バインディングは、オーケストレーション ポートなど、ロール リンクの論理エンドポイントとの送信などの物理的なエンドポイント間のマッピングを作成し、ポートまたはパーティを受信します。 これにより、BizTalk ビジネス ソリューションの複数のコンポーネント間で通信できるようになります。 バインドを作成するには BizTalk Server 管理コンソールを使用します。  
  
## <a name="what-is-a-binding-file"></a>バインド ファイルとは何ですか。  
バインド ファイルとは、BizTalk アセンブリ、アプリケーション、またはグループのスコープ内の各 BizTalk オーケストレーションのバインド情報を含む XML ファイルです。 バインド ファイルについて説明します。  
  
-   各オーケストレーションがバインドされているホスト
  
-   ホストの信頼レベル
  
-   送信ポート、受信ポート、受信場所、およびパーティが構成されているそれぞれの設定
  
 バインド ファイルを生成し、アセンブリ、アプリケーション、またはグループに含まれているバインドを適用できます。 これにより、さまざまな展開環境のバインドを手動で構成することによってし、アプリケーションの展開を高速化します。  
  
 バインド ファイルは、BizTalk アセンブリ、アプリケーション、またはグループを自動的には生成されません。 ただし、バインドをエクスポートすることによって、バインド ファイルを生成できます。 バインド ファイルをインポートして、アプリケーションまたはグループにすることができます。  
  
 バインドおよびバインド ファイルについての詳細については、次を参照してください。[バインド ファイルとアプリケーションの展開](../../core/binding-files-and-application-deployment.md)です。
 
 > [!NOTE]
 >  バインド ファイルは、BizTalk アセンブリ、アプリケーション、またはグループを自動的には生成されません。 バインドをエクスポートすることによって、バインド ファイルを生成することができます。 バインド ファイルをインポートして、アプリケーションまたはグループにすることができます。  
  
## <a name="prerequisites"></a>前提条件  
I 番目のメンバーであるアカウントのサインイン、 [!INCLUDE[btsBizTalkServerNoVersion](../../includes/btsbiztalkservernoversion-md.md)] Administrators グループまたは BizTalk Operators グループ。 詳細なアクセス許可についてを参照してください。[を展開すると、BizTalk アプリケーションの管理に必要なアクセス許可](../../core/permissions-required-for-deploying-and-managing-a-biztalk-application.md)です。

 
## <a name="export-bindings"></a>バインドをエクスポートします。
このセクションでは、XML ファイルに BizTalk アプリケーションのバインドをエクスポートする方法について説明します。 別の BizTalk アプリケーションに XML ファイルからのバインドをインポートできます。 バインドをインポートするには、アプリケーション内の同じ名前の既存のバインドが上書きされます。 バインドをアプリケーションに追加して、既存のバインドを上書きしないようにすることもできます。 アプリケーションをインポートしない限り、追加したバインドは有効になりません。  
  
1.  開く、[!INCLUDE[btsBizTalkServerNoVersion](../../includes/btsbiztalkservernoversion-md.md)]管理コンソールです。  
  
2.  展開**BizTalk グループ**の順に展開および**アプリケーション**です。  
  
3.  エクスポートするバインドを選択するアプリケーションを右クリックして**エクスポート**、し、**バインド**です。  
  
4.  **バインドのエクスポート**] ページの [**ファイルへのエクスポート**バインドをエクスポートする XML ファイルの絶対パスを入力します。  
  
     たとえば、入力します。`C:\Bindings\Application1Bindings.Binding1.xml`  
  
5.  いることを確認**、現在のアプリケーションからのすべてのバインドをエクスポート**が選択されています。  
  
6.  グループのすべてのパーティ情報をエクスポートするには、選択、**グローバル パーティ情報をエクスポート**チェック ボックスをオンします。  
  
7.  [ **OK**] を選択します。 バインディングは、指定した場所に XML ファイルにエクスポートされます。  

## <a name="import-bindings"></a>バインドのインポート
BizTalk Server 管理コンソールを使用してバインドをインポートします。
  
1.  開く、[!INCLUDE[btsBizTalkServerNoVersion](../../includes/btsbiztalkservernoversion-md.md)]管理コンソールです。  
  
2.  展開**BizTalk グループ**の順に展開および**アプリケーション**です。  
  
3.  バインドのインポートを選択するアプリケーションを右クリックして**インポート**、し、**バインド**です。  
  
4.  バインド ファイルを選択し、**開く**です。  
  
バインド ファイルのアイテムがアプリケーションに書き込まれます。 これらのアイテムは、アプリケーションの該当するフォルダーに表示されます。 バインドの表示の一部として、送信ポートをインポートするなど、**送信ポート**フォルダーです。  

## <a name="passwords-are-removed"></a>パスワードは削除されます。  
セキュリティ上の理由により、[!INCLUDE[btsBizTalkServerNoVersion](../../includes/btsbiztalkservernoversion-md.md)] では、バインド ファイルのエクスポート時にバインドのパスワードがファイルから削除されます。 バインドをインポートした後で、送信ポートと受信場所のパスワードを再構成する必要があります。 [トランスポートのプロパティ] ダイアログ ボックスでパスワードを構成する、[!INCLUDE[btsBizTalkServerNoVersion](../../includes/btsbiztalkservernoversion-md.md)]コンソールの送信ポートまたは受信場所を管理します。 

ユーザー名とパスワードを指定する方法の詳細については、次を参照してください。 [、Siebel の資格情報 で、サインオンの構成](../../adapters-and-accelerators/adapter-siebel/configure-the-sign-in-credentials-for-the-siebel.md)です。

## <a name="see-also"></a>参照
[Siebel アダプターと BizTalk アプリケーションを作成する構成要素](../../adapters-and-accelerators/adapter-siebel/building-blocks-to-create-biztalk-applications-with-the-siebel-adapter.md)