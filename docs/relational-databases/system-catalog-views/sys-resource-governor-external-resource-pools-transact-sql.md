---
title: 系统resource_governor_external_resource_pools（转用-SQL） |微软文档
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
ms.openlocfilehash: 4751cb9164d5ca11cfdaca4365fa7156c2c2425e
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/04/2020
ms.locfileid: "80663001"
---
# <a name="sysresource_governor_external_resource_pools-transact-sql"></a>系统resource_governor_external_resource_pools（转算-SQL）
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]
**适用于：**[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)][!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)]和[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)][!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

返回 中的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]存储的外部资源池配置。 视图的每一行都确定了一个池的配置。
  
|列名称|数据类型|说明|
|-----------------|---------------|-----------------|
|external_pool_id|**Int**|资源池的唯一 ID。 不可为 null。|
|name|**sysname**|资源池的名称。 不可为 null。|
|max_cpu_percent|**Int**|出现 CPU 争用时资源池中的所有请求可获得的最大 CPU 带宽。 不可为 null。|
|max_memory_percent|**Int**|此资源池中的请求可使用的总服务器内存量的百分比。 不可为 null。 有效的最大值取决于池的最小值。 例如，可将 max_memory_percent 设置为 100，但有效的最大值会更低一些。|
|max_processes|**Int**|并发外部进程的最大数量。 默认值为 0，指定没有限制。 不可为 null。|
|版本|**比金特**|内部版本号。|
  
## <a name="permissions"></a>权限

需要 VIEW SERVER STATE 权限。

## <a name="see-also"></a>请参阅

[SQL Server 中机器学习的资源调控](../../machine-learning/administration/resource-governor.md)

[资源调控器目录视图&#40;处理-SQL&#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)

[sys.dm_resource_governor_resource_pools (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md)

[Resource Governor](../../relational-databases/resource-governor/resource-governor.md)

[系统dm_resource_governor_resource_pool_affinity&#40;转算-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pool-affinity-transact-sql.md)

[启用了外部脚本的服务器配置选项](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)

[ALTER EXTERNAL RESOURCE POOL (Transact-SQL)](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)
