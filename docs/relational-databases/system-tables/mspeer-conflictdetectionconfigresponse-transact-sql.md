---
title: "MSpeer_conflictdetectionconfigresponse (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
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
- MSpeer_conflictdetectionconfigresponse
- MSpeer_conflictdetectionconfigresponse_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSpeer_conflictdetectionconfigureresponse
ms.assetid: 2685fb66-731d-40f7-af4b-596b9222c5d4
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cb96eb44f44e3a7a0d1e1e4bcd0b1ce8dc00cf5e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="mspeerconflictdetectionconfigresponse-transact-sql"></a>MSpeer_conflictdetectionconfigresponse (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  用于在对等复制中存储每个节点对拓扑范围内配置请求的响应。 该表存储在发布数据库中。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|request_id|**int**|标识中的冲突配置请求项[MSpeer_conflictdetectionconfigrequest](../../relational-databases/system-tables/mspeer-conflictdetectionconfigrequest-transact-sql.md)表。|  
|peer_node|**sysname**|生成响应的服务器实例的名称。|  
|peer_db|**sysname**|在生成响应的对等方的订阅数据库。|  
|peer_version|**sysname**|指定发布服务器的版本号。|  
|peer_db_version|**sysname**|指定对等数据库的版本号。|  
|is_peer|**bit**|指示节点是否为只读订阅服务器。 值为**0**指示只读订阅服务器。|  
|conflict_detection_enabled|**bit**|指示是否为拓扑启用了冲突检测。|  
|originator_id|**varbinary(16)**|标识拓扑中的每个节点以进行冲突检测。 有关详细信息，请参阅 [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)。|  
|peer_conflict_retention|**int**|在冲突表中存储元数据的时间段（以天为单位）。|  
|peer_subscriptions|**XML**|有关响应请求的节点的信息。|  
|progress_phase|**nvarchar(32)**|使用下列值之一标识当前处理阶段：<br /><br /> Started<br /><br /> 已收集对等方版本<br /><br /> 已收集状态|  
|modified_date|**datetime**|阶段的完成日期和时间。|  
  
## <a name="see-also"></a>另请参阅  
 [复制表 &#40;Transact SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
