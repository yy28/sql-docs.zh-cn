---
title: "读取缩放可用性组 | Microsoft Docs"
ms.custom: 
ms.date: 10/24/2017
ms.prod:
- sql-server-2016
- sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 
caps.latest.revision: "9"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7c607ab320a7deb80fb140ee9f4cc25b798b7fc4
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="read-scale-availability-groups"></a>读取缩放可用性组
[!INCLUDE[tsql-appliesto-ssvnxt-xxxx-xxxx-xxx](../../../includes/tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md)]

可用性组不仅集合了 SQL Server 的最佳 HA 功能，它还是提供了集成缩放解决方案的综合性解决方案。 在典型数据库应用程序中，通常会有多个运行不同类型工作负荷的客户端，由于资源限制，这种情况有时会产生瓶颈。 可以释放资源并增加 OLTP 工作负荷的吞吐量，还可以提高性能并缩放只读工作负荷。 利用 SQL Server 的最快复制技术即可实现上述目的 - 创建一组复制数据库，减轻对只读副本的报告和分析工作负荷。 

利用可用性组，可将一个或多个次要副本配置为支持以只读方式访问辅助数据库。

运行分析或报告工作负荷的客户端应用程序可直接连接到辅助数据库。 或者，客户可以设置只读路由列表并连接到主要副本，主要副本将连接请求循环转发到路由列表中的每个次要副本。

## <a name="read-scale-availability-groups-without-cluster"></a>不需要群集的读取缩放可用性组

在 [!INCLUDE[sssql15-md](..\..\..\includes\sssql15-md.md)] 及以前的版本中，所有可用性组都需要群集。 群集用于提供业务连续性，即高可用性和灾难恢复 (HADR)。 此外，不能将次要副本配置为执行读取操作。 如果不以 HA 为目标，配置和运行群集意味着会产生大量运行开销。 SQL Server 2017 引入了不需要群集的读取缩放可用性组。 

如果业务要求是转换主要副本上运行的任务关键型工作负荷的资源，用户现在则可以使用只读路由或直接连接到可读次要副本，而无需依赖于与任何群集技术进行集成。 Windows 和 Linux 平台上的 SQL Server 2017 支持这些新功能。

>[!IMPORTANT]
>这不是高可用性安装程序。 不需要监视基础结构、协调故障检测和进行自动故障转移。 如果不具有群集，SQL Server 无法提供自动化 HA 解决方案可提供的低恢复时间目标 (RTO)。 需要 HA 功能的用户可使用群集管理器（Windows 上的 WSFC 或 Linux 上的 Pacemaker）。 
>
>读取缩放可用性组可提供灾难恢复功能。 当只读副本处于同步提交模式时，它们将提供零个恢复点目标 (RPO)。 若要对读取缩放可用性组进行故障转移，请参阅[对读取缩放可用性组上的主要副本进行故障转移](perform-a-planned-manual-failover-of-an-availability-group-sql-server.md#ReadScaleOutOnly)

## <a name="use-distributed-availability-groups-for-geographic-read-scale"></a>使用分布式可用性组进行地理读取缩放

不同地理位置的解决方案可以使用分布式可用性组实现读取缩放解决方案。 这能减轻主要副本、可读次要副本以及靠近读取工作负荷源的站点的读取工作负荷。 如此一来，不仅能减少主要副本中的资源用量，还能通过减少网络延迟和利用专用资源对读取吞吐量产生积极影响。

单个分布式可用性组最多可具有 17 个可读次要副本。 增加的缩放功能表现为：菊花链使可用性组的数量成倍增加，同时进一步增加了可读副本的数量。 还可以在同一可用性组中部署两个分布式可用性组，以在地理位置不同的环境中实现低延迟读取。




## <a name="next-steps"></a>后续步骤 

[在 Linux 上配置读取缩放可用性组](../../../linux/sql-server-linux-availability-group-configure-rs.md)

## <a name="see-also"></a>另请参阅  
 [AlwaysOn 可用性组概述 (SQL Server)](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  
