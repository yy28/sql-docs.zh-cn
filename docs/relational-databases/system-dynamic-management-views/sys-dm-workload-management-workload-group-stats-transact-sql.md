---
title: sys. dm_workload_management_workload_groups_stats （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 11/02/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: = azure-sqldw-latest||= sqlallproducts-allversions
ms.openlocfilehash: 6e77239d019cb51e66a34a3a5b909e01c28a7faa
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "73633431"
---
# <a name="sysdm_workload_management_workload_groups_stats-transact-sql"></a>sys. dm_workload_management_workload_groups_stats （Transact-sql）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

返回工作负荷组统计信息和工作负荷组在中[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]的有效值。  
  
|列名|数据类型|说明|范围|  
|-----------------|---------------|-----------------|-----------|  
|group_id|**int**|工作负荷组的唯一 ID。||
|name|**sysname**|工作负荷组的名称。||
|statistics_start_time|**datetime**|工作负荷组开始统计信息收集的时间。  此值可以是创建工作负荷组或实例暂停或缩放时的值。||
|total_request_count|**bigint**|工作负荷组中已完成请求的累计计数。||
|total_shared_resource_reqeusts|**bigint**|使用共享池中的资源的工作负荷组中已完成请求的累计计数。||
|total_queued_request_count|**bigint**|达到 max_concurrency 限制后排队的请求累计计数。||
|total_request_execution_timeouts|**bigint**|工作负荷组中的请求的累计计数，在完成之前根据 query_execution_timeout_sec 设置超时。||
|effective_min_percentage_resource|**tinyint**|允许考虑服务级别和工作负荷组设置的有效 min_percentage_resource 设置。 可在较低的服务级别调整有效 min_percentage_resource。  例如，在 DW100c 上，允许的最低 min_percentage_resource 为25%。  如果无法在服务级别授予值，则将 min_percentage_resource 调整为0%。  例如 min_percentage_resource，在 DW6000c 设置为10% 时，在向下缩放到 DW100c 时，将具有0% 的 effective_min_percentage_resource。||
|effective_cap_percentage_resource|**tinyint**|工作负荷组的有效 cap_percentage_resource。  如果有其他工作负荷组 min_percentage_resource > 0，effective_cap_percentage_resource 会按比例降低。||
|effective_request_min_resource_grant_percent|**decimal （5，2）**|工作负荷组 request_min_resource_grant_percent 的有效运行时值。 考虑服务级别以及如何配置工作负荷组的有效值。  如果因为服务级别而调整了 min_percentage_resource，effective_request_min_resource_grant_percent 将相应地进行调整。||
|effective_request_max_resource_grant_percent|**decimal （5，2）**|考虑所有工作负荷组的配置的工作负荷组 request_max_resource_grant_percent 的有效运行时值。||
|||||

## <a name="see-also"></a>另请参阅

 [SQL 数据仓库和并行数据仓库动态管理视图 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
