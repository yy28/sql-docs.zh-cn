---
title: "sys.dm_resource_governor_resource_pool_affinity (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 08/09/2016
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
- sys.dm_resource_governor_resource_pool_affinity_TSQL
- sys.dm_resource_governor_resource_pool_affinity
- dm_resource_governor_resource_pool_affinity
- dm_resource_governor_resource_pool_affinity_TSQL
dev_langs: TSQL
helpviewer_keywords:
- dm_resource_governor_resource_pool_affinity
- sys.dm_resource_governor_resource_pool_affinity
ms.assetid: a197ec19-a2ba-44f5-a4f2-3eee33ebd77d
caps.latest.revision: "9"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5261a64154de7603e4925437cb89271466ec97ce
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmresourcegovernorresourcepoolaffinity-transact-sql"></a>sys.dm_resource_governor_resource_pool_affinity (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  跟踪资源池亲关联。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)。  
  
|Colmn 名称|数据类型|Description|  
|----------------|---------------|-----------------|  
|Pool_id|**int**|资源池的 ID。 不可为 null。|  
|Processor_group|**int**|Windows 逻辑处理器组的 ID。 不可为 null。|  
|Scheduler_mask|**bigint**|表示与此池相关联的计划程序的二进制掩码。 不可为 null。|  
  
## <a name="remarks"></a>注释  
 使用 AUTO 的关联创建的池将不会在此视图中出现，因为它们没有关联。 有关详细信息，请参阅[CREATE RESOURCE POOL &#40;Transact SQL &#41;](../../t-sql/statements/create-resource-pool-transact-sql.md)和[更改资源池 &#40;Transact SQL &#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md)语句。  
  
## <a name="see-also"></a>另请参阅  
 [sys.dm_resource_governor_external_resource_pool_affinity (Transact SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md)  
  
  
