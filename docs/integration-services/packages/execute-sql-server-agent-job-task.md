---
title: "“执行 SQL Server 代理作业”任务 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.executesqlserveragentjobtask.f1"
helpviewer_keywords: 
  - "“执行 SQL Server 代理作业”任务 [Integration Services]"
  - "作业 [Integration Services]"
  - "SQL Server 代理 [Integration Services]"
ms.assetid: 3aa3bc0e-1a1c-452e-81b8-b4e3422ea053
caps.latest.revision: 44
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 44
---
# “执行 SQL Server 代理作业”任务
  “执行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业”任务运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理是一个 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 服务，它运行那些已在 SQL Server 实例中定义的作业。 您可以创建作业来执行 Transact-SQL 语句和 ActiveX 脚本、执行 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 和复制的维护任务或运行包。 还可以配置作业以监视 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 并激发警报。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业通常用来自动执行需要重复执行的任务。 有关详细信息，请参阅[执行作业](../../ssms/agent/implement-jobs.md)。  
  
 通过使用“执行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理”作业任务，包可以执行与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件有关的管理任务。 例如，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业可以运行系统存储过程（如 **sp_enum_dtspackages**）来获取文件夹中包的列表。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理必须处于运行状态，本地或多服务器管理作业才能自动运行。  
  
 此任务封装 **sp_start_job** 系统过程并把 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业的名称作为参数传递给该过程。 有关详细信息，请参阅 [sp_start_job (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md)。  
  
## 配置“执行 SQL Server 代理作业”任务  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器来设置属性。 此任务位于 **设计器中** “工具箱” **的** “维护计划中的任务” [!INCLUDE[ssIS](../../includes/ssis-md.md)] 部分。  
  
 有关可在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置的属性的详细信息，请单击以下主题：  
  
-   [“执行 SQL Server 代理作业”任务（维护计划）](../../relational-databases/maintenance-plans/execute-sql-server-agent-job-task-maintenance-plan.md)  
  
 有关如何在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置这些属性的详细信息，请单击下列主题：  
  
-   [设置任务或容器的属性](../Topic/Set%20the%20Properties%20of%20a%20Task%20or%20Container.md)  
  
  