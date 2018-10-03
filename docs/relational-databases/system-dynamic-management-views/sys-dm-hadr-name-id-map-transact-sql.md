---
title: sys.dm_hadr_name_id_map (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_hadr_name_id_map
- sys.dm_hadr_name_id_map_TSQL
- dm_hadr_name_id_map
- dm_hadr_name_id_map_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.dm_hadr_name_id_map dynamic management view
ms.assetid: e07bb8a9-37de-4a39-a257-950d7c3ae8fb
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 9560225279793efc290cae216f7757e0262e2357
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47814055"
---
# <a name="sysdmhadrnameidmap-transact-sql"></a>sys.dm_hadr_name_id_map (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  显示 Always On 可用性组的映射的当前实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]已联接到三个唯一 Id： 一个可用性组 ID、 WSFC 资源 ID 和一个 WSFC 组 id。 此映射旨在处理重命名 WSFC 资源/组的情形。  
   
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**ag_name**|**nvarchar(256)**|可用性组的名称。 这是在 Windows Server 故障转移群集 (WSFC) 群集内必须具有唯一性的用户指定名称。|  
|**ag_id**|**uniqueidentifier**|可用性组的唯一标识符 (GUID)。|  
|**ag_resource_id**|**nvarchar(256)**|作为 WSFC 群集中资源的可用性组的唯一 ID。|  
|**ag_group_id**|**nvarchar(256)**|可用性组的唯一 WSFC 组 ID。|  
  
## <a name="permissions"></a>Permissions  
 要求具有服务器的 VIEW SERVER STATE 权限。  
  
## <a name="see-also"></a>请参阅  
 [AlwaysOn 可用性组动态管理视图和函数 (Transact-SQL)](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)   
 [AlwaysOn 可用性组目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [监视可用性组 (Transact-SQL)](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [AlwaysOn 可用性组 (SQL Server)](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
  
  
