---
title: sys. dm_hadr_availability_replica_cluster_nodes （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_hadr_availability_replica_cluster_nodes
- sys.dm_hadr_availability_replica_cluster_nodes_TSQL
- dm_hadr_availability_replica_cluster_nodes_TSQL
- sys.dm_hadr_availability_replica_cluster_nodes
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], WSFC clusters
- sys.dm_hadr_availability_replica_cluster_nodes dynamic management view
ms.assetid: dbd7e416-badd-4332-a45c-438aa0145a99
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a5e33207fd6fd14fe4fe2f8bcc732b2f762f3723
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "67900630"
---
# <a name="sysdm_hadr_availability_replica_cluster_nodes-transact-sql"></a>sys.dm_hadr_availability_replica_cluster_nodes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  为 Windows Server 故障转移群集 (WSFC) 群集中 AlwaysOn 可用性组的每个可用性副本（不论联接状态如何）都返回一行。  

 ##  <a name="connected_state"></a>  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|group_name****|**nvarchar(256)**|可用性组的名称。|  
|**replica_server_name**|**nvarchar(256)**|承载副本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的名称。|  
|**node_name**|**nvarchar(256)**|群集节点的名称。|  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>权限  
 要求具有服务器的 VIEW SERVER STATE 权限。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;Transact-sql 监视可用性组&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [AlwaysOn 可用性组概述 (SQL Server)](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  
