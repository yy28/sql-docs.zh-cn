---
title: sys. pdw_loader_backup_run_details （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 04fc004f-ee15-4d7a-be08-78357aa99b55
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: dead5962987f7fb132f21bb4e3517f7cc9249601
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68127649"
---
# <a name="syspdw_loader_backup_run_details-transact-sql"></a>sys. pdw_loader_backup_run_details （Transact-sql）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  包含更详细的信息，而不仅仅是[pdw_loader_backup_runs sys.databases 中的信息 &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-backup-runs-transact-sql.md)，与中[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]的正在进行和已完成的备份、还原和加载操作有关的备份和还原操作有关[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]。 信息在两次系统重启之间仍会保留。  
  
|列名|数据类型|说明|范围|  
|-----------------|---------------|-----------------|-----------|  
|run_id|**int**|特定备份或还原运行的唯一标识符。<br /><br /> run_id 和 pdw_node_id 构成此视图的键。||  
|pdw_node_id|**int**|此记录包含其详细信息的设备节点的唯一标识符。<br /><br /> run_id 和 pdw_node_id 构成此视图的键。|请参阅 dm_pdw_nodes sys.databases 中的 node_id [&#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)。|  
|status|**nvarchar （16）**|运行的当前状态。|"已取消"、"已完成"、"失败"、"排队"、"正在运行"|  
|start_time|**datetime**|在此特定节点上开始操作的时间。||  
|end_time|**datetime**|操作在此特定节点上的结束时间（如果有）。||  
|total_elapsed_time|**int**|此特定节点上的操作运行的总时间。|如果 total_elapsed_time 超过了整数的最大值24.8 （以毫秒为单位），则会导致具体化失败，因为溢出。<br /><br /> 最大值（以毫秒为单位）等效于24.8 天。|  
|进度|**int**|操作的进度，以百分比表示。|0 到 100|  
  
## <a name="see-also"></a>另请参阅  
 [SQL 数据仓库和并行数据仓库目录视图](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
