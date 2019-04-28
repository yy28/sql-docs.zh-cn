---
title: Always On 可用性组 (SQL Server) 的服务器实例的配置 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], server instance
- Availability Groups [SQL Server], about
ms.assetid: fad8db32-593e-49d5-989c-39eb8399c416
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d8c9aa465237010ff48881a2df176de6d067da0c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62815274"
---
# <a name="configuration-of-a-server-instance-for-always-on-availability-groups-sql-server"></a>为 AlwaysOn 可用性组配置服务器实例 (SQL Server)
  本主题包含的信息涉及配置 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例以在 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 中提供支持[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]的要求。  
  
> [!IMPORTANT]  
>  有关针对 Windows Server 故障转移群集 (WSFC) 节点的 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 先决条件和限制以及 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的实例的基本信息，请参阅[针对 AlwaysOn 可用性组的先决条件、限制和建议 (SQL Server)](prereqs-restrictions-recommendations-always-on-availability.md)。  
  
 
  
##  <a name="TermsAndDefinitions"></a> 术语和定义  
  
 提供替代数据库镜像的企业级方案的高可用性和灾难恢复解决方案。 “可用性组”  针对一组离散的用户数据库（称为“可用性数据库” ，它们共同实现故障转移）支持故障转移环境。  
  
 可用性副本  
 可用性组的实例化，该可用性组由特定的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例承载，该实例维护属于该可用性组的每个可用性数据库的本地副本。  存在两种类型的可用性副本：一个“主副本” 和一至四个“辅助副本”。 承载给定可用性组的可用性副本的服务器实例必须位于单个 Windows Server 故障转移群集 (WSFC) 群集的不同节点上。  
  
 [数据库镜像端点](../../database-mirroring/the-database-mirroring-endpoint-sql-server.md)  
 端点就是一个 SQL Server 对象，它支持 SQL Server 在网络中通信。 若要参与数据库镜像和/或 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] ，服务器实例需要一个特殊的专用端点。 服务器实例上所有的镜像和可用性组连接都使用相同的数据库镜像端点。 此端点用途特殊，专门用于接收来自其他服务器实例的这些连接。  
  
##  <a name="ConfigSI"></a> 若要配置的服务器实例以支持 AlwaysOn 可用性组  
 要支持 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]，服务器实例必须位于承载可用性组的 WSFC 故障转移群集的某个节点上，启用 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 并且占有一个数据库镜像端点。  
  
1.  在要参与一个或多个可用性组的每个服务器实例上都启用 AlwaysOn 可用性组功能。 一个给定服务器实例只能为一个给定可用性组承载单个可用性副本。  
  
2.  确保服务器实例拥有数据库镜像端点。  
  
##  <a name="RelatedTasks"></a> 相关任务  
 **若要启用 AlwaysOn 可用性组**  
  
-   [启用和禁用 AlwaysOn 可用性组 (SQL Server)](enable-and-disable-always-on-availability-groups-sql-server.md)  
  
 **确定数据库镜像端点是否存在**  
  
-   [sys.database_mirroring_endpoints (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql)  
  
 **创建数据库镜像端点**  
  
-   [创建数据库镜像端点的 AlwaysOn 可用性组&#40;SQL Server PowerShell&#41;](database-mirroring-always-on-availability-groups-powershell.md)  
  
-   [为 Windows 身份验证创建数据库镜像终结点 (Transact-SQL)](../../database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
-   [允许数据库镜像终结点使用证书进行出站连接 (Transact-SQL)](../../database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md)  
  
##  <a name="RelatedContent"></a> 相关内容  
  
-   **博客：**  
  
     [AlwaysON-HADRON 学习系列：启用了 HADRON 的数据库的工作线程池用法](https://blogs.msdn.com/b/psssql/archive/2012/05/17/alwayson-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases.aspx)  
  
     [SQL Server AlwaysOn 团队博客：SQL Server AlwaysOn 团队官方博客](https://blogs.msdn.com/b/sqlalwayson/)  
  
     [CSS SQL Server 工程师博客](https://blogs.msdn.com/b/psssql/)  
  
-   **视频：**  
  
     [Microsoft SQL Server Code-Named"Denali"AlwaysOn 系列，第 1 部分：Introducing the Next Generation High Availability Solution](http://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI302)（Microsoft SQL Server Code-Named "Denali" Always On 系列，第 1 部分：介绍下一代高可用性解决方案）  
  
     [Microsoft SQL Server Code-Named"Denali"AlwaysOn 系列，第 2 部分：构建使用 AlwaysOn 的关键任务高可用性解决方案](http://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI404)  
  
-   **白皮书：**  
  
     [Microsoft SQL Server AlwaysOn 解决方案指南有关高可用性和灾难恢复](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
     [针对 SQL Server 2012 的 Microsoft 白皮书](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [SQL Server 客户咨询团队白皮书](http://sqlcat.com/)  
  
## <a name="see-also"></a>请参阅  
 [AlwaysOn 可用性组概述&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [先决条件、 限制和建议为 AlwaysOn 可用性组&#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)   
 [数据库镜像终结点 (SQL Server)](../../database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [AlwaysOn 可用性组：互操作性 (SQL Server)](always-on-availability-groups-interoperability-sql-server.md)   
 [故障转移群集和 AlwaysOn 可用性组&#40;SQL Server&#41;](failover-clustering-and-always-on-availability-groups-sql-server.md)   
 [Windows Server 故障转移群集 (WSFC) 与 SQL Server](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)   
 [AlwaysOn 故障转移群集实例](../../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)  
  
  
