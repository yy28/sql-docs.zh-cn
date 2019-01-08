---
title: MSmerge_identity_range_allocations (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_identity_range_allocations
- MSmerge_identity_range_allocations_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_identity_range_allocations system table
ms.assetid: 6362e35e-0ab3-4638-855b-1ce013f5fd6d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 09544c1e8735c3a6ad4fd6abfca430e84fabd775
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52809689"
---
# <a name="msmergeidentityrangeallocations-transact-sql"></a>MSmerge_identity_range_allocations (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSmerge_identity_range_allocations**表用于跟踪的标识范围分配，对发布服务器和订阅服务器，已发布项目的历史记录。 此表存储在分发数据库中。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|发布服务器的 ID。|  
|**publisher_db**|**nvarchar(128)**|发布数据库的名称。|  
|**发布**|**nvarchar(128)**|发布的名称。|  
|**article**|**nvarchar(128)**|项目的名称。|  
|**订阅服务器**|**nvarchar(128)**|订阅服务器的名称。|  
|**subscriber_db**|**nvarchar(128)**|订阅数据库的名称。|  
|**is_pub_range**|**bit**|列出是否将标识范围分配给发布服务器。|  
|**ranges_allocated**|**tinyint**|已分配的标识范围数。|  
|**range_begin**|**numeric(38)**|范围的起始值。|  
|**range_end**|**numeric(38)**|范围中的最后一个值。|  
|**next_range_begin**|**numeric(38)**|要分配的下一个范围的起始值。|  
|**next_range_end**|**numeric(38)**|要分配的下一个范围中的最后一个值。|  
|**max_used**|**numeric(38)**|所使用的最大标识值。|  
|**time_of_allocation**|**datetime**|执行分配的时间。|  
  
## <a name="see-also"></a>请参阅  
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
