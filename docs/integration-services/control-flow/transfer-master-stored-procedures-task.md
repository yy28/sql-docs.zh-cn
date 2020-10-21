---
description: 传输主存储过程任务
title: 传输主存储过程任务 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.transfermasterspstask.f1
- sql13.dts.designer.transferstoredprocedurestask.general.f1
- sql13.dts.designer.transferstoredprocedurestask.storedprocedures.f1
helpviewer_keywords:
- Transfer Master Stored Procedures task [Integration Services]
ms.assetid: 81702560-48a3-46d1-a469-e41304c7af8e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a053581c9f6ca8f9592aef42c1649511ecc51a02
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2020
ms.locfileid: "92194219"
---
# <a name="transfer-master-stored-procedures-task"></a>传输主存储过程任务

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


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
 在该任务的 **ExecutionValue** 属性中定义的执行值返回已传输的存储过程数。 通过将用户定义的变量分配给传输主存储过程任务的 **ExecValueVariable** 属性，包中的其他对象就可以访问有关存储过程传输的信息。 有关详细信息，请参阅 [Integration Services (SSIS) 变量](../../integration-services/integration-services-ssis-variables.md)和[在包中使用变量](../integration-services-ssis-variables.md)。  
  
## <a name="log-entries"></a>日志项  
 传输主存储过程任务包括下列自定义日志项：  
  
-   TransferStoredProceduresTaskStartTransferringObjects   此日志项报告传输已经开始。 日志项包括开始时间。  
  
-   TransferSStoredProceduresTaskFinishedTransferringObjects  此日志项报告传输已经完成。 日志项包括结束时间。  
  
 此外， **OnInformation** 事件的日志项报告已传输的存储过程数， **OnWarning** 事件的日志项是为目标服务器上被覆盖的每个存储过程写入的。  
  
## <a name="security-and-permissions"></a>安全和权限  
 用户必须具有查看源服务器上 **master** 数据库中的存储过程列表的权限，而且必须是 sysadmin 服务器角色的成员，或者必须具有对目标服务器上 **master** 数据库中所创建的存储过程的权限。  
  
## <a name="configuration-of-the-transfer-master-stored-procedures-task"></a>传输主存储过程任务的配置  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 有关可在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置的属性的信息，请单击以下主题：  
  
-   [“表达式”页](../../integration-services/expressions/expressions-page.md)  
  
 有关以编程方式设置这些属性的信息，请单击以下主题：  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferStoredProceduresTask.TransferStoredProceduresTask>  
  
### <a name="configuring-the-transfer-master-stored-procedures-task-programmatically"></a>以编程方式配置传输主存储过程任务  
  
## <a name="related-tasks"></a>Related Tasks  
 有关如何在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置这些属性的详细信息，请单击下列主题：  
  
-   [设置任务或容器的属性](./add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  
## <a name="transfer-master-stored-procedures-task-editor-general-page"></a>传输主存储过程任务编辑器（“常规”页）
  可以使用 **“传输主存储过程任务编辑器”** 对话框的 **“常规”** 页，对传输主存储过程任务进行命名和说明。  
  
> [!NOTE]  
>  此任务只将 **dbo** 拥有的用户定义存储过程从源服务器上的 **master** 数据库传递到目标服务器上的 **master** 数据库。 若要在目标服务器上创建存储过程，必须在目标服务器上的 **master** 数据库中授予用户 CREATE PROCEDURE 权限，或者用户必须为目标服务器上 **sysadmin** 固定服务器角色的成员。  
  
### <a name="options"></a>选项  
 **名称**  
 为传输主存储过程任务键入唯一的名称。 此名称用作任务图标中的标签。  
  
> [!NOTE]  
>  任务名称在一个包内必须是唯一的。  
  
 **说明**  
 键入传输主存储过程任务的说明。  
  
## <a name="transfer-master-stored-procedures-task-editor-stored-procedures-page"></a>传输主存储过程任务编辑器（“存储过程”页）
  可以使用“传输主存储过程任务编辑器”对话框的“存储过程”页，指定用于将一个或多个用户定义存储过程从一个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中的 **master** 数据库复制到另一个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中的 **master** 数据库的属性。  
  
> [!NOTE]  
>  此任务只将 **dbo** 拥有的用户定义存储过程从源服务器上的 **master** 数据库传递到目标服务器上的 **master** 数据库。 若要在目标服务器上创建存储过程，必须在目标服务器上的 **master** 数据库中授予用户 CREATE PROCEDURE 权限，或者用户必须为目标服务器上 **sysadmin** 固定服务器角色的成员。  
  
### <a name="options"></a>选项  
 **SourceConnection**  
 从列表中选择一个 SMO 连接管理器，或单击 \<New connection...> 创建与源服务器的新连接。  
  
 **DestinationConnection**  
 从列表中选择一个 SMO 连接管理器，或单击 \<New connection...> 创建与目标服务器的新连接。  
  
 **IfObjectExists**  
 选择该任务应如何处理目标服务器上的 **master** 数据库中已经存在的同名用户定义存储过程。  
  
 此属性具有下表所列的选项：  
  
|值|说明|  
|-----------|-----------------|  
|**FailTask**|如果目标服务器上的 **master** 数据库中已存在同名的存储过程，则任务失败。|  
|**Overwrite**|任务将覆盖目标服务器上的 **master** 数据库中的同名存储过程。|  
|**Skip**|任务将跳过目标服务器上的 **master** 数据库中存在的同名存储过程。|  
  
 **TransferAllStoredProcedures**  
 选择是否应将源服务器上 **master** 数据库中的所有用户定义存储过程复制到目标服务器。  
  
|值|说明|  
|-----------|-----------------|  
|**True**|复制 **master** 数据库中的所有用户定义存储过程。|  
|**False**|仅复制指定的存储过程。|  
  
 **StoredProceduresList**  
 选择应将源服务器上 **master** 数据库中的哪些用户定义存储过程复制到目标 **master** 数据库。 只有在 **TransferAllStoredProcedures** 设置为 **False**时，此选项才可用。  
  
## <a name="see-also"></a>另请参阅  
 [传输 SQL Server 对象任务](../../integration-services/control-flow/transfer-sql-server-objects-task.md)   
 [Integration Services 任务](../../integration-services/control-flow/integration-services-tasks.md)   
 [控制流](../../integration-services/control-flow/control-flow.md)  
  
