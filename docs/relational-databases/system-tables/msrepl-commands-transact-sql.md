---
title: "MSrepl_commands (Transact SQL) |Microsoft 文档"
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
- MSrepl_commands
- MSrepl_commands_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSrepl_commands system table
ms.assetid: 53b9f9cd-9429-47a0-aba2-908fc60e7036
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ee2da8ec88cc85128e13ef502c083358c623c92f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="msreplcommands-transact-sql"></a>MSrepl_commands (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSrepl_commands**表包含的复制的命令行。 此表存储在分发数据库中。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**publisher_database_id**|**int**|发布服务器数据库的 ID。|  
|**xact_seqno**|**varbinary(16)**|事务序列号。|  
|**type**|**int**|命令类型。|  
|**article_id**|**int**|文章的 ID。|  
|**originator_id**|**int**|发起方的 ID。|  
|**command_id**|**int**|命令的 ID。|  
|**partial_command**|**bit**|指示这是否为部分命令。|  
|**command**|**varbinary(1024)**|命令值。|  
|**hashkey**|**int**|仅供内部使用。|  
|**originator_lsn**|**varbinary(16)**|标识原始发布中命令的 LSN。 这在对等事务复制中使用。|  
  
## <a name="see-also"></a>另请参阅  
 [复制表 &#40;Transact SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 &#40;Transact SQL &#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_replcmds &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)  
  
  
