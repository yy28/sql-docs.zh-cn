---
title: sys. resource_governor_external_resource_pools （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 11/13/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.resource_governor_external_resource_pools
- sys.resource_governor_external_resource_pools_TSQL
- resource_governor_external_resource_pools
- resource_governor_external_resource_pools_TSQL
helpviewer_keywords:
- sys.resource_governor_external_resource_pools
- resource_governor_external_resource_pools
ms.assetid: 75063e36-a91b-496f-9936-88f3d57bd447
author: stevestein
ms.author: sstein
ms.openlocfilehash: 79c81cafe588fd827ece6184cab5470df8ec4c42
ms.sourcegitcommit: eef5ab1966062e190dc1cd49409bc0429ba6d1e4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/26/2020
ms.locfileid: "80290844"
---
# <a name="sysresource_governor_external_resource_pools-transact-sql"></a>sys. resource_governor_external_resource_pools （Transact-sql）
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]
**适用于：** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)]和[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)][!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

返回中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]存储的外部资源池配置。 视图的每一行都确定了一个池的配置。
  
|列名称|数据类型|说明|
|-----------------|---------------|-----------------|
|external_pool_id|**int**|资源池的唯一 ID。 不可为 null。|
|name|**sysname**|资源池的名称。 不可为 null。|
|max_cpu_percent|**int**|出现 CPU 争用时资源池中的所有请求可获得的最大 CPU 带宽。 不可为 null。|
|max_memory_percent|**int**|此资源池中的请求可使用的总服务器内存量的百分比。 不可为 null。 有效的最大值取决于池的最小值。 例如，可将 max_memory_percent 设置为 100，但有效的最大值会更低一些。|
|max_processes|**int**|并发外部进程的最大数量。 默认值为 0，指定没有限制。 不可为 null。|
|版本|**bigint**|内部版本号。|
  
## <a name="permissions"></a>权限

需要 VIEW SERVER STATE 权限。

## <a name="see-also"></a>另请参阅

[SQL Server 中的机器学习的资源调控](../../advanced-analytics/r/resource-governance-for-r-services.md)

[Resource Governor 目录视图 &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)

[sys. dm_resource_governor_resource_pools &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md)

[资源调控器](../../relational-databases/resource-governor/resource-governor.md)

[sys. dm_resource_governor_resource_pool_affinity &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pool-affinity-transact-sql.md)

[“已启用外部脚本”服务器配置选项](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)

[ALTER EXTERNAL RESOURCE POOL (Transact-SQL)](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)
