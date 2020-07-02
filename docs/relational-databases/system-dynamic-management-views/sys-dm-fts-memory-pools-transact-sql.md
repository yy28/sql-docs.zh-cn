---
title: sys. dm_fts_memory_pools （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_fts_memory_pools_TSQL
- sys.dm_fts_memory_pools_TSQL
- sys.dm_fts_memory_pools
- dm_fts_memory_pools
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_fts_memory_pools dynamic management view
ms.assetid: 24747239-cd78-4d55-a00a-19233a457f42
author: pmasl
ms.author: pelopes
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0f14acaaf8e4f92a603270619c181e9d97108c5d
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85734520"
---
# <a name="sysdm_fts_memory_pools-transact-sql"></a>sys.dm_fts_memory_pools (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  返回有关可供全文爬网或全文爬网范围的全文收集器组件使用的共享内存池的信息。  
   
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**pool_id**|**int**|已分配的内存池的 ID。<br /><br /> 0 = 小型缓冲区<br /><br /> 1 = 大型缓冲区|  
|**buffer_size**|**int**|内存池中每个已分配的缓冲区的大小。|  
|**min_buffer_limit**|**int**|内存池中允许的最小缓冲区数。|  
|**max_buffer_limit**|**int**|内存池中允许的最大缓冲区数。|  
|**buffer_count**|**int**|内存池中共享内存缓冲区的当前个数。|  
  
## <a name="permissions"></a>权限  

在上 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] ，需要 `VIEW SERVER STATE` 权限。   
在 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 高级层上，需要具有 `VIEW DATABASE STATE` 数据库中的权限。 在 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 标准层和基本层上，需要**服务器管理员**或**Azure Active Directory 管理员**帐户。   
 
## <a name="physical-joins"></a>物理联接  
 ![此动态管理视图的重要联接](../../relational-databases/system-dynamic-management-views/media/join-dm-fts-memory-pools-1.gif "此动态管理视图的重要联接")  
  
## <a name="relationship-cardinalities"></a>关系基数  
  
|From|功能|关系|  
|----------|--------|------------------|  
|dm_fts_memory_buffers.pool_id|dm_fts_memory_pools.pool_id|多对一|  
  
## <a name="examples"></a>示例  
 以下示例返回 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 进程的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 全文收集器组件所拥有的总共享内存。  
  
```  
SELECT SUM(buffer_size * buffer_count) AS "total memory"   
    FROM sys.dm_fts_memory_pools;  
```  
  
## <a name="see-also"></a>另请参阅  
 [全文搜索和语义搜索动态管理视图和函数 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)  
  
  
