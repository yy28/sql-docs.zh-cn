---
title: MSmerge_genhistory (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
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
- MSmerge_genhistory_TSQL
- MSmerge_genhistory
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_genhistory system table
ms.assetid: 475d08ae-eb8b-49de-afd6-33c96ab8004d
caps.latest.revision: 28
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cabcaca806b2a09617e417542b8b6440280a5016
ms.sourcegitcommit: a431ca21eac82117492d7b84c398ddb3fced53cc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/17/2018
ms.locfileid: "39101685"
---
# <a name="msmergegenhistory-transact-sql"></a>MSmerge_genhistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSmerge_genhistory**表订阅服务器 （在保持期内） 所了解的每个生成占一行。 用于避免在交换时发送公用生成，并使从备份还原的订阅服务器重新同步。 此表存储在发布和订阅数据库中。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**guidsrc**|**uniqueidentifier**|由订阅服务器的生成标识的更改的全局标识符。|  
|**pubid**|**uniqueidentifier**|发布标识符。|  
|**生成**|**bigint**|代值。|  
|**art_nick**|**int**|项目的别名。|  
|**昵称**|**varbinary(1001)**|已悉知具有此生成的其他订阅服务器的别名列表。 用来避免将生成发送给已看到那些更改的订阅服务器。 别名列表中的别名按顺序排序，以便提高搜索效率。 如果别名数目超过此字段的容量，将不会从此优化中获益。|  
|**coldate**|**datetime**|将当前生成添加到表时的日期。|  
|**genstatus**|**tinyint**|生成具有下列状态：<br /><br /> **0** = 打开。<br /><br /> **1** = 关闭。<br /><br /> **2** = 关闭并在另一个订阅服务器发起。|  
|**changecount**|**int**|给定生成中反映的更改数|  
  
## <a name="see-also"></a>请参阅  
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
