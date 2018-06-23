---
title: 父包的实现 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- parent packages [Integration Services]
ms.assetid: d8f94830-fa27-4151-88df-cbdc6bf0fc80
caps.latest.revision: 23
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 3f14fbfda070c2cfe566044be427c14aa4674b8d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36025496"
---
# <a name="implementation-of-the-parent-package"></a>父包的实现
  负载平衡跨越多个服务器的 SSIS 包时，如果子包已经创建并部署且用来运行子包的远程 SQL Server 代理作业也创建之后，其下一个步骤是创建父包。 父包将包含很多执行 SQL Server 代理作业任务，每个任务负责调用用于运行其中一个子包的不同的 SQL Server 代理作业。 父包中的执行 SQL Server 代理作业任务又会运行各个 SQL Server 代理作业。 父包中的每个任务都包含诸如信息，例如，如何连接到远程服务器以及服务器上运行什么作业等。 有关详细信息，请参阅 [Execute SQL Server Agent Job Task](control-flow/execute-sql-server-agent-job-task.md)。  
  
 若要标识执行子包的父包，请在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 的解决方案资源管理器中右键单击该包，然后单击 **“入口点包”**。  
  
## <a name="listing-child-packages"></a>列出子包  
 如果将包含父包和子包的项目部署到 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务器，则可以查看由父包执行的子包的列表。 运行父包时， **中将自动生成父包** “概述” [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]报表。 该报表列出了由父包中包含的执行包任务执行的子包，如下图所示。  
  
 ![包含子包列表的概述报告](media/overviewreport-childpackagelisting.png "Overview Report with list of child packages")  
  
 有关访问 **“概述”** 报表的信息，请参阅 [Reports for the Integration Services Server](../../2014/integration-services/reports-for-the-integration-services-server.md)。  
  
## <a name="precedence-constraints-in-the-parent-package"></a>父包中的优先约束  
 在父包中的执行 SQL Server 代理作业任务之间创建优先约束时，这些优先约束只控制 SQL Server 代理作业在远程服务器上的启动时间。 优先约束无法接收关于从 SQL Server 代理作业的步骤中运行的子包成功或失败的信息。  
  
 这意味着子包的成功或失败不会传播到父包，因为父包中执行 SQL Server 代理作业的单独功能是请求 SQL Server 代理作业运行该子包。 成功调用 SQL Server 代理作业之后，父包将收到<xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult.Success>的结果。  
  
 此方案中的失败只表示调用远程 SQL Server 代理作业任务已经失败。 可以发生该情况的一种情形是远程服务器已关闭且代理未响应。 但是，只要代理激发，父包就会成功完成其任务。  
  
> [!NOTE]  
>  可以使用包含 **sp_start_job N'package_name'** 的 Transact-SQL 语句的执行 SQL 任务。 有关详细信息，请参阅 [sp_start_job (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-start-job-transact-sql)。  
  
## <a name="debugging-environment"></a>调试环境  
 测试父包时，请在设计器的调试环境中通过使用“调试”/“启动调试”(F5) 来运行父包。 另外，还可以使用命令提示符实用工具 **dtexec**。 有关详细信息，请参阅 [dtexec Utility](packages/dtexec-utility.md)。  
  
  
