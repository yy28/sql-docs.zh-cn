---
title: MSpeer_topologyresponse （Transact-sql） |Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b8edfe5033d198eaca52a8cf320e9b3dac9960e7
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85751643"
---
# <a name="mspeer_topologyresponse-transact-sql"></a>MSpeer_topologyresponse (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asdw-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  用于在对等复制中存储每个节点对拓扑状态请求的响应。 该表存储在发布数据库中。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|request_id|**int**|标识[MSpeer_topologyrequest](../../relational-databases/system-tables/mspeer-topologyrequest-transact-sql.md)表中的拓扑状态请求条目。|  
|peer|**sysname**|生成响应的服务器实例的名称。|  
|peer_version|**int**|指定发布服务器的版本号。|  
|peer_db|**sysname**|生成响应的对等方的订阅数据库。|  
|originator_id|**int**|标识拓扑中的每个节点以进行冲突检测。 有关详细信息，请参阅 [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)。|  
|peer_conflict_retention|**int**|在冲突表中存储元数据的时间段（以天为单位）。|  
|received_date|**datetime**|收到拓扑请求的时间。|  
|connection_info|**xml**|有关响应请求的节点的信息。|  
  
## <a name="see-also"></a>另请参阅  
 [Transact-sql&#41;&#40;复制表](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
