---
title: "sys.availability_databases_cluster (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.availability_databases_cluster_TSQL
- sys.availability_databases_cluster
- availability_databases_cluster_TSQL
- availability_databases_cluster
dev_langs: TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], WSFC clusters
- sys.availability_databases_cluster catalog view
- Availability Groups [SQL Server], databases
ms.assetid: 8d9c57e5-7f39-4315-b466-92748231140a
caps.latest.revision: "14"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0cd9ecf7618cf95939773f26f9803a9310e78b19
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="sysavailabilitydatabasescluster-transact-sql"></a>sys.availability_databases_cluster (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  包含每个可用性数据库的实例上的一个行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]上承载的可用性副本的 Windows Server 故障转移群集 (WSFC) 群集，而不考虑是否的本地副本数据库中任何 Always On 可用性组联接到可用性组尚未。  
  
> [!NOTE]  
>  将数据库添加到可用性组后，主数据库自动联接到该组。 必须在每个辅助副本上准备辅助数据库，之后才能将其联接到可用性组。   
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**group_id**|**uniqueidentifier**|数据库参与其中的可用性组（如果有）的唯一标识符。<br /><br /> NULL = 数据库不是可用性组中的可用性副本的一部分。|  
|**group_database_id**|**uniqueidentifier**|数据库在其参与的可用性组（如果有）中的唯一标识符。 **group_database_id**对于此数据库和每个辅助副本在其的数据库是否联接到可用性组主副本上均相同。<br /><br /> NULL = 数据库不是任何可用性组中的可用性副本的一部分。|  
|**database_name**|**sysname**|已添加到可用性组的数据库名称。|  
  
## <a name="permissions"></a>Permissions  
 如果调用方**sys.availability_databases_cluster**不是数据库，请参阅相应的行是 ALTER ANY DATABASE 所需的最小权限或 VIEW ANY DATABASE 服务器级权限，或创建的所有者中的数据库权限**master**数据库。  
  
## <a name="see-also"></a>另请参阅  
 [sys.availability_groups &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)   
 [sys.databases (Transact-SQL)](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.dm_hadr_database_replica_states &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)   
 [sys.dm_hadr_database_replica_cluster_states &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-cluster-states-transact-sql.md)   
 [AlwaysOn 可用性组概述 (SQL Server)](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  
