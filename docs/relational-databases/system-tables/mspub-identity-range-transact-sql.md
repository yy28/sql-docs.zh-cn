---
title: MSpub_identity_range (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSpub_identity_range_TSQL
- MSpub_identity_range
dev_langs:
- TSQL
helpviewer_keywords:
- MSpub_identity_range system table
ms.assetid: 68746eef-32e1-42bc-aff0-9798cd0e88b8
author: stevestein
ms.author: sstein
ms.openlocfilehash: b1b204024d65e72eb65eefc9f63f914eab6ace29
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68032598"
---
# <a name="mspubidentityrange-transact-sql"></a>MSpub_identity_range (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSpub_identity_range**表提供了标识范围管理支持。 该表存储在发布数据库和订阅数据库中。  
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|**objid**|**int**|包含由复制管理的标识列的表的 ID。|  
|**范围**|**bigint**|控制将在调整的订阅中分配的连续标识值的范围大小。|  
|**pub_range**|**bigint**|控制将在调整的发布中分配的连续标识值的范围大小。|  
|**current_pub_range**|**bigint**|发布使用的当前范围。 它可以不同于*pub_range*如果更改后查看**sp_changearticle**和下一步的范围调整前。|  
|**threshold**|**int**|用于控制分发代理何时分配新标识范围的百分比值。 在指定的值的百分比*阈值*是使用，分发代理将创建一个新的标识范围。|  
|**last_seed**|**bigint**|当前范围的下限。|  
  
## <a name="see-also"></a>请参阅  
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
