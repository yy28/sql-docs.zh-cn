---
title: sys.resource_governor_workload_groups (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/16/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.resource_governor_workload_groups
- resource_governor_workload_groups_TSQL
- sys.resource_governor_workload_groups_TSQL
- resource_governor_workload_groups
dev_langs:
- TSQL
helpviewer_keywords:
- sys.resource_governor_workload_groups catalog view
ms.assetid: 619ba4b7-868f-4784-b527-ec1dfd703c4f
caps.latest.revision: 20
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ed0f740bab86f9199a5610dc038c39da940f6235
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sysresourcegovernorworkloadgroups-transact-sql"></a>sys.resource_governor_workload_groups (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的存储工作负荷组配置。 每个工作负荷组都可以订阅一个且只能订阅一个资源池。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|group_id|**int**|工作负荷组的唯一 ID。 不可为 null。|  
|name|**sysname**|工作负荷组的名称。 不可为 null。|  
|importance|**sysname**|**注意：**重要性仅适用于在相同的资源池中的工作负荷组。<br /><br /> 此工作负荷组中的请求的相对重要性。 重要性是以下项之一，使用介质正在默认值： 低、 中、 高。<br /><br /> 不可为 null。|  
|request_max_memory_grant_percent|**int**|授予单个请求的最大内存量（以百分比表示）。 默认值为 25。 不可为 null。<br /><br /> **注意：**如果此设置为高于 50%，则较大的查询将运行一次一个地。 因此，在查询正在运行时出现内存不足错误的风险更高。|  
|request_max_cpu_time_sec|**int**|针对单个请求的最大 CPU 使用限制（以秒为单位）。 默认值为 0，指定没有限制。 不可为 null。<br /><br /> **注意：**详细信息，请参阅[CPU 阈值超出 Event Class](../../relational-databases/event-classes/cpu-threshold-exceeded-event-class.md)。|  
|request_memory_grant_timeout_sec|**int**|针对单个请求的内存授予超时（以秒为单位）。 默认值为 0，表示使用基于查询开销的内部计算。 不可为 null。|  
|max_dop|**int**|工作负荷组的最大并行度。 默认值为 0，表示使用全局设置。 不可为 null。<br /><br /> **节点：**此设置将重写查询选项**maxdop**。|  
|group_max_requests|**int**|并发请求的最大数目。 默认值为 0，指定没有限制。 不可为 null。|  
|pool_id|**int**|此工作负荷组使用的资源池的 ID。|  
|external_pool_id|**int**|**适用范围**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 此工作负荷组使用的外部资源池的 ID。|  
  
## <a name="remarks"></a>注释  
 目录视图显示存储的元数据。 若要查看内存中配置，请使用相应的动态管理视图中， [sys.dm_resource_governor_workload_groups &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-workload-groups-transact-sql.md)。  
  
 如果资源调控器配置已发生更改，但尚未应用 ALTER RESOURCE GOVERNOR RECONFIGURE 语句，则存储的配置和内存中的配置可能会不同。  
  
## <a name="permissions"></a>权限  
 若要查看内容，则需要拥有 VIEW ANY DEFINITION 权限；若要更改内容，则需要拥有 CONTROL SERVER 权限。  
  
## <a name="see-also"></a>另请参阅  
 [sys.dm_resource_governor_workload_groups (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-workload-groups-transact-sql.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [资源调控器目录视图&#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)  
  
  
