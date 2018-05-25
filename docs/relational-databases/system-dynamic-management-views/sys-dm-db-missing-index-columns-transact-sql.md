---
title: sys.dm_db_missing_index_columns (Transact SQL) |Microsoft 文档
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
- dm_db_missing_index_columns_TSQL
- sys.dm_db_missing_index_columns_TSQL
- sys.dm_db_missing_index_columns
- dm_db_missing_index_columns
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_missing_index_columns dynamic management function
- missing indexes feature [SQL Server], sys.dm_db_missing_index_columns dynamic management function
ms.assetid: 3b24e5ed-0c79-47e5-805c-a0902d0aeb86
caps.latest.revision: 40
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: c457cd76f0c1090147d2df41a47c4c6f3c2ef5ad
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2018
---
# <a name="sysdmdbmissingindexcolumns-transact-sql"></a>sys.dm_db_missing_index_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回与缺少索引（不包括空间索引）的数据库表列有关的信息。 **sys.dm_db_missing_index_columns**是动态管理函数。  

## <a name="syntax"></a>语法  
  
```  
  
sys.dm_db_missing_index_columns(index_handle)  
```  
  
## <a name="arguments"></a>参数  
 *index_handle*  
 唯一地标识缺失索引的整数。 它可以从下列动态管理对象中获得：  
  
 [sys.dm_db_missing_index_details &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md)  
  
 [sys.dm_db_missing_index_groups &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-groups-transact-sql.md)  
  
## <a name="table-returned"></a>返回的表  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**column_id**|**int**|列的 ID。|  
|column_name|**sysname**|表列的名称。|  
|**column_usage**|**varchar(20)**|查询使用列的方式。 可能的值以及及其说明是：<br /><br /> 相等性： 列分配给一个谓词，表示相等的窗体： <br />                        *table.column* = *constant_value*<br /><br /> 是否不相等： 列分配给一个谓词，例如，表示不相等，形式的谓词： *table.column* > *constant_value*。 “=”之外的任何比较运算符都表示不相等。<br /><br /> 包括： 列不用于谓词赋值，但用于另一个原因，例如，包含一个查询。|  
  
## <a name="remarks"></a>注释  
 返回的信息**sys.dm_db_missing_index_columns**时查询查询优化器优化，而且不具有持久性，会更新。 缺失索引信息只保留到重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 前。 如果数据库管理员要在服务器回收后保留缺失索引信息，则应定期制作缺失索引信息的备份副本。  
  
## <a name="transaction-consistency"></a>事务一致性  
 如果事务创建或删除了一个表，则包含有关已删除对象的缺失索引信息的行将从此动态管理对象中删除，以保持事务一致性。  
  
## <a name="permissions"></a>权限  
 必须授予用户 VIEW SERVER STATE 权限或任何隐含 VIEW SERVER STATE 权限的权限，以便查询此动态管理函数。  
  
## <a name="examples"></a>示例  
 以下示例对 `Address` 表运行查询，然后使用 `sys.dm_db_missing_index_columns` 动态管理视图运行查询以返回缺失索引的表列。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT City, StateProvinceID, PostalCode  
FROM Person.Address  
WHERE StateProvinceID = 9;  
GO  
SELECT mig.*, statement AS table_name,  
    column_id, column_name, column_usage  
FROM sys.dm_db_missing_index_details AS mid  
CROSS APPLY sys.dm_db_missing_index_columns (mid.index_handle)  
INNER JOIN sys.dm_db_missing_index_groups AS mig ON mig.index_handle = mid.index_handle  
ORDER BY mig.index_group_handle, mig.index_handle, column_id;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [sys.dm_db_missing_index_details &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md)   
 [sys.dm_db_missing_index_groups &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-groups-transact-sql.md)   
 [sys.dm_db_missing_index_group_stats &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-group-stats-transact-sql.md)  
  
  
