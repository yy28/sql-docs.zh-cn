---
title: MSmerge_tombstone (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_tombstone_TSQL
- MSmerge_tombstone
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_tombstone system table
ms.assetid: 8b3fc7bf-729b-40f2-8a26-e7dfbe8ddb38
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ab57e69118edfe4a647d6baeedf5a10ee8460247
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63026457"
---
# <a name="msmergetombstone-transact-sql"></a>MSmerge_tombstone (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSmerge_tombstone**表包含已删除的行的信息，并允许将删除传播到其他订阅服务器。 此表存储在发布和订阅数据库中。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**rowguid**|**uniqueidentifier**|行标识符。|  
|**tablenick**|**int**|表的别名。|  
|**类型**|**tinyint**|删除的类型：<br /><br /> 1 = 用户删除。<br /><br /> 5 = 行不再属于筛选分区。<br /><br /> 6 = 系统删除。|  
|**lineage**|**varbinary(249)**|指示被删除的记录的版本，以及删除此记录时已知的更新。 出现两台订阅服务器在同一时间分别对一个行执行更新和删除操作的情况时，允许规则执行一致的冲突解决。|  
|**generation**|**int**|在删除行时赋值。 如果订阅服务器请求 N 代，生成的唯一逻辑删除 > = N 发送。|  
|**logical_record_parent_rowguid**|**uniqueidentifier**|标识被删除的行所属的逻辑记录。|  
|**logical_record_lineage**|**Varbinary(501)**|订阅服务器别名和版本号对，用于维护此行所属的逻辑记录的删除历史记录。|  
  
## <a name="see-also"></a>请参阅  
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
