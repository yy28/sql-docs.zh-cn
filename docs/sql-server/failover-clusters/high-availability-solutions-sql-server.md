---
title: "高可用性解决方案 (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 05/19/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- high availability [SQL Server], solutions
- Database Engine [SQL Server], availability
- database availability [SQL Server]
- availability [SQL Server]
- server availability [SQL Server]
ms.assetid: b2eda634-0f8e-4703-801b-7ba895544ff5
caps.latest.revision: 84
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: dd78349c495ceb9b653ae3b44915da327c489152
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="high-availability-solutions-sql-server"></a>高可用性解决方案 (SQL Server)
  本主题介绍了几个提高服务器或数据库可用性的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 高可用性解决方案。 高可用性解决方案可减少硬件或软件故障造成的影响，保持应用程序的可用性，从而将用户可以察觉到的停机时间减至最少。    
    
   
>  **注意！** 想要知道哪个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本支持给定的高可用性解决方案？ 请参阅 [SQL Server 2016 各个版本支持的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)中的“高可用性 (AlwaysOn)”部分。    
     
    
##  <a name="TermsAndDefinitions"></a> SQL Server 高可用性解决方案概述    
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供了几个为服务器或数据库打造高可用性的可选方案。 高可用性可选方案包括：    
    
*  AlwaysOn 故障转移群集实例    
 作为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] AlwaysOn 产品/服务的一部分，AlwaysOn 故障转移群集实例利用 Windows Server 故障转移群集 (WSFC) 功能通过冗余在实例级别（ *故障转移群集实例* (FCI)）提供了本地高可用性。 FCI 是在 Windows Server 故障转移群集 (WSFC) 节点上和（可能）多个子网中安装的单个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。 在网络中，FCI 显示为在单台计算机上运行的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例，不过它提供了从一个 WSFC 节点到另一个 WSFC 节点的故障转移（如果当前节点不可用）。    
    
 有关详细信息，请参阅 [AlwaysOn 故障转移群集实例 (SQL Server)](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)实例的故障转移群集实例。    
    
*  [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]    
 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 是 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 中引入的企业级高可用性和灾难恢复解决方案，可使一个或多个用户数据库的可用性达到最高。 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 要求 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例驻留在 Windows Server 故障转移群集 (WSFC) 节点上。 有关详细信息，请参阅 [AlwaysOn 可用性组 (SQL Server)](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)。    
    
  
>  **注意！** FCI 可利用 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 提供数据库级别的远程灾难恢复。 有关详细信息，请参阅[故障转移群集和 AlwaysOn 可用性组 (SQL Server)](../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md)。    
    
*  数据库镜像。 **注意！** [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 建议改用 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 。     
数据库镜像是一种解决方案，可提供几乎是瞬时的故障转移，以提高数据库的可用性。 数据库镜像可以用来维护相应生产数据库（称为“主体数据库 ”）的单个备用数据库（或“镜像数据库 ”）。 有关详细信息，请参阅[数据库镜像 (SQL Server)](../../database-engine/database-mirroring/database-mirroring-sql-server.md)。    
    
*  日志传送    
 与 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 和数据库镜像一样，日志传送是数据库级操作。 可以使用日志传送来维护单个生产数据库（称为*主数据库*）的一个或多个温备用数据库（称为*辅助数据库*）。 有关日志传送的详细信息，请参阅[关于日志传送 (SQL Server)](../../database-engine/log-shipping/about-log-shipping-sql-server.md)。    
    
##  <a name="RecommendedSolutions"></a> 有关使用 SQL Server 保护数据的建议的解决方案    
 为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 环境提供数据保护的建议：    
    
-   对于通过第三方共享磁盘解决方案 (SAN) 进行的数据保护，建议你使用 AlwaysOn 故障转移群集实例。    
    
-   对于通过 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]进行的数据保护，建议您使用 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]。    
    
       >  如果你运行的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本不支持 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]，建议你使用日志传送。 有关哪些版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]的信息，请参阅 [SQL Server 2016 各个版本支持的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)中的“高可用性 (AlwaysOn)”部分。    
    
## <a name="see-also"></a>另请参阅    
 [Windows Server 故障转移群集 (WSFC) 与 SQL Server](../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)     
 [数据库镜像：互操作性和共存 (SQL Server)](../../database-engine/database-mirroring/database-mirroring-interoperability-and-coexistence-sql-server.md)     
 [SQL Server 2016 中不推荐使用的数据库引擎功能](../../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)    
    
  


