---
title: MSpub_identity_range (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
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
caps.latest.revision: 24
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: eafa458b7ae7d4e90f047659f9bc217f8a28c3b2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
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
|**threshold**|**int**|用于控制分发代理何时分配新标识范围的百分比值。 如果在中指定值的百分比*阈值*是使用，在分发代理程序创建的新标识范围。|  
|**last_seed**|**bigint**|当前范围的下限。|  
  
## <a name="see-also"></a>另请参阅  
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
