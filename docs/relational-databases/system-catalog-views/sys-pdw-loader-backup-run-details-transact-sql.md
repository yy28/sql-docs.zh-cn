---
title: sys.pdw_loader_backup_run_details (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 04fc004f-ee15-4d7a-be08-78357aa99b55
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 76c6b3030ba8701e5d5bb1753a09b1390a713e07
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47727966"
---
# <a name="syspdwloaderbackuprundetails-transact-sql"></a>sys.pdw_loader_backup_run_details (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  包含更多详细的信息中的信息之外[sys.pdw_loader_backup_runs &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-backup-runs-transact-sql.md)和正在进行和已完成的备份和还原操作中的关于[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]和有关正在进行完成备份、 还原和加载操作中的[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]。 信息在两次系统重启之间仍会保留。  
  
|列名|数据类型|Description|范围|  
|-----------------|---------------|-----------------|-----------|  
|run_id|**int**|为特定的备份或还原运行的唯一标识符。<br /><br /> run_id 和 pdw_node_id 形成此视图的键。||  
|pdw_node_id|**int**|此记录保存详细信息的设备节点的唯一标识符。<br /><br /> run_id 和 pdw_node_id 形成此视图的键。|请参阅中的 node_id [sys.dm_pdw_nodes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)。|  
|status|**nvarchar(16)**|运行的当前状态。|取消，已完成，失败、 已排队、 正在运行|  
|start_time|**datetime**|在此特定节点启动操作的时间。||  
|end_time|**datetime**|在操作结束时间在此特定节点上，如果有的话。||  
|total_elapsed_time|**int**|在此特定节点运行该操作的总时间。|如果 total_elapsed_time 超过一个整数 （以毫秒为单位的 24.8 天） 的最大值，它将导致具体化失败由于溢出。<br /><br /> 以毫秒为单位的最大值相当于 24.8 天。|  
|进度|**int**|操作表示为百分比的进度。|0 到 100|  
  
## <a name="see-also"></a>请参阅  
 [SQL 数据仓库和并行数据仓库目录视图](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
