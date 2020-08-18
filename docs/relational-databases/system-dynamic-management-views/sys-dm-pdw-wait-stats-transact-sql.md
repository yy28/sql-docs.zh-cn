---
description: 'sys. dm_pdw_wait_stats (Transact-sql) '
title: sys. dm_pdw_wait_stats (Transact-sql) |Microsoft Docs
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
ms.openlocfilehash: f5a8d40b7181f932f5e42192224e91f5c6aa4c8a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88397823"
---
# <a name="sysdm_pdw_wait_stats-transact-sql"></a>sys. dm_pdw_wait_stats (Transact-sql) 
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  保存与在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不同节点上运行的实例相关的操作系统状态相关信息。 有关等待类型及其说明的列表，请参阅 [dm_os_wait_stats](https://msdn.microsoft.com/library/ms179984\(v=sql.120\).aspx)。  
  
|列名|数据类型|说明|范围|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|此项引用的节点的 ID。||  
|**wait_name**|**nvarchar(255)**|等待类型的名称。||  
|**max_wait_time**|**bigint**|此等待类型的最长等待时间。||  
|**request_count**|**bigint**|此等待类型未完成的等待次数。||  
|**signal_time**|**bigint**|正在等待的线程从收到信号通知到其开始运行之间的时差。||  
|**completed_count**|**bigint**|自上次服务器重新启动以来已完成的等待的总次数。||  
|**wait_time**|**bigint**|此等待类型在 millisecons 中的总等待时间。 包含 signal_time。||  
  
## <a name="see-also"></a>另请参阅  
 [SQL 数据仓库和并行数据仓库动态管理视图 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)   
 [sys. dm_pdw_waits &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md)  
  
  
