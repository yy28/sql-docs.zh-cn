---
title: "sys.dm_hadr_cluster (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_hadr_cluster
- dm_hadr_cluster_HADR
- sys.dm_hadr_cluster_TSQL
- dm_hadr_cluster
dev_langs: TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.dm_hadr_cluster catalog view
- Availability Groups [SQL Server], WSFC clusters
ms.assetid: 13ce70e4-9d43-4a80-a826-099e6213bf85
caps.latest.revision: "20"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ea7fef3018ef9e7c88100c1a0c3a7b444bfaeac7
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmhadrcluster-transact-sql"></a>sys.dm_hadr_cluster (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  如果中的托管实例的 Windows Server 故障转移群集 (WSFC) 节点[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]为启用[!INCLUDE[ssHADR](../../includes/sshadr-md.md)]具有 WSFC 仲裁， **sys.dm_hadr_cluster**返回公开群集名称和信息的行有关仲裁。 如果 WSFC 节点不包含任何仲裁，则不返回任何行。  
 > [!TIP]
 > 从[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]，此动态管理视图支持 Alwayson 故障转移群集实例除了 Alwayson 可用性组。

|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**cluster_name**|**nvarchar （128)**|承载启用了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 实例的 WSFC 群集的名称。|  
|**quorum_type**|**tinyint**|此 WSFC 群集使用的仲裁的类型，可为下列值之一：<br /><br /> 0 = 节点的大多数。 此仲裁配置可以承受半数（舍入）减 1 个节点故障。 例如，对于七个节点的群集，此仲裁配置可以承受三个节点故障。<br /><br /> 1 = 节点和磁盘的大多数。 如果磁盘见证服务器保持联机，此仲裁配置可以承受半数（舍入）节点故障。 例如，一个磁盘见证服务器保持联机的六节点群集可以承受三个节点故障。 如果磁盘见证服务器脱机或失败，此仲裁配置可以承受半数（舍入）减 1 个节点故障。 例如，一个磁盘见证服务器已失败的六节点群集可以承受两个 (3-1=2) 节点故障。<br /><br /> 2 = 节点和文件共享的大多数。 此仲裁配置的工作方式与“节点和磁盘的大多数”的工作方式类似，但使用文件共享见证服务器而不是磁盘见证服务器。<br /><br /> 3 = 无大多数: 仅限磁盘。 如果仲裁磁盘联机，此仲裁配置可以承受除一个节点之外的所有节点故障。|  
|**quorum_type_desc**|**varchar(50)**|说明**quorum_type**、 一个的：<br /><br /> NODE_MAJORITY<br /><br /> NODE_AND_DISK_MAJORITY<br /><br /> NODE_AND_FILE_SHARE_MAJORITY<br /><br /> NO_MAJORITY:_DISK_ONLY|  
|**quorum_state**|**tinyint**|WSFC 仲裁的状态，可为下列值之一：<br /><br /> 0 = 未知仲裁状态<br /><br /> 1 = 标准仲裁<br /><br /> 2 = 强制仲裁|  
|**quorum_state_desc**|**varchar(50)**|说明**quorum_state**、 一个的：<br /><br /> UNKNOWN_QUORUM_STATE<br /><br /> NORMAL_QUORUM<br /><br /> FORCED_QUORUM|  
  
## <a name="permissions"></a>Permissions  
 要求具有服务器的 VIEW SERVER STATE 权限。  
  
## <a name="see-also"></a>另请参阅  
 [AlwaysOn 可用性组动态管理视图和函数 (Transact-SQL)](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)   
 [AlwaysOn 可用性组目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [监视可用性组 (Transact-SQL)](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [sys.dm_hadr_cluster_members (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-members-transact-sql.md)  
  
  
