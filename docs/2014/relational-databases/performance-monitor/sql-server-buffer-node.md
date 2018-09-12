---
title: SQL Server:Buffer Node | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Buffer Node
- Buffer Node object
ms.assetid: fd3f9f0f-7c38-4cfd-a0c5-ee93dd52d9a5
caps.latest.revision: 19
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 89575a9d98d44c459d262f7ee23152a3efa0e2b7
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/06/2018
ms.locfileid: "43811713"
---
# <a name="sql-serverbuffer-node"></a>SQL Server:Buffer Node
  **Buffer Node** 对象提供了对 **Buffer Manager** 对象所提供的计数器进行补充的计数器。 通过它，您可以监视每个非一致性内存访问 (NUMA) 节点的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 缓冲池页分布。 对于正在使用的每个 NUMA 节点，都有一个 **Buffer Node** 对象实例。 在非 NUMA 体系结构上，将存在一个单独的 **Buffer Node** 对象实例。  
  
## <a name="buffer-node-performance-objects"></a>缓冲区节点性能对象  
 此表说明了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Buffer Node** 性能对象。  
  
|SQL Server Buffer Node 计数器|Description|  
|-------------------------------------|-----------------|  
|**Database pages**|指示此节点的缓冲池中包含数据库内容的页数。|  
|**Page life expectancy**|指示某页在没有引用的情况下，在此节点的缓冲池中停留的最小时间（秒）。|  
|**Local Node page lookups/sec**|指示从此节点发出并从此节点获得结果的查找请求数。|  
|**Remote Note page lookups/sec**|指示从此节点发出但从其他节点获得结果的查找请求数。|  
  
 如果 SQL Server 在非 NUMA 硬件上运行，则 **Buffer Node** 和 **Buffer Manager** 对象的计数器应该匹配。  
  
 在 NUMA 硬件上，所有 **Buffer Node** 的相应计数器的总和应该与所有 **Buffer Manager**的相应计数器的总和匹配。  
  
> [!NOTE]  
>  由于计数器具有动态性以及抽样准确性有所偏差，计数器的值与总和可能不会精确匹配。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server Buffer Manager 对象](sql-server-buffer-manager-object.md)   
 [“服务器内存”服务器配置选项](../../database-engine/configure-windows/server-memory-server-configuration-options.md)   
 [监视资源使用情况（系统监视器）](monitor-resource-usage-system-monitor.md)   
 [sys.dm_os_performance_counters (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql)  
  
  
