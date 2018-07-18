---
title: 创建和配置可用性组 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], deploying
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], creating
ms.assetid: 7f89fab8-6ee2-4273-9de0-e594bfb9407f
caps.latest.revision: 27
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 85c1b9717d27e1298b5e638e3f2788215c73c6ea
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37156938"
---
# <a name="creation-and-configuration-of-availability-groups-sql-server"></a>创建和配置可用性组 (SQL Server)
  本节中的主题介绍如何在 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 实例（这些实例驻留在单个 WSFC 故障转移群集内的不同 Windows Server 故障转移群集 (WSFC) 节点上）上部署 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 实现。  
  
 在创建您的第一个可用性组前，我们强烈建议您首先熟悉以下主题中的内容：  
  
 [先决条件、 限制和建议为 AlwaysOn 可用性组&#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)  
 此主题说明针对计算机、WSFC 节点、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]实例、可用性组、副本和数据库的先决条件、限制和建议。 此主题还包含有关安全注意事项的信息。  
  
 [AlwaysOn 可用性组入门&#40;SQL Server&#41;](getting-started-with-always-on-availability-groups-sql-server.md)  
 包含以下相关步骤信息：配置服务器实例、创建可用性组、为客户端连接配置可用性组、管理可用性组和监视可用性组。  
  
 
  
##  <a name="RelatedTasks"></a> 相关任务  
 **配置 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]**  
  
-   [启用和禁用 AlwaysOn 可用性组 (SQL Server)](enable-and-disable-always-on-availability-groups-sql-server.md)  
  
-   [创建数据库镜像端点的 AlwaysOn 可用性组&#40;SQL Server PowerShell&#41;](database-mirroring-always-on-availability-groups-powershell.md)  
  
-   [为 Windows 身份验证创建数据库镜像终结点 (Transact-SQL)](../../database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
-   [允许数据库镜像终结点使用证书进行出站连接 (Transact-SQL)](../../database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md)  
  
 **若要配置 AlwaysOn 可用性组入门**  
  
-   [AlwaysOn 可用性组入门&#40;SQL Server&#41;](getting-started-with-always-on-availability-groups-sql-server.md)  
  
 **创建和配置新的可用性组**  
  
-   [使用可用性组向导 (SQL Server Management Studio)](use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [创建可用性组 (Transact-SQL)](create-an-availability-group-transact-sql.md)  
  
-   [创建可用性组 (SQL Server PowerShell)](../../../powershell/sql-server-powershell.md)  
  
-   [使用“新建可用性组”对话框 (SQL Server Management Studio)](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [在添加或修改可用性副本时指定终结点 URL (SQL Server)](specify-endpoint-url-adding-or-modifying-availability-replica.md)  
  
-   [创建或配置可用性组侦听程序 (SQL Server)](create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [配置灵活的故障转移策略以控制自动故障转移 （AlwaysOn 可用性组） 的条件](configure-flexible-automatic-failover-policy.md)  
  
-   [配置可用性副本备份 (SQL Server)](configure-backup-on-availability-replicas-sql-server.md)  
  
-   [配置对可用性副本的只读访问 (SQL Server)](configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [为可用性组配置只读路由 (SQL Server)](configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
-   [将辅助副本联接到可用性组 (SQL Server)](join-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [启动 AlwaysOn 辅助数据库的数据移动&#40;SQL Server&#41;](start-data-movement-on-an-always-on-secondary-database-sql-server.md)  
  
-   [为可用性组手动准备辅助数据库 (SQL Server)](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
-   [将辅助数据库联接到可用性组 (SQL Server)](join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
-   [管理可用性组中数据库的登录名和作业 (SQL Server)](../../logins-and-jobs-for-availability-group-databases.md)  
  
 **故障排除**  
  
-   [解决 AlwaysOn 可用性组配置 (SQL Server) 删除问题](troubleshoot-always-on-availability-groups-configuration-sql-server.md)  
  
-   [解决失败的添加文件操作问题&#40;AlwaysOn 可用性组&#41;](troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md)  
  
##  <a name="RelatedContent"></a> 相关内容  
  
-   **博客：**  
  
     [AlwaysON-HADRON 学习系列： 启用了 HADRON 的工作线程池用法的数据库](http://blogs.msdn.com/b/psssql/archive/2012/05/17/alwayson-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases.aspx)  
  
     [SQL Server AlwaysOn 团队博客： SQL Server AlwaysOn 官方团队博客](http://blogs.msdn.com/b/sqlalwayson/)  
  
     [CSS SQL Server 工程师博客](http://blogs.msdn.com/b/psssql/)  
  
-   **视频：**  
  
     [Microsoft SQL Server Code-Named"Denali"AlwaysOn 系列，第一部分： 介绍下一代高可用性解决方案](http://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI302)  
  
     [Microsoft SQL Server Code-Named"Denali"AlwaysOn 系列，第 2 部分： 生成使用 AlwaysOn 的关键任务高可用性解决方案](http://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI404)  
  
-   **白皮书：**  
  
     [Microsoft SQL Server AlwaysOn 解决方案指南有关高可用性和灾难恢复](http://go.microsoft.com/fwlink/?LinkId=227600)  
  
     [针对 SQL Server 2012 的 Microsoft 白皮书](http://msdn.microsoft.com/library/hh403491.aspx)  
  
     [SQL Server 客户咨询团队白皮书](http://sqlcat.com/)  
  
## <a name="see-also"></a>请参阅  
 [AlwaysOn 可用性组概述&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [管理可用性组 (SQL Server)](administration-of-an-availability-group-sql-server.md)   
 [针对运行问题的 AlwaysOn 可用性组 (SQL Server) 的 AlwaysOn 策略](always-on-policies-for-operational-issues-always-on-availability.md)   
 [监视可用性组 (SQL Server)](monitoring-of-availability-groups-sql-server.md)   
 [AlwaysOn 可用性组： 互操作性 (SQL Server)](always-on-availability-groups-interoperability-sql-server.md)  
  
  
