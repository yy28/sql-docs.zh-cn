---
description: MSmerge_identity_range (Transact-SQL)
title: MSmerge_identity_range (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_identity_range_TSQL
- MSmerge_identity_range
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_identity_range system table
ms.assetid: 493a2028-88a0-4e83-ad89-ae5661d9f477
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 4011fcc653e72327fbbd20b3b7d8ec1da135f4f9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88463905"
---
# <a name="msmerge_identity_range-transact-sql"></a>MSmerge_identity_range (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSmerge_identity_range**表用于跟踪分配给订阅的标识列的数值范围，这些列用于对复制自动管理这些范围分配的发布。 该表存储在发布数据库和订阅数据库中。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**subid**|**uniqueidentifier**|给定订阅的唯一标识号。|  
|**artid**|**uniqueidentifier**|给定项目的唯一标识号。|  
|**range_begin**|**数值 (38) **|当前范围的开始标识值。|  
|**range_end**|**数值 (38) **|当前范围的结束标识值。|  
|**next_range_begin**|**数值 (38) **|要分配的下一个范围的开始标识值。|  
|**next_range_end**|**数值 (38) **|要分配的下一个范围的结束标识值。|  
|**is_pub_range**|**bit**|如果为发布指定了标识范围，则该值为 **1** 。|  
|**max_used**|**数值 (38) **|可分配的最大标识值。|  
  
## <a name="see-also"></a>另请参阅  
 [Transact-sql&#41;&#40;复制表 ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
