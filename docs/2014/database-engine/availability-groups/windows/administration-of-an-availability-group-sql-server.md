---
title: 管理可用性组 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Availability Groups [SQL Server], managing
ms.assetid: 0b7542fa-235e-413d-81bf-3eff9ee07480
caps.latest.revision: 18
author: rothja
ms.author: jroth
manager: jhubbard
ms.openlocfilehash: 57452567fcc01aef2bce0908a8ada4b4395c1425
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36017188"
---
# <a name="administration-of-an-availability-group-sql-server"></a>管理可用性组 (SQL Server)
  在 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 中管理现有 AlwaysOn 可用性组涉及以下一个或多个任务：  
  
-   更改现有可用性副本的属性以便更改客户端连接访问（用于配置可读的辅助副本）等，更改其故障转移模式、可用性模式或会话超时设置。  
  
-   添加或删除辅助副本。  
  
-   添加或删除数据库。  
  
-   暂停或恢复数据库。  
  
-   执行计划的手动故障转移（手动故障转移）或强制手动故障转移（强制故障转移）。  
  
-   创建和配置可用性组侦听器。  
  
-   为某一给定可用性组管理 [可读次要副本](active-secondaries-readable-secondary-replicas-always-on-availability-groups.md) 。 这涉及在以辅助角色运行时将一个或多个副本配置为只读访问以及配置只读路由。  
  
-   为某一给定可用性组管理 [次要副本上的备份](active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md) 。 这涉及配置您希望运行备份作业的位置，然后编写备份作业脚本，以便实现您的备份首选项。 在承载可用性副本的每个 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例上，对于可用性组中的每个数据库，您都需要为备份作业编写脚本。  
  
-   删除可用性组。  
  
-   针对操作系统升级的 AlwaysOn 可用性组的跨群集迁移  
  
  
##  <a name="RelatedTasks"></a> 相关任务  
 **配置现有的可用性组**  
  
-   [将辅助副本添加到可用性组 (SQL Server)](add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [将次要副本从可用性组删除 (SQL Server)](remove-a-secondary-replica-from-an-availability-group-sql-server.md)  
  
-   [将数据库添加到可用性组 (SQL Server)](availability-group-add-a-database.md)  
  
-   [将辅助数据库从可用性组删除 (SQL Server)](remove-a-secondary-database-from-an-availability-group-sql-server.md)  
  
-   [将主数据库从可用性组删除 (SQL Server)](remove-a-primary-database-from-an-availability-group-sql-server.md)  
  
-   [配置灵活的故障转移策略以控制自动故障转移的条件&#40;AlwaysOn 可用性组&#41;](configure-flexible-automatic-failover-policy.md)  
  
 **管理可用性组**  
  
-   [配置可用性副本备份 (SQL Server)](configure-backup-on-availability-replicas-sql-server.md)  
  
-   [执行可用性组的计划手动故障转移 (SQL Server)](perform-a-planned-manual-failover-of-an-availability-group-sql-server.md)  
  
-   [执行可用性组的强制手动故障转移 (SQL Server)](perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)  
  
-   [删除可用性组 (SQL Server)](remove-an-availability-group-sql-server.md)  
  
 **管理可用性副本**  
  
-   [将辅助副本添加到可用性组 (SQL Server)](add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [将辅助副本联接到可用性组 (SQL Server)](join-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [将次要副本从可用性组删除 (SQL Server)](remove-a-secondary-replica-from-an-availability-group-sql-server.md)  
  
-   [更改可用性副本的可用性模式 (SQL Server)](change-the-availability-mode-of-an-availability-replica-sql-server.md)  
  
-   [更改可用性副本的故障转移模式 (SQL Server)](change-the-failover-mode-of-an-availability-replica-sql-server.md)  
  
-   [配置可用性副本备份 (SQL Server)](configure-backup-on-availability-replicas-sql-server.md)  
  
-   [配置对可用性副本的只读访问 (SQL Server)](configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [为可用性组配置只读路由 (SQL Server)](configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
-   [更改可用性副本的会话超时期限 (SQL Server)](change-the-session-timeout-period-for-an-availability-replica-sql-server.md)  
  
 **管理可用性数据库**  
  
-   [将数据库添加到可用性组 (SQL Server)](availability-group-add-a-database.md)  
  
-   [将辅助数据库联接到可用性组 (SQL Server)](join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
-   [将主数据库从可用性组删除 (SQL Server)](remove-a-primary-database-from-an-availability-group-sql-server.md)  
  
-   [将辅助数据库从可用性组删除 (SQL Server)](remove-a-secondary-database-from-an-availability-group-sql-server.md)  
  
-   [挂起可用性数据库 (SQL Server)](suspend-an-availability-database-sql-server.md)  
  
-   [恢复可用性数据库 (SQL Server)](resume-an-availability-database-sql-server.md)  
  
 **监视可用性组**  
  
-   [监视可用性组 (SQL Server)](monitoring-of-availability-groups-sql-server.md)  
  
 **为了支持将可用性组迁移到新的 WSFC 群集（跨群集迁移）**  
  
-   [更改服务器实例的 HADR 群集上下文 (SQL Server)](change-the-hadr-cluster-context-of-server-instance-sql-server.md)  
  
-   [使可用性组脱机 (SQL Server)](../../take-an-availability-group-offline-sql-server.md)  
  
  
##  <a name="RelatedContent"></a> 相关内容  
  
-   **博客：**  
  
     [SQL Server AlwaysOn 团队博客： SQL Server AlwaysOn 团队官方博客](http://blogs.msdn.com/b/sqlalwayson/)  
  
     [CSS SQL Server 工程师博客](http://blogs.msdn.com/b/psssql/)  
  
-   **视频：**  
  
     [Microsoft SQL Server Code-Named"Denali"AlwaysOn 系列，第 1 部分： 简介下一代高可用性解决方案](http://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI302)  
  
     [Microsoft SQL Server Code-Named"Denali"AlwaysOn 系列，第 2 部分： 生成任务关键型高可用性解决方案使用 AlwaysOn](http://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI404)  
  
-   **白皮书：**  
  
     [针对 SQL Server 2012 的 Microsoft 白皮书](http://msdn.microsoft.com/library/hh403491.aspx)  
  
     [SQL Server 客户咨询团队白皮书](http://sqlcat.com/)  
  
  
## <a name="see-also"></a>请参阅  
 [AlwaysOn 可用性组&#40;SQL Server&#41;](always-on-availability-groups-sql-server.md)   
 [AlwaysOn 可用性组概述&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [AlwaysOn 可用性组的服务器实例配置&#40;SQL Server&#41;](configuration-of-a-server-instance-for-always-on-availability-groups-sql-server.md)  
 [创建和配置可用性组 (SQL Server)](creation-and-configuration-of-availability-groups-sql-server.md)   
 [活动辅助副本： 可读辅助副本&#40;AlwaysOn 可用性组&#41;](active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)   
 [活动辅助副本： 辅助副本上备份&#40;AlwaysOn 可用性组&#41;](active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)  
 [可用性组侦听程序、客户端连接和应用程序故障转移 &#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md)   
 [针对 AlwaysOn 可用性组运行问题的 AlwaysOn 策略&#40;SQL Server&#41;](always-on-policies-for-operational-issues-always-on-availability.md)   
 [监视可用性组 (SQL Server)](monitoring-of-availability-groups-sql-server.md)   
 [AlwaysOn 可用性组： 互操作性&#40;SQL Server&#41;](always-on-availability-groups-interoperability-sql-server.md)   
 [AlwaysOn 可用性组的 TRANSACT-SQL 语句概述&#40;SQL Server&#41;](transact-sql-statements-for-always-on-availability-groups.md)   
 [AlwaysOn 可用性组的 PowerShell Cmdlet 概述&#40;SQL Server&#41;](overview-of-powershell-cmdlets-for-always-on-availability-groups-sql-server.md)  
  
  