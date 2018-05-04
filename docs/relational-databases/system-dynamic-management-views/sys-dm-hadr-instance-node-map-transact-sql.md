---
title: sys.dm_hadr_instance_node_map (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.sys.dm_hadr_instance_node_map_TSQL
- sys.sys.dm_hadr_instance_node_map
- sys.dm_hadr_instance_node_map_TSQL
- sys.dm_hadr_instance_node_map
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], WSFC clusters
- sys.sys.dm_hadr_instance_node_map dynamic management view
ms.assetid: ccfaf62c-9f87-43cf-a5e7-8942e91dd041
caps.latest.revision: 9
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e12291f81708378120b45b474b0959976918471e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmhadrinstancenodemap-transact-sql"></a>sys.dm_hadr_instance_node_map (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  对于每个实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]承载的可用性副本上加入其 Alwayson 可用性组，则返回承载该服务器实例的 Windows Server 故障转移群集 (WSFC) 节点的名称。 此动态管理视图具有以下用法：  
  
-   此动态管理视图对于检测包含承载于同一 WSFC 节点上的多个可用性副本的可用性组很有用，这是一个不受支持的配置，如果可用性组的配置不正确，则在进行 FCI 故障转移后可能出现此配置。 有关详细信息，请参阅[故障转移群集和 AlwaysOn 可用性组 (SQL Server)](../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md)。  
  
-   当多个 SQL Server 实例承载于同一 WSFC 节点上时，资源 DLL 将使用此动态管理视图来确定要连接到的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。  
   
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**ag_resource_id**|**nvarchar(256)**|作为 WSFC 群集中资源的可用性组的唯一 ID。|  
|**instance_name**|**nvarchar(256)**|名称-*服务器*/*实例*-承载的副本的可用性组的服务器实例。|  
|**node_name**|**nvarchar(256)**|WSFC 群集节点的名称。|  
  
## <a name="permissions"></a>权限  
 要求具有服务器的 VIEW SERVER STATE 权限。  
  
## <a name="see-also"></a>另请参阅  
 [AlwaysOn 可用性组动态管理视图和函数 (Transact-SQL)](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)   
 [AlwaysOn 可用性组目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [监视可用性组 & #40;Transact SQL & #41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [AlwaysOn 可用性组 (SQL Server)](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
  
  
