---
title: "基本可用性组（AlwaysOn 可用性组）| Microsoft Docs"
ms.custom: 
ms.date: 09/27/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: availability-groups
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 285adbc7-ac9b-40f6-b4a9-3f1591d3b632
caps.latest.revision: "9"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 15696e7bf14fb5a240f1ef14070f28bb5d87a1f2
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/18/2018
---
# <a name="basic-availability-groups-always-on-availability-groups"></a>基本可用性组（AlwaysOn 可用性组）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  AlwaysOn Basic 可用性组为 SQL Server 2016 和 SQL Server 2017 Standard Edition 提供高可用性解决方案。 基本可用性组支持单个数据库的故障转移环境。 它的创建和管理与传统（高级）的 [AlwaysOn 可用性组 (SQL Server)](../../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md) 的 Enterprise Edition 非常类似。 本文档概述了基本可用性组的差异和限制。  
  
## <a name="features"></a>功能  
 AlwaysOn 基本可用性组取代已弃用的数据库镜像功能，并提供类似级别的功能支持。 基本可用性组使主数据库可以维护单一的副本。 此副本可以使用同步提交模式或异步提交模式。 有关可用性模式的详细信息，请参阅[可用性模式（AlwaysOn 可用性组）](../../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md)。 次要副本将保持非活动状态，除非需要进行故障转移。 此故障转移会反转主要和次要角色分配，导致次要副本成为活动的主数据库。 有关故障转移的详细信息，请参阅[故障转移和故障转移模式（AlwaysOn 可用性组）](../../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md)。 基本可用性组可以在跨本地和 Microsoft Azure 的混合环境中运行。  
  
## <a name="limitations"></a>限制  
 相比 SQL Server 2016 Enterprise Edition 上的高级可用性组，基本可用性组仅使用一部分功能。 基本可用性组包括以下限制：  
  
- 两个副本（主要和次要）的限制。  
  
- 对次要副本没有读取访问权限。  
  
- 在次要副本上没有备份。  

- 在次要副本上没有完整性检查。 

- 不支持在运行 SQL Server 2016 社区技术预览版 3 (CTP3) 之前的 SQL Server 版本的服务器上托管的副本。  
  
- 不支持在现有基本可用性组中添加或删除副本。  
  
- 支持一个可用性数据库。  
  
- 基本可用性组不能升级到高级可用性组。 必须删除该组并重新添加到包含仅运行 SQL Server 2016 Enterprise Edition 的服务器的组中。  
  
- 仅 Standard Edition 服务器支持基本可用性组。 

- 基本可用性组不能为分布式可用性组的一部分。 
  
## <a name="configuration"></a>配置  
 可以在任意两个 SQL Server 2016 Standard Edition 服务器上创建 AlwaysOn 基本可用性组。 当创建基本可用性组时，必须在创建期间指定两个副本。  
  
 若要创建基本可用性组，请使用 **CREATE AVAILABILITY GROUP** transact-SQL 命令并指定“WITH BASIC”选项（默认值为“ADVANCED”）。 有关详细信息，请参阅 [CREATE AVAILABILITY GROUP (Transact-SQL)](../../../t-sql/statements/create-availability-group-transact-sql.md)。 目前对于在 SQL Server Management Studio 中创建基本可用性组不提供 UI 支持。  
  
> [!NOTE]  
>  在指定“WITH BASIC”  时，基本可用性组的限制适用于 **CREATE AVAILABILITY GROUP** 命令。 例如，如果你尝试创建一个允许读取访问权限的基本可用性组，将收到错误。 其他限制同样适用。 有关详细信息，请参阅本主题的“限制”部分。  
  
## <a name="see-also"></a>另请参阅  
 [AlwaysOn 可用性组概述 (SQL Server)](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  
