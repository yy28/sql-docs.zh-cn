---
title: sys. dm_pdw_wait_stats （Transact-sql） |Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68088719"
---
# <a name="sysdm_pdw_wait_stats-transact-sql"></a>sys. dm_pdw_wait_stats （Transact-sql）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  保存与在不同节点[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]上运行的实例相关的操作系统状态相关信息。 有关等待类型及其说明的列表，请参阅[dm_os_wait_stats](https://msdn.microsoft.com/library/ms179984\(v=sql.120\).aspx)。  
  
|列名|数据类型|说明|范围|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id |**int**|此项引用的节点的 ID。||  
|**wait_name**|**nvarchar(255)**|等待类型的名称。||  
|**max_wait_time**|**bigint**|此等待类型的最长等待时间。||  
|**request_count**|**bigint**|此等待类型未完成的等待次数。||  
|**signal_time**|**bigint**|正在等待的线程从收到信号通知到其开始运行之间的时差。||  
|**completed_count**|**bigint**|自上次服务器重新启动以来已完成的等待的总次数。||  
|**wait_time**|**bigint**|此等待类型在 millisecons 中的总等待时间。 包含 signal_time。||  
  
## <a name="see-also"></a>另请参阅  
 [SQL 数据仓库和并行数据仓库动态管理视图 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)   
 [sys. dm_pdw_waits &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md)  
  
  
