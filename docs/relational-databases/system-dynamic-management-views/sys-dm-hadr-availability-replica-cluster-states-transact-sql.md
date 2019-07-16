---
title: sys.dm_hadr_availability_replica_cluster_states (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_hadr_availability_replica_cluster_states_TSQL
- dm_hadr_availability_replica_cluster_states
- sys.dm_hadr_availability_replica_cluster_states
- dm_hadr_availability_replica_cluster_states_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], WSFC clusters
- sys.dm_hadr_availability_replica_cluster_states dynamic management view
ms.assetid: 2e0dd780-6a71-4f4b-b7f7-6e063bec71d6
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 5021a2074d49d7a8b1da88d82c52b175f16ff3c3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67900633"
---
# <a name="sysdmhadravailabilityreplicaclusterstates-transact-sql"></a>sys.dm_hadr_availability_replica_cluster_states (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  为 Windows Server 故障转移群集 (WSFC) 群集中所有 AlwaysOn 可用性组（无论副本位置如何）的每个 AlwaysOn 可用性副本（无论加入状态如何）都返回一行。  
  
##  <a name="connected_state"></a>  
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|**replica_id**|**uniqueidentifier**|可用性副本的唯一标识符。|  
|**replica_server_name**|**nvarchar(256)**|承载副本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的名称。|  
|**group_id**|**uniqueidentifier**|可用性组的唯一标识符。|  
|**join_state**|**tinyint**|0 = 未联接<br /><br /> 1 = 已联接，独立实例<br /><br /> 2 = 已联接，故障转移群集实例|  
|**join_state_desc**|**nvarchar(60)**|NOT_JOINED<br /><br /> JOINED_STANDALONE_INSTANCE<br /><br /> JOINED_FAILOVER_CLUSTER_INSTANCE|  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>权限  
 要求具有服务器的 VIEW SERVER STATE 权限。  
  
## <a name="see-also"></a>请参阅  
 [监视可用性组 (Transact-SQL)](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
  
