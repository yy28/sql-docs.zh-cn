---
title: MSmerge_partition_groups （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_partition_groups_TSQL
- MSmerge_partition_groups
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_partition_groups system table
ms.assetid: 5d56d780-ee40-4afc-9c2a-d1723d86e430
author: stevestein
ms.author: sstein
ms.openlocfilehash: 362735d33f835c7b66e4f0994fd5c4ff6f084f15
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68102196"
---
# <a name="msmerge_partition_groups-transact-sql"></a>MSmerge_partition_groups (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSmerge_partition_groups**表在给定数据库的每个预计算分区中存储一行。 除了列出的列以外，还将为参数化行筛选器中使用的每个函数在该表中添加一列。 例如，如果筛选器使用[HOST_NAME](../../t-sql/functions/host-name-transact-sql.md)函数，则会将名为**HOST_NAME_FN**的列添加到表中。 对于每一组已经与该发布服务器同步的唯一函数值，相应地存储一行。 如果两个或更多个订阅服务器通过对所有这些函数完全相同的值进行同步，则会在该表中共享相同的行，因此将会全部共享相同的分区 ID。该表存储在发布数据库中。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**partition_id**|**int**|为预计算分区提供唯一 ID 号的标识列。|  
|**publication_number**|**smallint**|存储在**sysmergepublications**中的发布编号。|  
|**maxgen_whenadded**|**bigint**|在该表中插入行时在发布服务器中已知的最大生成值。|  
|**using_partition_groups**|**bit**|指示分区是否属于使用预计算分区的发布，可以是下列值之一：<br /><br /> **0** = 发布不使用预计算分区。<br /><br /> **1** = 发布使用预计算分区<br /><br /> 有关详细信息，请参阅[使用预计算分区优化参数化筛选器性能](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)。|  
|**HOST_NAME_FN**|**nvarchar(128)**|使用参数化行筛选器生成分区时所提供的值。 有关详细信息，请参阅 [参数化行筛选器](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)。|  
  
## <a name="see-also"></a>另请参阅  
 [Transact-sql&#41;&#40;复制表](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
