---
title: MScached_peer_lsns （Transact-sql） |Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 7e062d1f7ef5a1c184211a8f4040ac8c295216e7
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82832349"
---
# <a name="mscached_peer_lsns-transact-sql"></a>MScached_peer_lsns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MScached_peer_lsns**表用于跟踪事务日志中的 LSN 值，这些值用于确定将哪些命令返回到对等复制中的给定订阅服务器。 此表存储在分发数据库中。  
  
## <a name="definition"></a>定义  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**agent_id**|**int**|分发代理的 ID。|  
|**发出**|**sysname**|起始发布服务器的名称。|  
|**originator_db**|**sysname**|起始发布数据库的名称。|  
|**originator_publication_id**|**int**|标识起始发布。|  
|**originator_db_version**|**int**|标识发起方数据库的版本号。|  
|**originator_lsn**|**varbinary(16)**|起始事务的 LSN。|  
  
## <a name="remarks"></a>备注  
 LSN 值只能在插入后立即使用，这些值在系统中没有持久含义。  
  
## <a name="see-also"></a>另请参阅  
 [Transact-sql&#41;&#40;复制表](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
