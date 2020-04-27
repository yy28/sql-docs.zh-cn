---
title: 配置数据库引擎实例 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 84e36fcb-2c78-48e8-8e4b-bf784a3ee557
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 578b870128486285a7c31bf9a860b85d170f8771
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62786600"
---
# <a name="configure-database-engine-instances-sql-server"></a>配置数据库引擎实例 (SQL Server)
  [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的每个实例都必须经过配置，以符合为该实例所承载的数据库所定义的性能和可用性要求。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 包括一些配置选项，这些选项控制资源使用情况等行为和诸如审核或触发器递归等功能的可用性。  
  
## <a name="instance-configuration"></a>Instance Configuration  
 将一个数据库部署到生产中时，通常使用一个服务级别协议 (SLA) 来定义一些方面，比如需要的数据库性能级别和数据库可用性级别。 SLA 的条款通常会促进实例的配置要求的形成。  
  
 实例通常在安装后即进行配置。 初始配置通常由计划部署到实例的数据库类型的 SLA 要求确定。 完成部署数据库后，数据库管理员将监视实例性能，如果性能指标表明实例未达到 SLA 要求，则根据需要调整配置设置。  
  
## <a name="configuration-tasks"></a>配置任务  
  
|任务说明|主题|  
|----------------------|-----------|  
|说明各种实例配置选项以及如何查看或更改这些选项。|[服务器配置选项 (SQL Server)](server-configuration-options-sql-server.md)|  
|说明如何查看和配置实例中新的数据文件和日志文件的默认位置。|[查看或更改数据文件和日志文件的默认位置 (SQL Server Management Studio)](view-or-change-the-default-locations-for-data-and-log-files.md)|  
|说明如何将 SQL Server 配置为使用软件 NUMA。|[将 SQL Server 配置为使用软件 NUMA &#40;SQL Server&#41;](soft-numa-sql-server.md)|  
|说明如何将 TCP/IP 端口映射到非一致性内存访问 (NUMA) 节点关联。|[将 TCP IP 端口映射到 NUMA 节点 (SQL Server)](map-tcp-ip-ports-to-numa-nodes-sql-server.md)|  
|说明如何启用 Windows“锁定内存页”策略。 此策略将确定哪些帐户可以使用进程将数据保留在物理内存中，从而阻止系统将数据分页到磁盘的虚拟内存中。|[启用“锁定内存页”选项 (Windows)](enable-the-lock-pages-in-memory-option-windows.md)|  
  
## <a name="see-also"></a>另请参阅  
 [数据库引擎实例 (SQL Server)](database-engine-instances-sql-server.md)  
  
  
