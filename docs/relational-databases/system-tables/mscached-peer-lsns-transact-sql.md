---
title: MScached_peer_lsns (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MScached_peer_lsns_TSQL
- MScached_peer_lsns
dev_langs:
- TSQL
helpviewer_keywords:
- MScached_peer_lsns system table
ms.assetid: f8b6089a-0230-45f9-8c34-9fe0d2a3a74e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 406715f59a3a45184b9700d72331688911bc83e2
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52810299"
---
# <a name="mscachedpeerlsns-transact-sql"></a>MScached_peer_lsns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MScached_peer_lsns**表用于跟踪用于确定的命令以返回到对等复制中的给定订阅服务器中的事务日志的 LSN 值。 此表存储在分发数据库中。  
  
## <a name="definition"></a>定义  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**agent_id**|**int**|分发代理的 ID。|  
|**发起方**|**sysname**|起始发布服务器的名称。|  
|**originator_db**|**sysname**|起始发布数据库的名称。|  
|**originator_publication_id**|**int**|标识起始发布。|  
|**originator_db_version**|**int**|标识发起方数据库的版本号。|  
|**originator_lsn**|**varbinary(16)**|起始事务的 LSN。|  
  
## <a name="remarks"></a>备注  
 LSN 值只能在插入后立即使用，这些值在系统中没有持久含义。  
  
## <a name="see-also"></a>请参阅  
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
