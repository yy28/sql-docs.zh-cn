---
title: sys.dm_hadr_cluster_members (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/31/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_hadr_cluster_members_TSQL
- sys.dm_hadr_cluster_members
- dm_hadr_cluster_members_TSQL
- dm_hadr_cluster_members
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], WSFC clusters
- sys.dm_hadr_cluster_members catalog view
ms.assetid: feb20b3a-8835-41d3-9a1c-91d3117bc170
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e19451a24d35e63fa84a17d409d19b5c9b02ccc3
ms.sourcegitcommit: 7c052fc969d0f2c99ad574f99076dc1200d118c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2019
ms.locfileid: "55570720"
---
# <a name="sysdmhadrclustermembers-transact-sql"></a>sys.dm_hadr_cluster_members (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  如果承载启用了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 本地实例的 WSFC 节点具有 SQL 仲裁，则为构成仲裁的每一个成员及各个成员的状态都返回一行。 这包括在群集中的所有节点 (返回与 CLUSTER_ENUM_NODE 类型一同**Clusterenum**函数) 以及磁盘或文件共享见证服务器，如果有的话。 为给定成员返回的行包含有关该成员状态的信息。 例如，对于具有一个节点已关闭，当多数节点仲裁的五节点群集**sys.dm_hadr_cluster_members**为启用的服务器实例从查询[!INCLUDE[ssHADR](../../includes/sshadr-md.md)]驻留在具有仲裁的节点上**sys.dm_hadr_cluster_members**反映为"NODE_DOWN"已关闭节点的状态。  
  
 如果 WSFC 节点没有仲裁，则不会返回任何行。  
  
 使用此动态管理视图可以解答下列问题：  
  
-   哪些节点当前正在 WSFC 群集上运行？  
  
-   WSFC 群集可以容忍多少次失败，之后才会在多数节点情况下失去仲裁？  

 > [!TIP]
 > 从[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]，此动态管理视图支持 Alwayson 故障转移群集实例除了 Always On 可用性组。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**member_name**|**nvarchar(128)**|成员名称，可以是一个计算机名称、驱动器号或文件共享路径。|  
|**member_type**|**tinyint**|成员的类型，可为下列值之一：<br /><br /> 0 = WSFC 节点<br /><br /> 1 = 磁盘见证服务器<br /><br /> 2 = 文件共享见证服务器<br /><br /> 3 = 云见证|  
|**member_type_desc**|**nvarchar(50)**|说明**member_type**、 一个的：<br /><br /> CLUSTER_NODE<br /><br /> DISK_WITNESS<br /><br /> FILE_SHARE_WITNESS<br /><br /> CLOUD_WITNESS|  
|**member_state**|**tinyint**|成员状态，可为下列值之一：<br /><br /> 0 = 脱机<br /><br /> 1 = 联机|  
|**member_state_desc**|**nvarchar(60)**|说明**member_state**、 一个的：<br /><br /> UP<br /><br /> 向下|  
|**number_of_quorum_votes**|**tinyint**|此仲裁成员拥有的仲裁票数。 对于无多数：磁盘仅仲裁提供支持，此值默认为 0。 对于其他仲裁类型，此值默认为 1。|  
  
## <a name="permissions"></a>权限  
 要求具有服务器的 VIEW SERVER STATE 权限。  
  
## <a name="examples"></a>示例  
  
## <a name="see-also"></a>请参阅  
 [AlwaysOn 可用性组动态管理视图和函数 (Transact-SQL)](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)   
 [AlwaysOn 可用性组目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [监视可用性组 (Transact-SQL)](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [AlwaysOn 可用性组&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
  
  
