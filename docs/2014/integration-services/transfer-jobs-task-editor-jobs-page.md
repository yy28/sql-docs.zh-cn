---
title: 传输作业任务编辑器（"作业" 页） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transferjobstask.jobs.f1
helpviewer_keywords:
- Transfer Jobs Task Editor
ms.assetid: e72b1dc7-8cda-4ee6-abb5-d438370f04df
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 0c430f08b4a86c981df5138c7f78e76b54e7de28
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84972822"
---
# <a name="transfer-jobs-task-editor-jobs-page"></a>传输作业任务编辑器（“作业”页）
  可以使用 **“传输作业任务编辑器”** 对话框的 **“作业”** 页，指定用于将一个或多个 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 代理作业从一个 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例复制到另一个实例的属性。 有关传输作业任务的详细信息，请参阅 [Transfer Jobs Task](control-flow/transfer-jobs-task.md)。  
  
> [!NOTE]  
>  若要访问源服务器上的作业，用户必须至少是该服务器上 **SQLAgentUserRole** 固定数据库角色的成员。 若要在目标服务器上成功创建作业，用户必须是 **sysadmin** 固定服务器角色或某个 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 代理固定数据库角色的成员。 有关 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 代理的固定数据库角色及其权限的详细信息，请参阅 [SQL Server 代理固定数据库角色](../ssms/agent/sql-server-agent-fixed-database-roles.md)。  
  
## <a name="options"></a>选项  
 **SourceConnection**  
 在列表中选择一个 SMO 连接管理器，或单击 "新建与 **\<New connection...>** 源服务器的连接"。  
  
 **DestinationConnection**  
 在列表中选择一个 SMO 连接管理器，或单击 "新建与 **\<New connection...>** 目标服务器的连接"。  
  
 **TransferAllJobs**  
 选择该任务是应将全部的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 代理作业还是仅将指定的作业从源服务器复制到目标服务器。  
  
 此属性具有下表所列的选项：  
  
|值|说明|  
|-----------|-----------------|  
|**True**|复制所有作业。|  
|**False**|仅复制指定的作业。|  
  
 **JobsList**  
 单击浏览按钮 **（...）** 以选择要复制的作业。 必须至少选择一个作业。  
  
> [!NOTE]  
>  在选择要复制的作业前，请指定 **SourceConnection** 。  
  
 在 **TransferAllJobs** 设置为 **True** 时， **JobsList**选项不可用。  
  
 **IfObjectExists**  
 选择该任务应如何处理在目标服务器上已存在的同名作业。  
  
 此属性具有下表所列的选项：  
  
|值|说明|  
|-----------|-----------------|  
|**FailTask**|如果目标服务器上已存在同名的作业，则任务失败。|  
|**Overwrite**|任务将覆盖目标服务器上同名的作业。|  
|**Skip**|任务将跳过目标服务器上存在的同名作业。|  
  
 **EnableJobsAtDestination**  
 选择是否应启用复制到目标服务器上的作业。  
  
 此属性具有下表所列的选项：  
  
|值|说明|  
|-----------|-----------------|  
|**True**|启用目标服务器上的作业。|  
|**False**|禁用目标服务器上的作业。|  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Integration Services 任务](control-flow/integration-services-tasks.md)   
 [传输作业任务编辑器 &#40;常规 "页面&#41;](general-page-of-integration-services-designers-options.md)   
 [表达式页](expressions/expressions-page.md)   
 [SMO 连接管理器](connection-manager/smo-connection-manager.md)  
  
  
