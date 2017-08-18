---
title: "远程 Blob 存储区 (RBS) 和 AlwaysOn 可用性组 (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 01a70258-d4fd-40bc-bc44-c490b5d6c420
caps.latest.revision: 15
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: e6b39d1e5bda9e7426b92611df9f0ac0dfa3a495
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="remote-blob-store-rbs-and-always-on-availability-groups-sql-server"></a>远程 Blob 存储区 (RBS) 和 AlwaysOn 可用性组 (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 可为 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][远程 Blob 存储区 (RBS)](../../../relational-databases/blob/remote-blob-store-rbs-sql-server.md) BLOB 对象 (Blob) 提供高可用性和灾难恢复解决方案。 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 通过将存储到可用性数据库中的所有 RBS 元数据和架构复制到辅助副本的方式来保护它们。 这是 SharePoint 内容数据库。 一般来说， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 不通过 Blob 单独存储此 RBS 元数据。  
  
 RBS BLOB 数据保护取决于 BLOB 存储位置，如下所示：  
  
|BLOB 存储位置|可用性组是否能够保护此 BLOB 数据？|  
|-------------------------|-----------------------------------------------------|  
|包含 RBS 元数据的同一数据库（使用 RBS 远程 FILESTREAM 提供程序存储）|是|  
|同一 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例中的另一个数据库（使用 RBS 远程 FILESTREAM 提供程序存储）|是<br /><br /> 建议您将此数据库放置在包含 RBS 元数据的数据库所在的同一可用性组中。|  
|不同 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例中的另一个数据库（使用 RBS 远程 FILESTREAM 提供程序存储）|是<br /><br /> 此数据库必须位于单独的可用性组中。|  
|第三方 BLOB 存储|是<br /><br /> 若要保护此 BLOB 数据，请使用 BLOB 存储提供程序的高可用性机制。|  
  
##  <a name="Limitations"></a> 限制  
  
-   RBS maintainer 需要将目标设定在主副本上。  
  
##  <a name="Recommendations"></a> 建议  
  
-   使用可用性组侦听器。 有关详细信息，请参阅 [可用性组侦听程序、客户端连接和应用程序故障转移 (SQL Server)](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)概念。  
  
##  <a name="RelatedContent"></a> 相关内容  
  
-   [维护远程 BLOB 存储](http://msdn.microsoft.com/library/gg316773\(SQL.105\).aspx) （位于 [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] 联机丛书）  
  
-   [运行 RBS Maintainer](http://blogs.msdn.com/b/sqlrbs/archive/2010/03/19/running-rbs-maintainer.aspx) （博客）  
  
-   [使用 FILESTREAM 提供程序配置 BLOB 存储 (RBS) (SharePoint 2010)](http://blogs.msdn.com/b/mvpawardprogram/archive/2012/04/02/configure-remote-blob-storage-rbs-with-the-filestream-provider-sharepoint-2010.aspx) （博客）  
  
## <a name="see-also"></a>另请参阅  
 [AlwaysOn 客户端连接 (SQL Server)](../../../database-engine/availability-groups/windows/always-on-client-connectivity-sql-server.md)   
 [远程 Blob 存储区 (RBS) (SQL Server)](../../../relational-databases/blob/remote-blob-store-rbs-sql-server.md)  
  
  

