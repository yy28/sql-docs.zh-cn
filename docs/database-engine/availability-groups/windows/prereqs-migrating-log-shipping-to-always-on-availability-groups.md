---
title: 将日志传送迁移到 AlwaysOn 可用性组的先决条件 | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- log shipping [SQL Server], AlwaysOn Availability Groups
- Availability Groups [SQL Server], interoperability
ms.assetid: 2738ce65-205e-4682-92d8-dc7e37c58b2b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c246912b7e12690427bc296d3db277481eddc42f
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/13/2018
ms.locfileid: "51606917"
---
# <a name="prereqs-migrating-log-shipping-to-always-on-availability-groups"></a>将日志传送迁移到 AlwaysOn 可用性组的先决条件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  本主题介绍将日志传送主数据库与其一个或多个辅助数据库一起转换为 AlwaysOn 主数据库和辅助数据库的先决条件。  
  
> [!NOTE]  
>  您可将可用性组中的任何主数据库或辅助数据库（可能可读）配置为日志传送主数据库。  
  
 **本主题内容：**  
  
-   [可用性组先决条件](#AGPrereqsRealAddress)  
  
-   [日志传送先决条件](#LogShipPrereqs)  
  
-   [相关任务](#RelatedTasks)  
  
-   [相关内容](#RelatedContent)  
  
##  <a name="AGPrereqsRealAddress"></a> 可用性组先决条件  
 若要允许备份作业在可用性组的主要副本上运行，请使用下列 AlwaysOn 可用性组备份设置：  
  
|“属性”|设置|  
|--------------|-------------|  
|可用性组的自动备份首选项|仅在主副本上|  
|主副本的备份优先级。|>0|  
  
 **详细信息：**  
  
 [查看可用性组属性 (SQL Server)](../../../database-engine/availability-groups/windows/view-availability-group-properties-sql-server.md)  
  
 [配置可用性副本备份 (SQL Server)](../../../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)  
  
##  <a name="LogShipPrereqs"></a> 日志传送先决条件  
  
-   日志传送主数据库必须驻留在承载可用性组的初始/当前主副本的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例上。  
  
-   为使某一给定的日志传送辅助数据库可转换为 AlwaysOn 辅助数据库，该数据库必须：  
  
    -   使用与主数据库相同的名称。  
  
    -   驻留在为可用性组承载辅助副本的服务器实例上。  
  
 在备份作业已在主数据库上运行后，禁用该备份作业；并且在还原作业已在给定辅助数据库上运行后，禁用还原作业。  
  
 在您为可用性组创建了所有辅助数据库后，如果您想要在辅助副本上执行备份，则需要重新配置该可用性组的自动备份首选项。  
  
 **详细信息：**  
  
 [将日志传送配置转换为可用性组](https://blogs.msdn.microsoft.com/sqlalwayson/2012/01/09/converting-a-logshipping-configuration-to-availability-group/) （SQL Server 博客）  
  
##  <a name="RelatedTasks"></a> 相关任务  
 **日志传送**  
  
-   [将日志传送升级至 SQL Server 2016 (Transact-SQL)](../../../database-engine/log-shipping/upgrading-log-shipping-to-sql-server-2016-transact-sql.md)  
  
-   [删除日志传送 (SQL Server)](../../../database-engine/log-shipping/remove-log-shipping-sql-server.md)  
  
 **Always On 可用性组**  
  
-   [使用可用性组向导 (SQL Server Management Studio)](../../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [使用“新建可用性组”对话框 (SQL Server Management Studio)](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [创建可用性组 (Transact-SQL)](../../../database-engine/availability-groups/windows/create-an-availability-group-transact-sql.md)  
  
-   [创建可用性组 (SQL Server PowerShell)](../../../database-engine/availability-groups/windows/create-an-availability-group-sql-server-powershell.md)  
  
-   [将辅助数据库联接到可用性组 (SQL Server)](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
-   [配置可用性副本备份 (SQL Server)](../../../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)  
  
##  <a name="RelatedContent"></a> 相关内容  
  
-   **博客：**  
  
     [将日志传送配置转换为可用性组](https://blogs.msdn.microsoft.com/sqlalwayson/2012/01/09/converting-a-logshipping-configuration-to-availability-group/)  
  
     [将日志传送主数据库和辅助数据库添加到现有可用性组](https://blogs.msdn.microsoft.com/sqlalwayson/2012/02/01/add-a-log-shipping-primary-database-and-secondary-databases-to-an-existing-availability-group/)  
  
     [SQL Server AlwaysOn 团队博客：SQL Server AlwayOn 团队官方博客](https://blogs.msdn.microsoft.com/sqlalwayson/)  
  
     [CSS SQL Server 工程师博客](https://blogs.msdn.com/b/psssql/)  
  
-   **白皮书：**  
  
     [迁移指南：从之前组合数据库镜像和日志传送的部署迁移到 AlwaysOn 可用性组](https://msdn.microsoft.com/library/jj635217)  
  
     [针对 SQL Server 2012 的 Microsoft 白皮书](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [SQL Server 客户咨询团队白皮书](https://sqlcat.com/)  
  
## <a name="see-also"></a>另请参阅  
 [关于日志传送 (SQL Server)](../../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [AlwaysOn 可用性组概述 (SQL Server)](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [监视可用性组 (SQL Server)](../../../database-engine/availability-groups/windows/monitoring-of-availability-groups-sql-server.md)  
  
  
