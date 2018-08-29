---
title: sys.dm_db_missing_index_groups (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_db_missing_index_groups
- sys.dm_db_missing_index_groups_TSQL
- dm_db_missing_index_groups
- dm_db_missing_index_groups_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_missing_index_groups dynamic management view
- missing indexes feature [SQL Server], sys.dm_db_missing_index_groups dynamic management view
ms.assetid: 9cc00acd-d83d-49f8-be72-5b2aebed246b
caps.latest.revision: 39
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a6bb53e0f67c6db6f9ca0e5f6260812abfdac4c1
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43066819"
---
# <a name="sysdmdbmissingindexgroups-transact-sql"></a>sys.dm_db_missing_index_groups (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  此 DMV 返回有关特定索引组中除空间索引中缺少的索引的信息。 
  
 在 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 中，动态管理视图不能公开将影响数据库包含的信息，也不能公开有关用户可以访问的其他数据库的信息。 要避免公开此类信息，需要将包含不属于已连接租户的数据的每一行都筛选掉。  
   
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**index_group_handle**|**int**|标识缺失索引组。|  
|**index_handle**|**int**|标识缺失索引所属由指定的组**index_group_handle**。<br /><br /> 一个索引组仅包含一个索引。|  
  
## <a name="remarks"></a>Remarks  
 返回的信息**sys.dm_db_missing_index_groups**时更新查询优化查询优化器，因而不会持久保留。 缺失索引信息只保留到重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 前。 如果数据库管理员要在服务器回收后保留缺失索引信息，则应定期制作缺失索引信息的备份副本。  
  
 输出结果集中的任一列都不是一个键，但是它们结合在一起将形成一个索引键。  

  >[!NOTE]
  >针对此 DMV 的结果集被限制为 600 的行。 每一行都包含一个缺失的索引。 如果有多个缺失索引的 600，应该解决现有的缺失索引，以便您然后可以查看较新的。
  
## <a name="permissions"></a>Permissions  
 若要查询此动态管理视图，必须授予用户 VIEW SERVER STATE 权限或隐含 VIEW SERVER STATE 权限的任何权限。  
  
## <a name="see-also"></a>请参阅  
 [sys.dm_db_missing_index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-columns-transact-sql.md)   
 [sys.dm_db_missing_index_details &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md)   
 [sys.dm_db_missing_index_group_stats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-group-stats-transact-sql.md)  
  
  
