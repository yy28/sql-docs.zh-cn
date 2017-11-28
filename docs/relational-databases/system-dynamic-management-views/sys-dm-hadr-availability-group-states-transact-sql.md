---
title: "sys.dm_hadr_availability_group_states (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_hadr_availability_group_states
- sys.dm_hadr_availability_group_states_TSQL
- dm_hadr_availability_group_states_TSQL
- dm_hadr_availability_group_states
dev_langs: TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.dm_hadr_availability_group_states dynamic management view
ms.assetid: d18019dd-f8dc-4492-b035-b1a639369b65
caps.latest.revision: "43"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b48d1d3291a1cdcbfcaa84b71c323e1ea410afc8
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmhadravailabilitygroupstates-transact-sql"></a>sys.dm_hadr_availability_group_states (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  为每个 Always On 可用性组所拥有的本地实例上的可用性副本返回一行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 每行显示定义给定可用性组的运行状况的状态。  
  
> [!NOTE]  
>  若要获取的完整列表，请查询[sys.availability_groups](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)目录视图。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**group_id**|**uniqueidentifier**|可用性组的唯一标识符。|  
|**primary_replica**|**varchar （128)**|正在承载当前主副本的服务器实例的名称。<br /><br /> NULL = 不是主副本或无法与 WSFC 故障转移群集通信。|  
|**primary_recovery_health**|**tinyint**|指示主副本的恢复状况，可为下列值之一：<br /><br /> 0 = 正在进行<br /><br /> 1 = 联机<br /><br /> NULL<br /><br /> 在辅助副本上**primary_recovery_health**列为 NULL。|  
|**primary_recovery_health_desc**|**nvarchar(60)**|说明**primary_replica_health**、 一个的：<br /><br /> ONLINE_IN_PROGRESS<br /><br /> ONLINE<br /><br /> NULL|  
|**secondary_recovery_health**|**tinyint**|指示辅助副本副本，其中一个恢复运行状况：<br /><br /> 0 = 正在进行<br /><br /> 1 = 联机<br /><br /> NULL<br /><br /> 在主副本上， **secondary_recovery_health**列为 NULL。|  
|**secondary_recovery_health_desc**|**nvarchar(60)**|说明**secondary_recovery_health**、 一个的：<br /><br /> ONLINE_IN_PROGRESS<br /><br /> ONLINE<br /><br /> NULL|  
|**synchronization_health**|**tinyint**|反映的汇总**synchronization_health**的可用性组中的所有可用性副本。 以下是可能的值以及及其说明。<br /><br /> 0： 不正常。 所有可用性副本都没有正常**synchronization_health** (2 = 正常)。<br /><br /> 1： 部分正常运行。 某些（但并非全部）可用性副本的同步运行状况是正常的。<br /><br /> 2： 正常运行。 每个可用性副本的同步运行状况都是正常的。<br /><br /> 有关副本同步运行状况的信息，请参阅**synchronization_health**中的列[sys.dm_hadr_availability_replica_states &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-states-transact-sql.md).|  
|**synchronization_health_desc**|**nvarchar(60)**|说明**synchronization_health**、 一个的：<br /><br /> NOT_HEALTHY<br /><br /> PARTIALLY_HEALTHY<br /><br /> HEALTHY|  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>Permissions  
 要求具有服务器的 VIEW SERVER STATE 权限。  
  
## <a name="see-also"></a>另请参阅  
 [监视可用性组 (Transact-SQL)](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [AlwaysOn 可用性组 (SQL Server)](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [Always On 可用性组动态管理视图和函数 &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)  
  
  
