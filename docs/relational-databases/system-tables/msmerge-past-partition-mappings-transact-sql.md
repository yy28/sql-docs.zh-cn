---
title: MSmerge_past_partition_mappings （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_past_partition_mappings
- MSmerge_past_partition_mappings_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_past_partition_mappings system table
ms.assetid: 06d54ff5-4d29-4eeb-b8be-64d032e53134
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 9faca4ae8492f7ec0c784b05b16799c5b5b398ae
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82827213"
---
# <a name="msmerge_past_partition_mappings-transact-sql"></a>MSmerge_past_partition_mappings (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  对于给定的已更改行，在该表中，每个分区 id 都**MSmerge_past_partition_mappings**在每个分区 id 中存储一行，但不再属于。 该表存储在发布数据库中。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**publication_number**|**smallint**|存储在**sysmergepublications**中的发布编号。|  
|**tablenick**|**int**|已发布表的别名。|  
|**rowguid**|**uniqueidentifier**|给定行的行标识符。|  
|**partition_id**|**int**|该行所属分区的 ID。 如果行更改与所有订阅服务器相关，则值为-1。|  
|**产生**|**bigint**|发生分区更改的生成的值。|  
|**reason**|**tinyint**|仅供内部使用。|  
  
## <a name="see-also"></a>另请参阅  
 [Transact-sql&#41;&#40;复制表](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
