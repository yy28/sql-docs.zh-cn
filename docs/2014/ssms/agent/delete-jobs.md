---
title: 删除作业 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- delete jobs
ms.assetid: bffb915e-bc84-4417-aa35-183243ca3312
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2afa9d161085a6907d14e536d2fef65b1b85ee46
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48101079"
---
# <a name="delete-jobs"></a>删除作业
  作业是一系列由 SQL Server 代理按顺序执行的指定操作。 默认情况下，执行完成时不删除作业。 无论该作业是否成功，你都可以删除一个或多个 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业。 还可以配置 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理以在作业成功、失败或完成时自动将其删除。  
  
 默认情况下的成员**sysadmin**固定的服务器角色可以执行[sp_delete_job &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-delete-job-transact-sql)系统存储过程来删除作业。 其他用户必须被授予 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **数据库中下列** 代理固定数据库角色的权限之一：  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 有关这些角色的权限的详细信息，请参阅 [SQL Server 代理固定数据库角色](sql-server-agent-fixed-database-roles.md)。  
  
 **sysadmin** 固定服务器角色成员可以通过执行 **sp_delete_job** 删除任何作业。 非 **sysadmin** 固定服务器角色成员的用户只能删除该用户所拥有的作业。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|||  
|-|-|  
|**Description**|**主题**|  
|介绍如何删除一个或多个 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业。|[删除一个或多个作业](delete-one-or-more-jobs.md)|  
|介绍如何配置 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理，以在作业成功、失败或完成时自动将其删除。|[Automatically Delete a Job](automatically-delete-a-job.md)|  
  
  
