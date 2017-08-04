---
title: "传输主存储的过程任务 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.transfermasterspstask.f1
helpviewer_keywords:
- Transfer Master Stored Procedures task [Integration Services]
ms.assetid: 81702560-48a3-46d1-a469-e41304c7af8e
caps.latest.revision: 25
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b309790e8ac39e9ac978c56bc451cfd68c5e3c75
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="transfer-master-stored-procedures-task"></a>传输主存储过程任务
  传输主存储过程任务在 **的实例上的** master [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库之间传输一个或多个用户定义的存储过程。 若要从 **master** 数据库传输存储过程，该过程的所有者必须是 dbo。  
  
 传输主存储过程任务可以配置为传输所有存储过程，也可以配置为只传输指定的存储过程。 此任务并不复制系统存储过程。  
  
 要传输的主存储过程可能已经存在于目标服务器上。 传输主存储过程可以配置为以下列方式处理现有存储过程：  
  
-   覆盖现有存储过程。  
  
-   如果存在重复的存储过程，则该任务失败。  
  
-   跳过重复的存储过程。  
  
 在运行时，传输主存储过程任务使用两个 SMO 连接管理器连接到源服务器和目标服务器。 SMO 连接管理器与传输主存储过程任务分开进行配置，然后在传输主存储过程任务中引用连接管理器。 SMO 连接管理器指定服务器以及在访问该服务器时要使用的身份验证模式。 有关详细信息，请参阅 [SMO Connection Manager](../../integration-services/connection-manager/smo-connection-manager.md)。  
  
## <a name="transferring-stored-procedures-between-instances-of-sql-server"></a>在 SQL Server 实例之间传输存储过程  
 传输主存储过程任务支持 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 源和目标。  
  
## <a name="events"></a>事件  
 该任务将引发报告已传输的存储过程数的信息事件，而且在覆盖存储过程时还会引发警告事件。  
  
 传输主存储过程任务并不报告存储过程传输的进度；它仅报告 0% 和 100 % 完成。  
  
## <a name="execution-value"></a>执行值  
 在该任务的 **ExecutionValue** 属性中定义的执行值返回已传输的存储过程数。 通过将用户定义的变量分配给传输主存储过程任务的 **ExecValueVariable** 属性，包中的其他对象就可以访问有关存储过程传输的信息。 有关详细信息，请参阅 [Integration Services (SSIS) 变量](../../integration-services/integration-services-ssis-variables.md)和[在包中使用变量](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)。  
  
## <a name="log-entries"></a>日志项  
 传输主存储过程任务包括下列自定义日志项：  
  
-   TransferStoredProceduresTaskStartTransferringObjects   此日志项报告传输已经开始。 日志项包括开始时间。  
  
-   TransferSStoredProceduresTaskFinishedTransferringObjects  此日志项报告传输已经完成。 日志项包括结束时间。  
  
 此外， **OnInformation** 事件的日志项报告已传输的存储过程数， **OnWarning** 事件的日志项是为目标服务器上被覆盖的每个存储过程写入的。  
  
## <a name="security-and-permissions"></a>安全性和权限  
 用户必须具有查看源服务器上 **master** 数据库中的存储过程列表的权限，而且必须是 sysadmin 服务器角色的成员，或者必须具有对目标服务器上 **master** 数据库中所创建的存储过程的权限。  
  
## <a name="configuration-of-the-transfer-master-stored-procedures-task"></a>传输主存储过程任务的配置  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 有关可以在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置的属性的信息，请单击以下主题之一：  
  
-   [传输主存储过程任务编辑器（“常规”页）](../../integration-services/control-flow/transfer-master-stored-procedures-task-editor-general-page.md)  
  
-   [传输主存储过程任务编辑器（“存储过程”页）](../../integration-services/control-flow/transfer-master-stored-procedures-task-editor-stored-procedures-page.md)  
  
-   [“表达式”页](../../integration-services/expressions/expressions-page.md)  
  
 有关以编程方式设置这些属性的信息，请单击以下主题：  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferStoredProceduresTask.TransferStoredProceduresTask>  
  
### <a name="configuring-the-transfer-master-stored-procedures-task-programmatically"></a>以编程方式配置传输主存储过程任务  
  
## <a name="related-tasks"></a>相关任务  
 有关如何在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置这些属性的详细信息，请单击下列主题：  
  
-   [设置任务或容器的属性](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="see-also"></a>另请参阅  
 [传输 SQL Server 对象任务](../../integration-services/control-flow/transfer-sql-server-objects-task.md)   
 [Integration Services 任务](../../integration-services/control-flow/integration-services-tasks.md)   
 [控制流](../../integration-services/control-flow/control-flow.md)  
  
  
