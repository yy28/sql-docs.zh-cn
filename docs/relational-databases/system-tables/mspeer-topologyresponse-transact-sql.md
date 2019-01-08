---
title: MSpeer_topologyresponse (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSpeer_topologyresponse
- MSpeer_topologyresponse_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSpeer_topologyresponse
ms.assetid: 1bc5c0c6-c432-405c-89fd-e953d173a247
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 701cac875a9870de840f7955c3c327aee4133a3f
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52764529"
---
# <a name="mspeertopologyresponse-transact-sql"></a>MSpeer_topologyresponse (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  用于在对等复制中存储每个节点对拓扑状态请求的响应。 该表存储在发布数据库中。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|request_id|**int**|标识中的拓扑状态请求项[MSpeer_topologyrequest](../../relational-databases/system-tables/mspeer-topologyrequest-transact-sql.md)表。|  
|peer|**sysname**|生成响应的服务器实例的名称。|  
|peer_version|**int**|指定发布服务器的版本号。|  
|peer_db|**sysname**|生成响应的对等方的订阅数据库。|  
|originator_id|**int**|标识拓扑中的每个节点以进行冲突检测。 有关详细信息，请参阅 [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)。|  
|peer_conflict_retention|**int**|在冲突表中存储元数据的时间段（以天为单位）。|  
|received_date|**datetime**|收到拓扑请求的时间。|  
|connection_info|**xml**|有关响应请求的节点的信息。|  
  
## <a name="see-also"></a>请参阅  
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
