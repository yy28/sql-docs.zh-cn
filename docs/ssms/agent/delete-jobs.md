---
title: 删除作业 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- delete jobs
ms.assetid: bffb915e-bc84-4417-aa35-183243ca3312
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: d2368c80a1de2ae6eb44a9c8dbcd41aef9394f48
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="delete-jobs"></a>删除作业
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL 数据库托管实例](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支持大多数但并非所有 SQL Server 代理功能。 有关详细信息，请参阅 [Azure SQL 数据库托管实例与 SQL Server 之间的 T-SQL 差异](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

作业是一系列由 SQL Server 代理按顺序执行的指定操作。 默认情况下，执行完成时不删除作业。 无论该作业是否成功，你都可以删除一个或多个 [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理作业。 还可以配置 [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理以在作业成功、失败或完成时自动将其删除。  
  
默认情况下， **sysadmin** 固定服务器角色的成员可以执行 [sp_delete_job (Transact-SQL)](http://msdn.microsoft.com/en-us/b85db6e4-623c-41f1-9643-07e5ea38db09) 系统存储过程或删除某一作业。 其他用户必须被授予 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] msdb **数据库中下列** 代理固定数据库角色的权限之一：  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
有关这些角色的权限的详细信息，请参阅 [SQL Server 代理固定数据库角色](../../ssms/agent/sql-server-agent-fixed-database-roles.md)。  
  
**sysadmin** 固定服务器角色成员可以通过执行 **sp_delete_job** 删除任何作业。 非 **sysadmin** 固定服务器角色成员的用户只能删除该用户所拥有的作业。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|||  
|-|-|  
|**Description**|**主题**|  
|介绍如何删除一个或多个 [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理作业。|[删除一个或多个作业](../../ssms/agent/delete-one-or-more-jobs.md)|  
|介绍如何配置 [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理，以在作业成功、失败或完成时自动将其删除。|[Automatically Delete a Job](../../ssms/agent/automatically-delete-a-job.md)|  
  
