---
title: sys.dm_pdw_wait_stats (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: cfb8d905-c34f-44de-9574-dde81e170916
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 2d5815783528b89716cc8bfb426ea7c1b274802e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68088719"
---
# <a name="sysdmpdwwaitstats-transact-sql"></a>sys.dm_pdw_wait_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  包含与相关的信息[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]OS 状态与不同节点上运行的实例相关。 等待类型和及其说明的列表，请参阅[sys.dm_os_wait_stats](https://msdn.microsoft.com/library/ms179984\(v=sql.120\).aspx)。  
  
|列名|数据类型|描述|范围|  
|-----------------|---------------|-----------------|-----------|  
|**pdw_node_id**|**int**|此项引用的节点 ID。||  
|**wait_name**|**nvarchar(255)**|等待类型的名称。||  
|**max_wait_time**|**bigint**|此等待类型的最长等待时间。||  
|**request_count**|**bigint**|此等待数等待未完成的类型。||  
|**signal_time**|**bigint**|正在等待的线程从收到信号通知到其开始运行之间的时差。||  
|**completed_count**|**bigint**|重新启动以来的最后一个服务器完成此类型的等待的总数。||  
|**wait_time**|**bigint**|该等待类型的 millisecons 的总等待时间。 Signal_time 的非独占时间。||  
  
## <a name="see-also"></a>请参阅  
 [SQL 数据仓库和并行数据仓库动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)   
 [sys.dm_pdw_waits &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md)  
  
  
