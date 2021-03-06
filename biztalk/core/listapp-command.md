---
title: ListApp コマンド |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 5329dd55-4ce7-46d2-8983-90ac33725055
caps.latest.revision: 22
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 51299b6f3488e1088fac2b903c9146bee93885e5
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36987307"
---
# <a name="listapp-command"></a>ListApp コマンド
BizTalk アプリケーションに存在するすべてのリソース アイテムをコンソールに一覧表示します。このとき、アイテムごとのローカル一意識別子 (LUID) と種類も表示されます。 リソース アイテムが 1 つを使用して BizTalk アプリケーションに追加できる、 [AddResource コマンド](../core/addresource-command.md)アセンブリ、スクリプト、ファイル、ポリシー、COM コンポーネント、仮想ディレクトリ、BAM アイテム、または証明書など。 これらのリソース アイテムは、BizTalk Server 管理コンソールの [リソース] ノードにも表示されます。  
  
 このコマンドで ResourceSpec パラメーターを指定した場合、同じ情報が .xml ファイルに出力されます。 この .xml ファイルを使用することができます、 **ExportApp** 」の説明に従って、.msi ファイルに、アプリケーション内のアイテムのサブセットをエクスポートするコマンドを[ExportApp コマンド](../core/exportapp-command.md)します。  
  
 このコマンドでは、仮想ディレクトリの Web サーバーのホスト名が "localhost" に置き換えられます。 ResourceSpec パラメーターによって生成されたファイルを ExportApp コマンドで使用する場合、かつ、Web サーバーがリモート コンピューターに存在する場合は、このファイルを手動で編集し、ファイル内の "localhost" となっている部分を、ホスト名とポート番号に置き換える必要があります。 この作業を行わないと、仮想ディレクトリとその内容が、アプリケーションの .msi ファイルに追加されません。  
  
 例: http://MyWebServer:80/MyVirtualDirectory します。  
  
## <a name="usage"></a>使用方法  
 **BTSTask の ListApp** [**/applicationname は:**<em>値</em>] [**/ResourceSpec:**<em>値</em>] [**/Server:**<em>値</em>] [**/database:**<em>値</em>]  
  
## <a name="parameters"></a>パラメーター  
  
|パラメーター|必須|値|  
|---------------|--------------|-----------|  
|**/ApplicationName** (または **/A**、「解説」を参照してください)|いいえ|アイテムを一覧表示する BizTalk アプリケーションの名前。 名前にスペースが含まれている場合は、二重引用符 (") で囲む必要があります。  このパラメーターを指定しなかった場合、既定のアプリケーションが使用されます。|  
|**/ResourceSpec** (または **/R**、「解説」を参照してください)|いいえ|このコマンドで生成する .xml ファイルの完全パス。 このファイルには、アプリケーション内のアイテムが、対応する LUID および種類と共に列挙されます。 例: C:\Artifacts\MyArtifacts.xml。 パスにスペースが含まれる場合は、二重引用符 (") で囲む必要があります。 同じパスとファイル名を持つファイルは上書きされます。|  
|**/サーバー** (または **/S**、「解説」を参照してください)|いいえ|BizTalk 管理データベースをホストする SQL Server インスタンスの名前。ServerName\InstanceName,Port の形式で指定します。<br /><br /> インスタンス名の指定は、そのインスタンス名がサーバー名と異なる場合にのみ必要です。 ポートの指定は、SQL Server で使用するポート番号が既定値 (1433) と異なる場合にのみ必要です。<br /><br /> 例 :<br /><br /> Server=MyServer<br /><br /> Server=MyServer\MySQLServer,1533<br /><br /> 指定しなかった場合、ローカル コンピューターで実行されている SQL Server インスタンスの名前が使用されます。|  
|**/データベース**(または **/D**、「解説」を参照してください)|いいえ|BizTalk 管理データベースの名前。 指定しなかった場合、SQL Server のローカル インスタンスで実行されている BizTalk 管理データベースが使用されます。|  
  
## <a name="sample"></a>サンプル  
 **BTSTask の ListApp applicationname: myapplication/ResourceSpec:C:\Artifacts\MyArtifacts.xml**  
  
## <a name="remarks"></a>コメント  
 パラメーターの大文字と小文字は区別されません。 パラメーター名は、すべて入力する必要はありません。最初の数文字 (一意に特定できるだけの文字数) を入力するだけで構いません。  
  
## <a name="see-also"></a>参照  
 [BTSTask コマンド ライン リファレンス](../core/btstask-command-line-reference.md)