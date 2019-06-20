---
title: 为合并项目实现自定义冲突解决程序 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], stored procedure-based resolvers
- articles [SQL Server replication], conflict resolution
- conflict resolution [SQL Server replication], merge replication
ms.assetid: 76bd8524-ebc1-4d80-b5a2-4169944d6ac0
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 47d0f7c4eb6c78b9e551fafdc1e018a27604086e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62721228"
---
# <a name="implement-a-custom-conflict-resolver-for-a-merge-article"></a>为合并项目实现自定义冲突解决程序
  本主题说明如何 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]使用[!INCLUDE[tsql](../../includes/tsql-md.md)] [或基于 COM 的自定义冲突解决程序](merge/advanced-merge-replication-conflict-com-based-custom-resolvers.md) 在中为合并项目实现自定义冲突解决程序。  
  
 **本主题内容**  
  
-   **为合并项目实现自定义冲突解决程序，使用：**  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [基于 COM 的冲突解决程序](#COM)  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 您可以编写自己的自定义冲突解决程序以作为每个发布服务器上的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存储过程。 在同步过程中，如果在注册了冲突解决程序的项目中遇到冲突，则将调用此存储过程，并且合并代理会将有关冲突行的信息传递到该存储过程的所需参数中。 基于存储过程的自定义冲突解决程序将始终在发布服务器上创建。  
  
> [!NOTE]  
>  调用[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 存储过程冲突解决程序只是为了处理基于行更改的冲突。 它们不能用于处理其他类型的冲突，例如由于 PRIMARY KEY 冲突或唯一索引约束冲突而造成的插入失败。  
  
#### <a name="to-create-a-stored-procedure-based-custom-conflict-resolver"></a>创建基于存储过程的自定义冲突解决程序  
  
1.  在发布服务器的发布数据库或 **msdb** 数据库中，创建用于实现以下所需参数的新系统存储过程：  
  
    |参数|数据类型|Description|  
    |---------------|---------------|-----------------|  
    |**@tableowner**|`sysname`|冲突被解决的表的所有者名称。 这是发布数据库中的表的所有者。|  
    |**@tablename**|`sysname`|冲突被解决的表的名称。|  
    |**@rowguid**|`uniqueidentifier`|具有冲突的行的唯一标识符。|  
    |**@subscriber**|`sysname`|传播冲突更改的源服务器的名称。|  
    |**@subscriber_db**|`sysname`|传播冲突更改的源数据库的名称。|  
    |**@log_conflict OUTPUT**|`int`|合并进程是否应记录冲突以便以后进行解决：<br /><br /> **0** = 不记录冲突。<br /><br /> **1** = 订阅服务器是冲突解决落选方。<br /><br /> **2** = 发布服务器是冲突解决落选方。|  
    |**@conflict_message OUTPUT**|`nvarchar(512)`|记录冲突时要提供的有关解决方法的消息。|  
    |**@destowner**|`sysname`|订阅服务器上的已发布表的所有者。|  
  
     此存储过程使用合并代理传递给这些参数的值来实现自定义冲突解决逻辑；它必须返回结构与基表结构相同的单行结果集，并且包含该行的入选版本的数据值。  
  
2.  向订阅服务器用来连接到发布服务器的任何登录名授予对存储过程的 EXECUTE 权限。  
  
#### <a name="to-use-a-custom-conflict-resolver-with-a-new-table-article"></a>将自定义冲突解决程序用于新的表项目  
  
1.  执行 [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql) 以定义一个项目，为 **@article_resolver** **参数指定值** MicrosoftSQL **@article_resolver** ，并为 **@resolver_info** 参数指定用于实现冲突解决程序逻辑的存储过程的名称。 有关详细信息，请参阅 [Define an Article](publish/define-an-article.md)。  
  
#### <a name="to-use-a-custom-conflict-resolver-with-an-existing-table-article"></a>将自定义冲突解决程序用于现有表项目  
  
1.  执行 [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql)，指定 **@publication** 和 **@article** ，将 **@property** 的值指定为 **article_resolver**，将 **@value** 的值指定为 **MicrosoftSQL** **Server Stored ProcedureResolver**。  
  
2.  执行 [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql)，指定 **@publication** 和 **@article** ，将 **@property** 的值指定为 **@property** ，同时为 **@value** 中为合并项目实现自定义冲突解决程序。  
  
##  <a name="COM"></a> 使用基于 COM 的自定义冲突解决程序  
 <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport> 命名空间实现了一个接口，可以利用该接口编写复杂的业务逻辑以处理事件并解决在合并复制同步过程中发生的冲突。 有关详细信息，请参阅 [实现合并项目的业务逻辑处理程序](implement-a-business-logic-handler-for-a-merge-article.md)。 您也可以编写自己的基于本机代码的自定义业务逻辑以解决冲突。 使用诸如 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C++ 之类的产品，此逻辑可作为 COM 组件生成并编译到动态链接库 (DLL) 中。 这类基于 COM 的自定义冲突解决程序必须实现 ICustomResolver 接口，该接口是专为解决冲突而设计的  。  
  
#### <a name="to-create-and-register-a-com-based-custom-conflict-resolver"></a>创建和注册基于 COM 的自定义冲突解决程序  
  
1.  在与 COM 兼容的创作环境中，添加对自定义冲突解决程序库的引用。  
  
2.  对于 Visual C++ 项目，请使用 #import 命令将该库导入项目中。  
  
3.  创建一个用于实现 **ICustomResolver** 接口的类。  
  
4.  实现某些特定的方法和属性。  
  
5.  生成项目以创建自定义冲突解决程序库文件。  
  
6.  将该库部署在包含合并代理可执行文件的目录（通常为 \Microsoft SQL Server\100\COM）中。  
  
    > [!NOTE]  
    >  对于请求订阅，必须在订阅服务器上部署自定义冲突解决程序；对于推送订阅，必须在分发服务器上部署；或者部署在使用 Web 同步的 Web 服务器上。  
  
7.  使用 regsvr32.exe 注册部署目录中的自定义冲突解决程序库，如下所示：  
  
    ```  
    regsvr32.exe mycustomresolver.dll  
    ```  
  
8.  在发布服务器上，执行 [sp_enumcustomresolvers &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql) 以验证该库尚未注册为自定义冲突解决程序。  
  
9. 若要将该库注册为自定义冲突解决程序，请在分发服务器上执行 [sp_registercustomresolver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-registercustomresolver-transact-sql)。 指定的 COM 对象的友好名称 **@article_resolver** ，库的 ID (CLSID) **@resolver_clsid** ，并将值`false`对于 **@is_dotnet_assembly** .  
  
    > [!NOTE]  
    >  当不再需要某个自定义冲突解决程序时，可使用 [sp_unregistercustomresolver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-unregistercustomresolver-transact-sql) 将其取消注册。  
  
10. （可选）在集群上，对集群的所有节点重复步骤 5-8 来注册自定义冲突解决程序。 为了确保在故障转移之后自定义冲突解决程序能够正确载入协调器，此操作是必需的。  
  
#### <a name="to-use-a-custom-conflict-resolver-with-a-new-table-article"></a>将自定义冲突解决程序用于新的表项目  
  
1.  在发布服务器上执行 [sp_enumcustomresolvers &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql)，并记下所需解决程序的友好名称。  
  
2.  在发布服务器上，对发布数据库执行 [sp_addmergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql) 来定义项目。 将步骤 1 中项目冲突解决程序的友好名称指定给 **@article_resolver** 中为合并项目实现自定义冲突解决程序。 有关详细信息，请参阅 [定义项目](publish/define-an-article.md)。  
  
#### <a name="to-use-a-custom-conflict-resolver-with-an-existing-table-article"></a>将自定义冲突解决程序用于现有表项目  
  
1.  在发布服务器上执行 [sp_enumcustomresolvers &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql)，并记下所需解决程序的友好名称。  
  
2.  执行 [sp_changemergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql)，指定 **@publication** 、 **@article** ，为 **@property** 指定值 **article_resolver**，为 **@value** 指定项目解决程序的友好名称。  
  
#### <a name="viewing-a-sample-custom-resolver"></a>查看示例自定义冲突解决程序  
  
1.  SQL Server 2000 示例文件中提供了示例。 下载[ **sql2000samples.zip**](https://github.com/Microsoft/sql-server-samples/blob/master/samples/tutorials/Miscellaneous/sql2000samples.zip)。 这会将下载 3 个本质 6.9 mb 的文件。  
  
2.  从下载的压缩 .cab 文件中提取文件。  
  
3.  运行 **setup.exe**  
  
    > [!NOTE]  
    >  选择安装选项时，仅需安装 **复制** 示例。 (默认安装路径是**C:\Program Files (x86) \Microsoft SQL Server 2000 Samples\1033\\** )  
  
4.  转至安装文件夹。 （默认文件夹为 **C:\Program Files (x86)\Microsoft SQL Server 2000 Samples\1033\sqlrepl\unzip_sqlreplSP3.exe**）  
  
5.  运行 **unzip_sqlreplSP3.exe** 程序。  
  
    > [!NOTE]  
    >  默认情况下，com 冲突解决程序示例将安装到 **C:\Program Files (x86)\Microsoft SQL Server 2000 Samples\1033\sqlrepl\resolver\subspres** 文件夹。  
  
6.  在 **subspres** 文件夹中，在所有源文件中查找所有出现的 **#include sqlres.h** ，将其替换为 **#import "replrec.dll" no_namespace, raw_interfaces_only**  
  
## <a name="see-also"></a>请参阅  
 [Advanced Merge Replication Conflict Detection and Resolution](merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [COM-Based Custom Resolvers](merge/advanced-merge-replication-conflict-com-based-custom-resolvers.md)   
 [复制安全最佳做法](security/replication-security-best-practices.md)  
  
  
