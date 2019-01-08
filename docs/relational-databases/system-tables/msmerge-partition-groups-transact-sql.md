---
title: MSmerge_partition_groups (Transact SQL) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: cb8c77ba54e25c574d5f751febe8bdac3ba1dfbf
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52775339"
---
# <a name="msmergepartitiongroups-transact-sql"></a>MSmerge_partition_groups (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSmerge_partition_groups**表为每个预计算分区在给定的数据库中存储一行。 除了列出的列以外，还将为参数化行筛选器中使用的每个函数在该表中添加一列。 例如，一个名为的列**HOST_NAME_FN**如果使用筛选器添加到表[HOST_NAME](../../t-sql/functions/host-name-transact-sql.md)函数。 对于每一组已经与该发布服务器同步的唯一函数值，相应地存储一行。 如果两个或更多个订阅服务器进行同步时使用的函数值完全相同，则会在该表中包含相同的行，因此将全部使用相同的分区 ID。该表存储在发布数据库中。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**partition_id**|**int**|为预计算分区提供唯一 ID 号的标识列。|  
|**publication_number**|**smallint**|存储中的发布编号**sysmergepublications**。|  
|**maxgen_whenadded**|**bigint**|在该表中插入行时在发布服务器中已知的最大生成值。|  
|**using_partition_groups**|**bit**|指示分区是否属于使用预计算分区的发布，可以是下列值之一：<br /><br /> **0** = 发布不使用预计算的分区。<br /><br /> **1** = 发布使用预计算的分区<br /><br /> 有关详细信息，请参阅[使用预计算分区优化参数化筛选器性能](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)。|  
|**HOST_NAME_FN**|**nvarchar(128)**|使用参数化行筛选器生成分区时所提供的值。 有关详细信息，请参阅 [参数化行筛选器](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)。|  
  
## <a name="see-also"></a>请参阅  
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
