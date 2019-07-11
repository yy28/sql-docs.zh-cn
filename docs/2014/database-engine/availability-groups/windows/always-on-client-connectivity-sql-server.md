---
title: AlwaysOn 客户端连接 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], listeners
- Availability Groups [SQL Server], prerequisites and restrictions
- Availability Groups [SQL Server], client connectivity
ms.assetid: b456448d-1757-48c8-8bbb-2d1c2d6d61e9
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d8a1b81d60ef691e02d4b69cc71fa961bbaddf18
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67793432"
---
# <a name="always-on-client-connectivity-sql-server"></a>AlwaysOn 客户端连接 (SQL Server)
  本主题介绍与 AlwaysOn 可用性组进行客户端连接时的注意事项，包括针对客户端配置和设置的先决条件、限制和建议。  
  
 
  
##  <a name="ClientConnSupport"></a> 客户端连接支持  
 以下部分提供有关对客户端连接的 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 支持的信息。  
  
 **驱动程序支持**  
  
 下表概述了 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]的驱动程序支持：  
  
|驱动程序|多子网故障转移|应用程序意向|只读路由|多子网故障转移：更快的单子网终结点故障转移|多子网故障转移：SQL 群集实例的命名实例解析|  
|------------|----------------------------|------------------------|------------------------|--------------------------------------------------------------------|-----------------------------------------------------------------------------------|  
|SQL Native Client 11.0 ODBC|是|是|是|是|是|  
|SQL Native Client 11.0 OLEDB|否|是|是|否|否|  
|ADO.NET 与.NET Framework 4.0 和连接性修补程序 **<sup>*</sup>** |是|是|是|是|是|  
|ADO.NET 与.NET Framework 3.5 SP1 和连接性修补程序 **<sup>** </sup>** |是|是|是|是|是|  
|Microsoft JDBC driver 4.0 for SQL Server|是|是|是|是|是|  
  
 **<sup>*</sup>**  下载.NET Framework 4.0 的 ADO.NET 连接性修补程序： [ https://support.microsoft.com/kb/2600211 ](https://support.microsoft.com/kb/2600211)。  
  
 **<sup>** </sup>* * 下载连接性修补程序适用于使用.NET Framework 3.5 SP1: [ https://support.microsoft.com/kb/2654347 ](https://support.microsoft.com/kb/2654347)。  
  
> [!IMPORTANT]  
>  要连接到一个可用性组侦听器，客户端必须使用 TCP 连接字符串。  
  
##  <a name="RelatedTasks"></a> 相关任务  
  
-   [创建和配置可用性组 (SQL Server)](creation-and-configuration-of-availability-groups-sql-server.md)  
  
-   [创建或配置可用性组侦听程序 (SQL Server)](create-or-configure-an-availability-group-listener-sql-server.md)  
  

  
## <a name="see-also"></a>请参阅  
 [AlwaysOn 可用性组概述&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [故障转移群集和 AlwaysOn 可用性组&#40;SQL Server&#41;](failover-clustering-and-always-on-availability-groups-sql-server.md)   
 [先决条件、 限制和建议为 AlwaysOn 可用性组&#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)   
 [可用性组侦听程序、客户端连接和应用程序故障转移 &#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md)   
 [关于对可用性副本的客户端连接访问 &#40;SQL Server&#41;](about-client-connection-access-to-availability-replicas-sql-server.md)   
 [Microsoft SQL Server AlwaysOn 解决方案指南有关高可用性和灾难恢复](https://go.microsoft.com/fwlink/?LinkId=227600)   
 [SQL Server AlwaysOn 团队博客：SQL Server AlwaysOn 团队官方博客](https://blogs.msdn.com/b/sqlalwayson/)   
 [从运行 Windows Server 2003、Windows Vista、Windows Server 2008、Windows 7 或 Windows Server 2008 R2 的计算机重新建立 IPSec 连接时出现长时间延迟](https://support.microsoft.com/kb/980915)   
 [群集服务需要大约 30 秒对 Windows Server 2008 R2 中的 IPv6 IP 地址进行故障转移](https://support.microsoft.com/kb/2578113)   
 [如果群集与应用程序服务器之间不存在路由器，则故障转移操作的速度会很慢](https://support.microsoft.com/kb/2582281)  
  
  
