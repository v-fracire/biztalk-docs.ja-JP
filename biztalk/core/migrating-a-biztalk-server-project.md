---
title: BizTalk Server プロジェクトを移行する |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 5a4dde72-6555-4bf6-b90e-676aa65312ff
caps.latest.revision: 23
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: b0fd15de7aec81c046ab6b2fc23b6c63a1ec0615
ms.sourcegitcommit: 53b16fe6c1b1707ecf233dbd05f780653eb19419
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/01/2018
ms.locfileid: "50752706"
---
# <a name="migrating-a-biztalk-server-project"></a>BizTalk Server プロジェクトを移行します。
[!INCLUDE[btsVStudioNoVersion](../includes/btsvstudionoversion-md.md)] 用に開発されたプロジェクト[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]を使用して、新しい環境に移行できる[!INCLUDE[btsVStudioNoVersion](../includes/btsvstudionoversion-md.md)]変換します。 移行がサポートされているバージョンの一覧は、次を参照してください。[サポートされるアップグレード パスと環境向けインストール ガイド](http://social.technet.microsoft.com/wiki/contents/articles/28554.biztalk-server-supported-upgrade-paths-and-installation-guides.aspx)します。  

## <a name="biztalk-project-changes-after-running-the-conversion-wizard"></a>変換ウィザードを実行した後の BizTalk プロジェクトの変化  
 次の表では[!INCLUDE[btsbiztalkserver2006r2](../includes/btsbiztalkserver2006r2-md.md)]プロジェクト構成の名前変更、およびより新しいに変換がいくつかの特定の構成プロパティが、プロジェクトの後に再配置[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]プロジェクト。 ほとんどの[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]-に関連するプロジェクトの設定がある、**展開**プロジェクト デザイナーのタブ。  


| [!INCLUDE[btsbiztalkserver2006r2](../includes/btsbiztalkserver2006r2-md.md)] プロジェクト | [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] プロジェクト |
|--------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------|
|             **追跡情報を埋め込む**出力構成プロパティ             |      **定数 TRACE の定義**ビルド オプション、**ビルド**プロジェクト デザイナーのタブ       |
|           **デバッグ情報の生成**出力構成プロパティ           |      **定数 DEBUG の定義**ビルド オプション、**ビルド**プロジェクト デザイナーのタブ       |
|              **BPEL 準拠**コード生成構成プロパティ              |       **BPEL 準拠**コード プロジェクトのプロパティ ウィンドウで生成構成プロパティ        |

> [!NOTE]
>  BizTalk プロジェクトに 2 つのビルドの種類があるようになりました:**リリース**と**デバッグ**、後継**開発**と**展開**の前バージョン。 ただし、引き続きを参照してください、**開発**と**展開**から移行されるプロジェクトの構成[!INCLUDE[btsbiztalkserver2006r2](../includes/btsbiztalkserver2006r2-md.md)]します。  
> 
> [!CAUTION]
>  のみ、 \*.btproj と\*。 結果として、バックアップ、変換中にオプションを選択することでバックアップされるプロジェクト ファイルがバックアップされます。 他のファイルは手動でバックアップする必要があります。  
> 
> [!CAUTION]
>  XSD や ODX ファイルなどの自動生成項目のカスタマイズは、変換の間に失われます。 これは、Web 参照を BizTalk プロジェクトに追加すると生成される XSD ファイルにも当てはまります。  

## <a name="project-migration-and-delay-signing"></a>プロジェクトの移行と遅延署名  
 [!INCLUDE[btsbiztalkserver2006r2](../includes/btsbiztalkserver2006r2-md.md)] 使用するプロジェクト[遅延署名](http://go.microsoft.com/fwlink/p/?LinkId=140992)用に変換した後にビルド プロセス中に失敗する可能性があります[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]します。 これは、場合に発生**シリアル化アセンブリを生成**に移行されたプロジェクト構成が設定されていないために、ビルド設定**オフ**します。  

## <a name="project-migration-and-msmqt"></a>プロジェクトの移行と MSMQT  
 MSMQT は [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] には組み込まれなくなりました。 プロジェクトの移行の影響を与えるこの方法の詳細については、トピックを参照してください。[非推奨の MSMQT](../core/msmqt-deprecation.md)します。  

## <a name="project-conversion-requires-the-project-and-solution-file"></a>プロジェクトの変換に必要なプロジェクトおよびソリューション ファイル  
 [!INCLUDE[btsbiztalkserver2006r2](../includes/btsbiztalkserver2006r2-md.md)] プロジェクトを変換しようとして、ソリューション ファイルがない場合は、次のようなエラーが発生します。  

 **プロジェクト ファイルの変換中にエラーが発生しました。子要素\<BIZTALK\>要素の\<VisualStudioProject\>が無効です。**  

 プロジェクトの変換には、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] プロジェクトのソリューション ファイル (.sln) が必要です。 ソリューション ファイルがない場合は、[!INCLUDE[btsVStudioNet2005](../includes/btsvstudionet2005-md.md)] で作成し、[!INCLUDE[btsbiztalkserver2006r2](../includes/btsbiztalkserver2006r2-md.md)] プロジェクトをソリューションに追加する必要があります。 その後、[!INCLUDE[btsVStudioNoVersion](../includes/btsvstudionoversion-md.md)] 変換ウィザードを実行します。  

> [!NOTE]
>  Visual Studio でプロジェクト ファイル (.btproj) のみを使用して、プロジェクトを変換することができます。