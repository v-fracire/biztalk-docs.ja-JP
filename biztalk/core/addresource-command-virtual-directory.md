---
title: 'AddResource コマンド: 仮想ディレクトリ |Microsoft Docs'
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 446be3b3-31da-4f03-81b5-3a75c8da6558
caps.latest.revision: 24
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 364926e00f8d29fbce567a21d09265dee98a4e0f
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36993147"
---
# <a name="addresource-command-virtual-directory"></a>AddResource コマンド: 仮想ディレクトリ
使用する BizTalk アプリケーションには、Web サイトまたは Web サービス用の仮想ディレクトリを追加するには**AddResource**コマンドを指定**System.BizTalk:WebDirectory**型パラメーター。 このコマンドを実行すると、該当する仮想ディレクトリが BizTalk 管理データベースに追加されます。 仮想ディレクトリは、BizTalk Server 管理コンソール (追加先アプリケーションのリソース フォルダー) にも表示されます。 使用するとさらに、仮想ディレクトリが一覧表示、 [ListApp コマンド](../core/listapp-command.md)します。  
  
> [!IMPORTANT]
>  URL に https が含まれる仮想ディレクトリを追加する場合、URL には https ではなく http を使用する必要があります。 https を使用した場合、仮想ディレクトリの追加操作は失敗します。 URL に http を指定したとしても、インターネット インフォメーション サービス メタベースでは、依然として、その URL の https 設定が有効であるため、仮想ディレクトリは正常に機能します。  
  
> [!NOTE]
>  64 ビット版の Web サービスから仮想ディレクトリを追加し、その仮想ディレクトリを含むアプリケーションを 32 ビット コンピューターにインストールしようとしても、仮想ディレクトリはインストールされません。 64 ビット コンピューターにのみインストールされます。  
  
## <a name="usage"></a>使用方法  
 **BTSTask AddResource** [/**ApplicationName:**<em>値</em>] **/Type:System.BizTalk:WebDirectory****[/overwrite]****/Source:**<em>値</em>[**/Destination:**<em>値</em>] [**/Server:** <em>値</em>] [**/database:**<em>値</em>]  
  
## <a name="parameters"></a>パラメーター  
  
|                   パラメーター                   | 必須 |                                                                                                                                                                                                                                                         値                                                                                                                                                                                                                                                          |
|-----------------------------------------------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **/ApplicationName** (または **/A**、「解説」を参照してください) |    いいえ    |                                                                                                                                仮想ディレクトリを追加する BizTalk アプリケーションの名前。 名前にスペースが含まれている場合は、二重引用符 (") で囲む必要があります。 アプリケーション名が指定されなかった場合、グループの既定の BizTalk アプリケーションが使用されます。                                                                                                                                 |
|      **/入力**(または **/T**、「解説」を参照してください)       |   はい    |                                                                                                                                                                                                                          **System.BizTalk:WebDirectory** (この値小文字は区別されません)。                                                                                                                                                                                                                           |
|    **/上書き**(または **/O**、「解説」を参照してください)    |    いいえ    |                                                                                                                                               既存の仮想ディレクトリを更新するためのオプション。 指定しなかった場合、追加する仮想ディレクトリと同じ名前の仮想ディレクトリが既にアプリケーションに存在した場合、AddResource 操作は失敗します。                                                                                                                                                |
|     **/Source** (または **/S**、「解説」を参照してください)      |   はい    |                                                                                                                                                                                                 ソース仮想ディレクトリの完全 URI。<br /><br /> 例 :<br /><br /> http://MyHost:80/MyPath/MyVirtualDirectory                                                                                                                                                                                                 |
|  **/変換先**(または **/De**、「解説」を参照してください)   |    いいえ    |                                                                                                                                                    アプリケーションが .msi ファイルからインストールされたときに、仮想ディレクトリに割り当てる URI。 このパラメーターを指定しなかった場合、Source パラメーターの値が localhost と組み合わせて使用されます。                                                                                                                                                    |
|     **/サーバー** (または **/S**、「解説」を参照してください)      |    いいえ    | BizTalk 管理データベースをホストする SQL Server インスタンスの名前。ServerName\InstanceName,Port の形式で指定します。<br /><br /> インスタンス名の指定は、そのインスタンス名がサーバー名と異なる場合にのみ必要です。 ポートの指定は、SQL Server で使用するポート番号が既定値 (1433) と異なる場合にのみ必要です。<br /><br /> 例 :<br /><br /> Server=MyServer<br /><br /> Server=MyServer\MySQLServer,1533<br /><br /> 指定しなかった場合、ローカル コンピューターで実行されている SQL Server インスタンスの名前が使用されます。 |
|    **/データベース**(または **/Da**、「解説」を参照してください)    |    いいえ    |                                                                                                                                                                                     BizTalk 管理データベースの名前。 指定されていない場合は、SQL Server のローカル インスタンスで実行されている BizTalk 管理データベースが使用されます。                                                                                                                                                                                     |
  
## <a name="sample"></a>サンプル  
 **BTSTask AddResource applicationname: myapplication/Type: System.BizTalk:WebDirectory/overwrite/Source:<http://Host1:90/MyVirtualDirectory> /Destination:<http://Host2:90/MyVirtualDirectory> /Server:MyDatabaseServer/Database:BizTalkMgmtDb**  
  
## <a name="remarks"></a>コメント  
 パラメーターの大文字と小文字は区別されません。 パラメーター名は、すべて入力する必要はありません。最初の数文字 (一意に特定できるだけの文字数) を入力するだけで構いません。  
  
## <a name="see-also"></a>参照  
 [AddResource コマンド](../core/addresource-command.md)   
 [.NET アセンブリをアプリケーションに追加する方法](../core/how-to-add-a-net-assembly-to-an-application.md)