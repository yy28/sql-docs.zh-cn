---
title: MSmerge_genhistory （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_genhistory_TSQL
- MSmerge_genhistory
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_genhistory system table
ms.assetid: 475d08ae-eb8b-49de-afd6-33c96ab8004d
author: stevestein
ms.author: sstein
ms.openlocfilehash: bf9c38fe71c1282b19b947fc1771714dd138c45a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68017699"
---
# <a name="msmerge_genhistory-transact-sql"></a>MSmerge_genhistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  对于订阅者知道的每个代（在保持期内）， **MSmerge_genhistory**表都包含一行。 用于避免在交换时发送公用生成，并使从备份还原的订阅服务器重新同步。 该表存储在发布数据库和订阅数据库中。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**guidsrc**|**uniqueidentifier**|由订阅服务器的生成标识的更改的全局标识符。|  
|**pubid**|**uniqueidentifier**|发布标识符。|  
|**产生**|**bigint**|代值。|  
|**art_nick**|**int**|项目的昵称。|  
|**nicknames**|**varbinary （1001）**|已悉知具有此生成的其他订阅服务器的别名列表。 用来避免将生成发送给已看到那些更改的订阅服务器。 别名列表中的别名按顺序排序，以便提高搜索效率。 如果别名数目超过此字段的容量，将不会从此优化中获益。|  
|**coldate**|**datetime**|将当前生成添加到表时的日期。|  
|**genstatus**|**tinyint**|生成具有下列状态：<br /><br /> **0** = 打开。<br /><br /> **1** = 关闭。<br /><br /> **2** = 关闭，并在另一个订阅服务器上发出。|  
|**changecount**|**int**|给定生成中反映的更改数|  
  
## <a name="see-also"></a>另请参阅  
 [Transact-sql&#41;&#40;复制表](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
