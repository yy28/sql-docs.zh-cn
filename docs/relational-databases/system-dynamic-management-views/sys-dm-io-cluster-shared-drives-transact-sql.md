---
title: sys.dm_io_cluster_shared_drives (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_io_cluster_shared_drives_TSQL
- sys.dm_io_cluster_shared_drives
- dm_io_cluster_shared_drives_TSQL
- dm_io_cluster_shared_drives
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_io_cluster_shared_drives dynamic management view
ms.assetid: c8fcced8-c780-49dc-99bd-6beb3ca532c4
caps.latest.revision: 30
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 94586c73133a356ae384bca075efd68de27cdea7
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2018
ms.locfileid: "39555017"
---
# <a name="sysdmioclustershareddrives-transact-sql"></a>sys.dm_io_cluster_shared_drives (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  如果当前服务器实例为群集服务器，则此视图返回每个共享驱动器的名称。 如果当前服务器实例不是群集实例，则返回空行集。  
  
> [!NOTE]  
>  若要调用此项从[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用名称**sys.dm_pdw_nodes_io_cluster_shared_drives**。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**DriveName**|**nchar(2)**|驱动器的名称（驱动器号），表示共享群集磁盘阵列中的单个磁盘。 此列不可为空值。|  
|**pdw_node_id**|**int**|**适用于**: ssPDW<br /><br /> 对于此分布的节点标识符。|  
  
## <a name="remarks"></a>Remarks  
 如果已启用群集，则故障转移群集实例要求数据和日志文件位于共享磁盘上，以便在实例故障转移到另一节点后，可以访问这些数据和日志文件。 该视图中的每一行代表一个由此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 群集实例使用的共享磁盘。 只有该视图中所列磁盘可以用于存储该 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的数据或日志文件。 该视图中所列磁盘属于与实例关联的群集资源组。  
  
> [!NOTE]  
>  此视图将在未来版本中弃用。 我们建议你使用[sys.dm_io_cluster_valid_path_names &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-io-cluster-valid-path-names-transact-sql.md)相反。  
  
## <a name="permissions"></a>Permissions  
 用户必须对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例拥有 VIEW SERVER STATE 权限。  
  
## <a name="examples"></a>示例  
 以下示例使用 sys.dm_io_cluster_shared_drives，在群集服务器实例上确定共享驱动器：  
  
```  
SELECT * FROM sys.dm_io_cluster_shared_drives;  
```  
  
 下面是结果集：  
  
 DriveName  
  
 --------\-  
  
 m  
  
 n  
  
## <a name="see-also"></a>请参阅  
 [sys.dm_io_cluster_valid_path_names &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-io-cluster-valid-path-names-transact-sql.md)   
 [sys.dm_os_cluster_nodes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-cluster-nodes-transact-sql.md)   
 [sys.fn_servershareddrives &#40;TRANSACT-SQL&#41;](../../relational-databases/system-functions/sys-fn-servershareddrives-transact-sql.md)   
 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  
