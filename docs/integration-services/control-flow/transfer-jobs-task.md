---
title: "传输作业任务 |Microsoft 文档"
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
- sql13.dts.designer.transferjobstask.f1
- sql13.dts.designer.transferjobstask.general.f1
- sql13.dts.designer.transferjobstask.jobs.f1
helpviewer_keywords:
- Transfer Jobs task [Integration Services]
ms.assetid: 1bf33885-9c5b-47e4-a549-f5920b66a1de
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 8806c102eaec2c2540374bfaddc33b76d8f6e584
ms.openlocfilehash: a4264d737901fbb7c023e216d3d8faf5309469f9
ms.contentlocale: zh-cn
ms.lasthandoff: 08/11/2017

---
# <a name="transfer-jobs-task"></a>传输作业任务
  传输作业任务在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例之间传输一个或多个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理作业。  
  
 传输作业任务可以配置为传输所有作业，或者只传输指定的作业。 您还可以指示是否在目标服务器上启用传输的作业。  
  
 要传输的作业可能已经存在于目标服务器上。 传输作业任务可以配置为以下列方式处理现有作业：  
  
-   覆盖现有作业。  
  
-   如果存在重复作业，则该任务失败。  
  
-   跳过重复作业。  
  
 在运行时，传输作业任务使用一个或两个 SMO 连接管理器连接到源服务器和目标服务器。 SMO 连接管理器与传输作业任务分开进行配置，然后在传输作业任务中引用连接管理器。 SMO 连接管理器指定服务器以及在访问该服务器时要使用的身份验证模式。 有关详细信息，请参阅 [SMO Connection Manager](../../integration-services/connection-manager/smo-connection-manager.md)。  
  
## <a name="transferring-jobs-between-instances-of-sql-server"></a>在 SQL Server 实例之间传输作业  
 传输作业任务支持 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 源和目标。 对于使用哪个版本作为源或目标，没有限制。  
  
## <a name="events"></a>事件  
 传输作业任务将引发报告已传输的作业数的信息事件，而且在覆盖作业时还会引发警告事件。 该任务并不报告作业传输的进度，它仅报告 0% 和 100% 完成。  
  
## <a name="execution-value"></a>执行值  
 在该任务的 **ExecutionValue** 属性中定义的执行值返回已传输的作业数。 通过将用户定义的变量分配给传输作业任务的 **ExecValueVariable** 属性，包中的其他对象就可以访问有关作业传输的信息。 有关详细信息，请参阅 [Integration Services (SSIS) 变量](../../integration-services/integration-services-ssis-variables.md)和[在包中使用变量](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)。  
  
## <a name="log-entries"></a>日志项  
 传输作业任务包括下列自定义日志项：  
  
-   TransferJobsTaskStarTransferringObjects   此日志项报告传输已经开始。 日志项包括开始时间。  
  
-   TransferJobsTaskFinishedTransferringObjects    此日志项报告传输已经完成。 日志项包括结束时间。  
  
 此外，还有 **OnInformation** 事件的日志项（报告已传输的作业数），以及 **OnWarning** 事件的日志项（是为目标服务器上每个被覆盖的作业写入的）。  
  
## <a name="security-and-permissions"></a>安全性和权限  
 若要传输作业，用户必须是 sysadmin 固定服务器角色的成员，或者是同时位于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的源实例和目标实例上的 msdb 数据库的固定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理固定数据库角色的成员。  
  
## <a name="configuration-of-the-transfer-jobs-task"></a>传输作业任务的配置  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 有关可在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置的属性的信息，请单击以下主题：  
  
-   [“表达式”页](../../integration-services/expressions/expressions-page.md)  
  
 有关以编程方式设置这些属性的信息，请单击下列主题之一：  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferJobsTask.TransferJobsTask>  
  
## <a name="related-tasks"></a>相关任务  
 有关如何在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置这些属性的详细信息，请单击下列主题：  
  
-   [设置任务或容器的属性](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="transfer-jobs-task-editor-general-page"></a>传输作业任务编辑器（“常规”页）
  可以使用 **“传输作业任务编辑器”** 对话框的 **“常规”** 页，对传输作业任务进行命名和说明。  
  
> [!NOTE]  
>  只有目标服务器上 **sysadmin** 固定服务器角色或某个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理固定数据库角色的成员才能在其中成功创建作业。 若要访问源服务器上的作业，用户必须是该服务器上 **SQLAgentUserRole** 固定数据库角色的成员。 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理的固定数据库角色及其权限的详细信息，请参阅 [SQL Server 代理固定数据库角色](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79)。  
  
### <a name="options"></a>选项  
 **名称**  
 为传输作业任务键入唯一的名称。 此名称用作任务图标中的标签。  
  
> [!NOTE]  
>  任务名称在一个包内必须是唯一的。  
  
 **Description**  
 键入传输作业任务的说明。  
  
## <a name="transfer-jobs-task-editor-jobs-page"></a>传输作业任务编辑器（“作业”页）
  可以使用 **“传输作业任务编辑器”** 对话框的 **“作业”** 页，指定用于将一个或多个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业从一个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例复制到另一个实例的属性。  
  
> [!NOTE]  
>  若要访问源服务器上的作业，用户必须至少是该服务器上 **SQLAgentUserRole** 固定数据库角色的成员。 若要在目标服务器上成功创建作业，用户必须是 **sysadmin** 固定服务器角色或某个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理固定数据库角色的成员。 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理的固定数据库角色及其权限的详细信息，请参阅 [SQL Server 代理固定数据库角色](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79)。  
  
### <a name="options"></a>选项  
 **SourceConnection**  
 在列表中，选择 SMO 连接管理器，或单击**\<新连接 … >**创建与源服务器的新连接。  
  
 **DestinationConnection**  
 在列表中，选择 SMO 连接管理器，或单击**\<新连接 … >**以创建新的连接到目标服务器。  
  
 **TransferAllJobs**  
 选择该任务是应将全部的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业还是仅将指定的作业从源服务器复制到目标服务器。  
  
 此属性具有下表所列的选项：  
  
|“值”|Description|  
|-----------|-----------------|  
|**True**|复制所有作业。|  
|**False**|仅复制指定的作业。|  
  
 **JobsList**  
 单击浏览按钮 **(…)** 可选择要复制的作业。 必须至少选择一个作业。  
  
> [!NOTE]  
>  在选择要复制的作业前，请指定 **SourceConnection** 。  
  
 在 **TransferAllJobs** 设置为 **True** 时， **JobsList**选项不可用。  
  
 **IfObjectExists**  
 选择该任务应如何处理在目标服务器上已存在的同名作业。  
  
 此属性具有下表所列的选项：  
  
|“值”|Description|  
|-----------|-----------------|  
|**FailTask**|如果目标服务器上已存在同名的作业，则任务失败。|  
|**Overwrite**|任务将覆盖目标服务器上同名的作业。|  
|**Skip**|任务将跳过目标服务器上存在的同名作业。|  
  
 **EnableJobsAtDestination**  
 选择是否应启用复制到目标服务器上的作业。  
  
 此属性具有下表所列的选项：  
  
|“值”|Description|  
|-----------|-----------------|  
|**True**|启用目标服务器上的作业。|  
|**False**|禁用目标服务器上的作业。|  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 任务](../../integration-services/control-flow/integration-services-tasks.md)   
 [控制流](../../integration-services/control-flow/control-flow.md)  
  
  
