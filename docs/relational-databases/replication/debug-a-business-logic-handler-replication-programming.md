---
title: "调试业务逻辑处理程序（复制编程）| Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- merge replication business logic handlers [SQL Server replication]
- business logic handlers [SQL Server replication]
- BusinessLogicModule class
ms.assetid: edd0d17a-0e9c-4c28-8395-a7d47e8ce3d6
caps.latest.revision: 34
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 72ca7cf7a7de06c1b0da728fa1c8541bae1f0e8a
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="debug-a-business-logic-handler-replication-programming"></a>调试业务逻辑处理程序（复制编程）
  在同步合并订阅时，可以使用业务逻辑处理程序调用自定义业务逻辑。 有关详细信息，请参阅[合并同步期间执行业务逻辑](../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md)。  
  
 合并复制协调器 (replrec.dll) 调用包含业务逻辑的托管代码程序集。 在大多数情况下，replrec.dll 和自定义业务逻辑是在运行合并代理的计算机上执行的（对于请求订阅，在订阅服务器上执行；对于推送订阅，在分发服务器上执行）。 在 Web 同步或 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 订阅服务器的情况下，协调器和自定义业务逻辑在 Web 服务器上执行。  
  
### <a name="to-debug-a-business-logic-handler-on-a-local-computer"></a>在本地计算机上调试业务逻辑处理程序  
  
1.  配置发布和分发，创建一个发布，然后创建该发布的一个订阅。 有关详细信息，请参阅[配置发布和分发](../../relational-databases/replication/configure-publishing-and-distribution.md)和[创建、修改和删除发布和项目（复制）](../../relational-databases/replication/publish/create-modify-and-delete-publications-and-articles-replication.md)。  
  
2.  创建和注册业务逻辑处理程序。 有关详细信息，请参阅 [Implement a Business Logic Handler for a Merge Article](../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)。  
  
3.  在以编程的方式同步启动合并代理的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio 中创建一个复制管理对象 (RMO) 项目。 有关详细信息，请参阅 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md)。  
  
4.  在业务逻辑处理程序代码中，于正在调试的方法中或类构造函数中设置一个断点。 有关可在业务逻辑处理程序中实现的方法的详细信息，请参阅 <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> 方法主题。  
  
5.  在调试模式下生成业务逻辑处理程序，并将程序集和调试符号文件 (.pdb) 部署在步骤 1 中注册的位置。  
  
    > [!NOTE]  
    >  若要简化调试，请创建一个同时包含业务逻辑处理程序项目和同步订阅的项目的 Visual Studio .NET 解决方案。 在这种情况下，请将同步项目设置为启动项目，并将生成环境配置为在调试过程中将业务逻辑程序集部署到步骤 1 中注册的位置。  
  
6.  对订阅数据库或发布数据库执行插入、更新或删除命令。 命令和执行位置取决于正在调试的方法。  
  
7.  在调试模式下启动步骤 3 中的项目以同步订阅。  
  
8.  假定未设置任何其他断点且复制了正确的命令，则执行将在到达业务逻辑处理程序中的断点时停止。  
  
### <a name="to-debug-a-business-logic-handler-on-a-web-server-using-web-synchronization-or-for-a-sql-server-compact-subscriber"></a>在 Web 服务器上使用 Web 同步或为 SQL Server Compact 订阅服务器调试业务逻辑处理程序  
  
1.  配置发布和分发，创建一个发布，然后创该发布的建一个请求订阅。 该发布必须支持 Web 同步或 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 订阅服务器。  
  
2.  创建和注册业务逻辑处理程序。 有关详细信息，请参阅 [Implement a Business Logic Handler for a Merge Article](../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)。  
  
3.  在业务逻辑处理程序代码中，于正在调试的方法中或类构造函数中设置一个断点。 有关可在业务逻辑处理程序中实现的方法的详细信息，请参阅 <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> 方法主题。  
  
4.  在调试模式下生成业务逻辑处理程序，并将程序集和调试符号文件 (.pdb) 部署在 Web 服务器上步骤 1 中注册的位置。  
  
    > [!NOTE]  
    >  如果由于程序集正在使用而无法生成业务逻辑处理程序，则在 Web 服务器上，在命令提示符处键入命令 `iisreset` 以重置 Web 服务器。  
  
5.  在启用 Web 同步的情况下同步订阅。 同步期间，Web 服务器将加载注册的程序集。  
  
6.  使用 Visual Studio .NET 调试器，在 Web 服务器上附加到下列进程之一：  
  
    -   w3wp.exe - Windows Server 2003。  
  
    -   inetinfo.exe - Windows 2000 和 Windows XP。  
  
7.  在 **“输出”** 窗口中，检查调试输出以验证注册程序集的符号是否正确加载。 如果未加载符号，请确保在步骤 4 中复制了正确的 .pdb 文件，然后重复步骤 5。  
  
8.  对订阅数据库或发布数据库执行插入、更新或删除命令。 命令和执行位置取决于正在调试的方法。  
  
9. 使用 Visual Studio 调试器，附加到 w3wp.exe 进程。  
  
10. 使用 Web 同步再次同步订阅。  
  
11. 假定未设置任何其他断点且复制了正确的命令，则执行将在到达业务逻辑处理程序中的断点时停止。  
  
## <a name="see-also"></a>另请参阅  
 [Implement a Business Logic Handler for a Merge Article](../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)  
  
  

