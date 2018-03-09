---
title: "MSpub_identity_range (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSpub_identity_range_TSQL
- MSpub_identity_range
dev_langs:
- TSQL
helpviewer_keywords:
- MSpub_identity_range system table
ms.assetid: 68746eef-32e1-42bc-aff0-9798cd0e88b8
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dcf00bab09fb47969439740d4b93b40fd89bf42e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="mspubidentityrange-transact-sql"></a>MSpub_identity_range (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSpub_identity_range**表提供了标识范围管理支持。 该表存储在发布数据库和订阅数据库中。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**objid**|**int**|包含由复制管理的标识列的表的 ID。|  
|**范围**|**bigint**|控制将在调整的订阅中分配的连续标识值的范围大小。|  
|**pub_range**|**bigint**|控制将在调整的发布中分配的连续标识值的范围大小。|  
|**current_pub_range**|**bigint**|发布使用的当前范围。 它可以不同于*pub_range*如果更改了所后查看**sp_changearticle**和下一步的范围调整之前。|  
|**阈值**|**int**|用于控制分发代理何时分配新标识范围的百分比值。 如果在中指定值的百分比*阈值*是使用，在分发代理程序创建的新标识范围。|  
|**last_seed**|**bigint**|当前范围的下限。|  
  
## <a name="see-also"></a>另请参阅  
 [复制表 &#40;Transact SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
