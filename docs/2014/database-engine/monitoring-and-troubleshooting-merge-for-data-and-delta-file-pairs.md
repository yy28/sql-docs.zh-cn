---
title: 监视和故障排除合并的数据和差异文件对 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a8b0bacc-4d2c-42e4-84bf-1a97e0bd385b
caps.latest.revision: 12
author: stevestein
ms.author: sstein
manager: jhubbard
ms.openlocfilehash: 31c717aca9153ee851a35992ebdced9cea2d86c0
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36017396"
---
# <a name="monitoring-and-troubleshooting-merge-for-data-and-delta-file-pairs"></a>监视数据与差异文件对的合并以及排除其故障
  内存中 OLTP 使用合并策略自动合并相邻数据和差异文件对。 无法禁用合并活动。  
  
 可按如下方式监视数据和差异文件对：  
  
-   将内存中存储的大小与存储的总大小进行比较。 如果存储大得不成比例，则可能未触发合并。 有关信息  
  
-   看一看使用的数据和差异文件中的已用空间[sys.dm_db_xtp_checkpoint_files &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-files-transact-sql)若要查看是否时它应不获取触发合并。  
  
## <a name="performing-a-manual-merge"></a>执行手动合并  
 你可以使用[sys.sp_xtp_merge_checkpoint_files &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-merge-checkpoint-files-transact-sql)执行手动合并。  
  
 使用以下查询检索有关数据和差异文件的信息，  
  
```tsql  
select checkpoint_file_id, file_type_desc, internal_storage_slot, file_size_in_bytes, file_size_used_in_bytes,   
inserted_row_count, deleted_row_count, lower_bound_tsn, upper_bound_tsn   
from sys.dm_db_xtp_checkpoint_files  
where state = 1  
order by file_type_desc, upper_bound_tsn  
```  
  
 假定你找到未合并的三个数据文件。 可使用第一个数据文件的 `lower_bound_tsn` 值和最后一个数据文件的 `upper_bound_tsn` 发出以下命令：  
  
```tsql  
exec sys.sp_xtp_merge_checkpoint_files 'H_DB',  12345, 67890  
```  
  
 假定三个数据和差异文件对的每一对都有 15836 行，并且其中删除了 5279 行。 合并后，新数据文件有 31872 行，未删除行。 新数据文件的大小可远远大于初始分配的 128MB 大小。 这是因为手动合并优先于合并策略，强制合并所请求的文件。  
  
 博客[状态转换的检查点文件中具有内存优化表的数据库](http://blogs.technet.com/b/dataplatforminsider/archive/2014/01/23/state-transition-of-checkpoint-files-in-databases-with-memory-optimized-tables.aspx)描述状态转换的开始从数据和差异文件对垃圾回收。  
  
## <a name="see-also"></a>请参阅  
 [创建和管理用于内存优化的对象的存储](../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  
