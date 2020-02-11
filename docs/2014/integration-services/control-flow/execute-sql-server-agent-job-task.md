---
title: “执行 SQL Server 代理作业”任务 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.executesqlserveragentjobtask.f1
helpviewer_keywords:
- Execute SQL Server Agent Job task [Integration Services]
- jobs [Integration Services]
- SQL Server Agent [Integration Services]
ms.assetid: 3aa3bc0e-1a1c-452e-81b8-b4e3422ea053
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 5f91fcb7033dfe2944e863d67a6c6bf53434e6db
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62831920"
---
# <a name="execute-sql-server-agent-job-task"></a>“执行 SQL Server 代理作业”任务
  “执行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业”任务运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理是一[!INCLUDE[msCoName](../../includes/msconame-md.md)]种 Windows 服务，它运行在 SQL Server 的实例中定义的作业。 您可以创建作业来执行 Transact-SQL 语句和 ActiveX 脚本、执行 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 和复制的维护任务或运行包。 你还可以配置作业以监视[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]并激发警报。 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业通常用来自动执行需要重复执行的任务。 有关详细信息，请参阅 [执行作业](../../ssms/agent/implement-jobs.md)。  
  
 通过使用“执行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理”作业任务，包可以执行与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件有关的管理任务。 例如， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业可以运行系统存储过程（如 **sp_enum_dtspackages** ）来获取文件夹中包的列表。  
  
> [!NOTE]  
>  
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理必须处于运行状态，本地或多服务器管理作业才能自动运行。  
  
 此任务封装 **sp_start_job** 系统过程并把 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业的名称作为参数传递给该过程。 有关详细信息，请参阅 [sp_start_job (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-start-job-transact-sql)。  
  
## <a name="configuring-the-execute-sql-server-agent-job-task"></a>配置“执行 SQL Server 代理作业”任务  
 可以通过 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器来设置属性。 此任务位于 **设计器中** “工具箱” **的** “维护计划中的任务” [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 部分。  
  
 有关可在 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器中设置的属性的详细信息，请单击以下主题：  
  
-   [&#40;维护计划执行 SQL Server 代理作业任务&#41;](../../relational-databases/maintenance-plans/execute-sql-server-agent-job-task-maintenance-plan.md)  
  
 有关如何在 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器中设置这些属性的详细信息，请单击下列主题：  
  
-   [设置任务或容器的属性](../set-the-properties-of-a-task-or-container.md)  
  
  
