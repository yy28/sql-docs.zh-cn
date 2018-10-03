---
title: 远程 Blob 存储区 (RBS) 和 AlwaysOn 可用性组 (SQL Server) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 01a70258-d4fd-40bc-bc44-c490b5d6c420
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 16480ffcaf73a88f5983bef41b90f2276709d947
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48212057"
---
# <a name="remote-blob-store-rbs-and-alwayson-availability-groups-sql-server"></a>远程 Blob 存储区 (RBS) 和 AlwaysOn 可用性组 (SQL Server)
  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 可为 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][远程 Blob 存储区 (RBS)](../../../relational-databases/blob/remote-blob-store-rbs-sql-server.md) BLOB 对象 (Blob) 提供高可用性和灾难恢复解决方案。 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 通过将存储到可用性数据库中的所有 RBS 元数据和架构复制到辅助副本的方式来保护它们。 这是 SharePoint 内容数据库。 一般来说， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 不通过 Blob 单独存储此 RBS 元数据。  
  
 RBD BLOB 数据保护取决于 BLOB 存储位置，如下所示：  
  
|BLOB 存储位置|可用性组是否能够保护此 BLOB 数据？|  
|-------------------------|-----------------------------------------------------|  
|包含 RBS 元数据的同一数据库（使用 RBS 远程 FILESTREAM 提供程序存储）|用户帐户控制|  
|同一 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例中的另一个数据库（使用 RBS 远程 FILESTREAM 提供程序存储）|用户帐户控制<br /><br /> 建议您将此数据库放置在包含 RBS 元数据的数据库所在的同一可用性组中。|  
|不同 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例中的另一个数据库（使用 RBS 远程 FILESTREAM 提供程序存储）|用户帐户控制<br /><br /> 此数据库必须位于单独的可用性组中。|  
|第三方 BLOB 存储|否<br /><br /> 若要保护此 BLOB 数据，请使用 BLOB 存储提供程序的高可用性机制。|  
  
##  <a name="Limitations"></a> 限制  
  
-   RBS maintainer 需要将目标设定在主副本上。  
  
##  <a name="Recommendations"></a> 建议  
  
-   使用可用性组侦听器。 有关详细信息，请参阅 [可用性组侦听程序、客户端连接和应用程序故障转移 (SQL Server)](../../listeners-client-connectivity-application-failover.md)概念。  
  
##  <a name="RelatedContent"></a> 相关内容  
  
-   [维护远程 BLOB 存储](http://msdn.microsoft.com/library/gg316773\(SQL.105\).aspx) （位于 [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] 联机丛书）  
  
-   [运行 RBS Maintainer](http://blogs.msdn.com/b/sqlrbs/archive/2010/03/19/running-rbs-maintainer.aspx) （博客）  
  
-   [使用 FILESTREAM 提供程序配置 BLOB 存储 (RBS) (SharePoint 2010)](http://blogs.msdn.com/b/mvpawardprogram/archive/2012/04/02/configure-remote-blob-storage-rbs-with-the-filestream-provider-sharepoint-2010.aspx) （博客）  
  
## <a name="see-also"></a>请参阅  
 [AlwaysOn 客户端连接&#40;SQL Server&#41;](always-on-client-connectivity-sql-server.md)   
 [远程 Blob 存储区 (RBS) (SQL Server)](../../../relational-databases/blob/remote-blob-store-rbs-sql-server.md)  
  
  
