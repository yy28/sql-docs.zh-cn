---
title: MSpeer_lsns (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSpeer_lsns
- MSpeer_lsns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSpeer_lsns system table
ms.assetid: 0ba33907-601b-4c3d-8099-2663f680a161
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 08926758b2d217bde6f858405ebde1c2b38b4d66
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52796169"
---
# <a name="mspeerlsns-transact-sql"></a>MSpeer_lsns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **Mspeer_lsns**表用于将每个事务映射到对等复制拓扑中的订阅。 此表存储在采用对等复制拓扑的每个发布数据库中，以及对等发布的所有订阅服务器的订阅数据库中。 有关此类型的事务复制拓扑的详细信息，请参阅[对等事务复制](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)。 该表存储在发布数据库中。  
  
## <a name="definition"></a>定义  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|标识对等 LSN。|  
|**last_updated**|**datetime**|**Datetime**处进行了最后一个的行更新。|  
|**发起方**|**sysname**|发起事务的发布服务器的名称。|  
|**originator_db**|**sysname**|发起事务的数据库的名称。|  
|**originator_publication**|**sysname**|发起事务的发布的名称。|  
|**originator_publication_id**|**int**|发起事务的发布的标识符。|  
|**originator_db_version**|**int**|标识发起方数据库的版本号。|  
|**originator_lsn**|**int**|标识发起发布中的 LSN。|  
|**originator_version**|**int**|指定发布服务器的版本号。|  
|**originator_id**|**smallint**|标识拓扑中的每个节点以进行冲突检测。 有关详细信息，请参阅 [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)。|  
  
## <a name="see-also"></a>请参阅  
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
