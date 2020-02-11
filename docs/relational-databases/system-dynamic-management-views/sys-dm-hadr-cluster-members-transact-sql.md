---
title: sys. dm_hadr_cluster_members （Transact-sql） |Microsoft Docs
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
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8b28b708aabfdf3ec4e569aab6d8a95e2330b370
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67900767"
---
# <a name="sysdm_hadr_cluster_members-transact-sql"></a>sys.dm_hadr_cluster_members (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  如果承载启用了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 本地实例的 WSFC 节点具有 SQL 仲裁，则为构成仲裁的每一个成员及各个成员的状态都返回一行。 这包括群集中的所有节点（使用**Clusterenum**函数返回 CLUSTER_ENUM_NODE 类型）以及磁盘或文件共享见证（如果有）。 为给定成员返回的行包含有关该成员状态的信息。 例如，对于具有多数节点仲裁（其中一个节点处于关闭状态）的五个节点群集，当从为驻留在具有**dm_hadr_cluster_members**仲裁的节点上[!INCLUDE[ssHADR](../../includes/sshadr-md.md)]的节点上启用的服务器实例（即 "NODE_DOWN"）中查询 " **sys. dm_hadr_cluster_members**时。  
  
 如果 WSFC 节点没有仲裁，则不会返回任何行。  
  
 使用此动态管理视图可以解答下列问题：  
  
-   哪些节点当前正在 WSFC 群集上运行？  
  
-   WSFC 群集可以容忍多少次失败，之后才会在多数节点情况下失去仲裁？  

 > [!TIP]
 > 从开始[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]，此动态管理视图除了支持 Always On 可用性组外，还支持 Always On 故障转移群集实例。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**member_name**|**nvarchar(128)**|成员名称，可以是一个计算机名称、驱动器号或文件共享路径。|  
|**member_type**|**tinyint**|成员的类型，可为下列值之一：<br /><br /> 0 = WSFC 节点<br /><br /> 1 = 磁盘见证服务器<br /><br /> 2 = 文件共享见证服务器<br /><br /> 3 = 云见证|  
|**member_type_desc**|**nvarchar(50)**|**Member_type**的说明，请执行以下操作之一：<br /><br /> CLUSTER_NODE<br /><br /> DISK_WITNESS<br /><br /> FILE_SHARE_WITNESS<br /><br /> CLOUD_WITNESS|  
|**member_state**|**tinyint**|成员状态，可为下列值之一：<br /><br /> 0 = 脱机<br /><br /> 1 = 联机|  
|**member_state_desc**|**nvarchar （60）**|**Member_state**的说明，请执行以下操作之一：<br /><br /> UP<br /><br /> DOWN|  
|**number_of_quorum_votes**|**tinyint**|此仲裁成员拥有的仲裁票数。 对于“无大多数: 仅限磁盘”仲裁，此值默认为 0。 对于其他仲裁类型，此值默认为 1。|  
  
## <a name="permissions"></a>权限  
 要求具有服务器的 VIEW SERVER STATE 权限。  
  
## <a name="examples"></a>示例  
  
## <a name="see-also"></a>另请参阅  
 [Always On 可用性组动态管理视图和函数 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)   
 [Always On 可用性组目录视图 &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [监视可用性组 (Transact-SQL)](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [AlwaysOn 可用性组 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
  
  
