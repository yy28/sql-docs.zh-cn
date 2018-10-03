---
title: 传输主存储过程任务 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transfermasterspstask.f1
helpviewer_keywords:
- Transfer Master Stored Procedures task [Integration Services]
ms.assetid: 81702560-48a3-46d1-a469-e41304c7af8e
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0b7763c8aeffe60c361a9f54ac3c9657653af40a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48150227"
---
# <a name="transfer-master-stored-procedures-task"></a>传输主存储过程任务
  传输主存储过程任务在 **的实例上的** master [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库之间传输一个或多个用户定义的存储过程。 若要从 **master** 数据库传输存储过程，该过程的所有者必须是 dbo。  
  
 传输主存储过程任务可以配置为传输所有存储过程，也可以配置为只传输指定的存储过程。 此任务并不复制系统存储过程。  
  
 要传输的主存储过程可能已经存在于目标服务器上。 传输主存储过程可以配置为以下列方式处理现有存储过程：  
  
-   覆盖现有存储过程。  
  
-   如果存在重复的存储过程，则该任务失败。  
  
-   跳过重复的存储过程。  
  
 在运行时，传输主存储过程任务使用两个 SMO 连接管理器连接到源服务器和目标服务器。 SMO 连接管理器与传输主存储过程任务分开进行配置，然后在传输主存储过程任务中引用连接管理器。 SMO 连接管理器指定服务器以及在访问该服务器时要使用的身份验证模式。 有关详细信息，请参阅 [SMO Connection Manager](../connection-manager/smo-connection-manager.md)。  
  
## <a name="transferring-stored-procedures-between-instances-of-sql-server"></a>在 SQL Server 实例之间传输存储过程  
 传输主存储过程任务支持 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 源和目标。  
  
## <a name="events"></a>事件  
 该任务将引发报告已传输的存储过程数的信息事件，而且在覆盖存储过程时还会引发警告事件。  
  
 传输主存储过程任务并不报告存储过程传输的进度；它仅报告 0% 和 100 % 完成。  
  
## <a name="execution-value"></a>执行值  
 中定义的执行值`ExecutionValue`任务，属性返回传输的存储过程数。 通过将用户定义的变量分配`ExecValueVariable`传输主存储过程任务，有关存储的过程传输的信息的属性可提供给其他对象在包中。 有关详细信息，请参阅 [Integration Services (SSIS) 变量](../integration-services-ssis-variables.md)和[在包中使用变量](../use-variables-in-packages.md)。  
  
## <a name="log-entries"></a>日志项  
 传输主存储过程任务包括下列自定义日志项：  
  
-   TransferStoredProceduresTaskStartTransferringObjects   此日志项报告传输已经开始。 日志项包括开始时间。  
  
-   TransferSStoredProceduresTaskFinishedTransferringObjects  此日志项报告传输已经完成。 日志项包括结束时间。  
  
 此外，一个日志条目`OnInformation`事件报告已传输的存储的过程和一个日志条目的数目`OnWarning`每个存储过程将覆盖目标上写入事件。  
  
## <a name="security-and-permissions"></a>安全性和权限  
 用户必须具有查看源服务器上 **master** 数据库中的存储过程列表的权限，而且必须是 sysadmin 服务器角色的成员，或者必须具有对目标服务器上 **master** 数据库中所创建的存储过程的权限。  
  
## <a name="configuration-of-the-transfer-master-stored-procedures-task"></a>传输主存储过程任务的配置  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式设置属性。  
  
 有关可以在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置的属性的信息，请单击以下主题之一：  
  
-   [传输主存储的过程任务编辑器&#40;常规页&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [传输主存储的过程任务编辑器&#40;存储过程页&#41;](../transfer-master-stored-procedures-task-editor-stored-procedures-page.md)  
  
-   [“表达式”页](../expressions/expressions-page.md)  
  
 有关以编程方式设置这些属性的信息，请单击以下主题：  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferStoredProceduresTask.TransferStoredProceduresTask>  
  
### <a name="configuring-the-transfer-master-stored-procedures-task-programmatically"></a>以编程方式配置传输主存储过程任务  
  
## <a name="related-tasks"></a>Related Tasks  
 有关如何在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置这些属性的详细信息，请单击下列主题：  
  
-   [设置任务或容器的属性](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="see-also"></a>请参阅  
 [传输 SQL Server 对象任务](transfer-sql-server-objects-task.md)   
 [Integration Services 任务](integration-services-tasks.md)   
 [控制流](control-flow.md)  
  
  
