---
title: AlwaysOn 可用性组：互操作性 (SQL Server) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], about
- Availability Groups [SQL Server], interoperability
ms.assetid: daf87f90-2623-42ca-912c-b8f07d210510
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3f6123f66d687327ba56601419328e44fd920a2a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62815743"
---
# <a name="always-on-availability-groups-interoperability-sql-server"></a>AlwaysOn 可用性组：互操作性 (SQL Server)
  本主题说明 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中其他 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]功能的互操作性。  
  

  
##  <a name="Interop"></a> 与 AlwaysOn 可用性组互操作的功能  
 下表列出了在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中可与 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 互操作的 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]功能。  “详细信息”列中的链接表示给定功能的互操作性注意事项。  
  
|功能|详细信息|  
|-------------|----------------------|  
|变更数据捕获|[复制、 更改跟踪、 更改数据捕获和 AlwaysOn 可用性组&#40;SQL Server&#41;](replicate-track-change-data-capture-always-on-availability.md)|  
|更改跟踪|[复制、 更改跟踪、 更改数据捕获和 AlwaysOn 可用性组&#40;SQL Server&#41;](replicate-track-change-data-capture-always-on-availability.md)|  
|包含的数据库|[包含的数据库与 AlwaysOn 可用性组 (SQL Server)](always-on-availability-groups-sql-server.md)|  
|数据库加密|[加密的数据库与 AlwaysOn 可用性组&#40;SQL Server&#41;](encrypted-databases-with-always-on-availability-groups-sql-server.md)|  
|数据库快照|[数据库快照与 AlwaysOn 可用性组&#40;SQL Server&#41;](database-snapshots-with-always-on-availability-groups-sql-server.md)|  
|FILESTREAM 和 FileTable|[FILESTREAM 和 FileTable 与 AlwaysOn 可用性组&#40;SQL Server&#41;](filestream-and-filetable-with-always-on-availability-groups-sql-server.md)|  
|全文搜索|注意：全文索引与 AlwaysOn 辅助数据库同步。|  
|日志传送|[从迁移的先决条件日志传送到 AlwaysOn 可用性组&#40;SQL Server&#41;](prereqs-migrating-log-shipping-to-always-on-availability-groups.md)|  
|远程 Blob 存储区 (RBS)|[远程 Blob 存储区&#40;RBS&#41;和 AlwaysOn 可用性组&#40;SQL Server&#41;](remote-blob-store-rbs-and-always-on-availability-groups-sql-server.md)|  
|复制[为 AlwaysOn 可用性组 (SQL Server) 配置复制](configure-replication-for-always-on-availability-groups-sql-server.md)<br /><br /> [维护 AlwaysOn 发布数据库&#40;SQL Server&#41;](maintaining-an-always-on-publication-database-sql-server.md)<br /><br /> [复制、 更改跟踪、 更改数据捕获和 AlwaysOn 可用性组&#40;SQL Server&#41;](replicate-track-change-data-capture-always-on-availability.md)<br /><br /> [复制订阅服务器和 AlwaysOn 可用性组&#40;SQL Server&#41;](replication-subscribers-and-always-on-availability-groups-sql-server.md)|  
|Analysis Services|[Analysis Services 与 AlwaysOn 可用性组](analysis-services-with-always-on-availability-groups.md)|  
|Reporting Services|使用只读辅助副本作为报告数据源，减少您的读写主副本上的负载。<br /><br /> [Reporting Services 与 AlwaysOn 可用性组&#40;SQL Server&#41;](reporting-services-with-always-on-availability-groups-sql-server.md)|  
|Service Broker|[Service Broker 与 AlwaysOn 可用性组&#40;SQL Server&#41;](service-broker-with-always-on-availability-groups-sql-server.md)|  
|SQL Server 代理||  
  
##  <a name="NoInterop"></a> 不能与 AlwaysOn 可用性组互操作的功能  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 不能与以下功能互操作：  
  
-   跨数据库事务/分布式事务  
  
     有关不支持此类事务原因的信息，请参阅[数据库镜像或 AlwaysOn 可用性组 (SQL Server) 不支持跨数据库事务](transactions-always-on-availability-and-database-mirroring.md)。  
  
-   数据库镜像  
  
##  <a name="RelatedContent"></a> 相关内容  
  
-   **博客：**  
  
     [迁移指南：迁移到 SQL Server 2012 故障转移群集和可用性组从之前群集和镜像部署](https://blogs.msdn.com/b/sqlalwayson/archive/2012/04/09/now-available-migration-guide-migrating-to-sql-server-2012-failover-clustering-and-availability-groups-from-prior-clustering-and-mirroring-deployments.aspx)  
  
     [SQL Server AlwaysOn 团队博客：SQL Server AlwaysOn 团队官方博客](https://blogs.msdn.com/b/sqlalwayson/)  
  
     [CSS SQL Server 工程师博客](https://blogs.msdn.com/b/psssql/)  
  
-   **白皮书：**  
  
     [迁移指南：迁移到 AlwaysOn 可用性组从之前组合数据库镜像和部署日志传送](https://msdn.microsoft.com/library/jj635217)  
  
     [Microsoft SQL Server AlwaysOn 解决方案指南有关高可用性和灾难恢复](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
     [针对 SQL Server 2012 的 Microsoft 白皮书](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [SQL Server 客户咨询团队白皮书](http://sqlcat.com/)  
  
## <a name="see-also"></a>请参阅  
 [AlwaysOn 可用性组概述&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [先决条件、 限制和建议为 AlwaysOn 可用性组&#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)  
  
  
