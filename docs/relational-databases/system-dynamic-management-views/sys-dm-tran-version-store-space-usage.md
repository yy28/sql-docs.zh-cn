---
title: "sys.dm_tran_version_store_space_usage (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 04/30/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_tran_version_store_space_usage_TSQL
- sys.dm_tran_version_store_space_usage
- dm_tran_version_store_space_usage
- dm_tran_version_store_space_usage_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.dm_tran_version_store_space_usage dynamic management view
ms.assetid: 7ab44517-0351-4f91-bdd9-7cf940f03c51
caps.latest.revision: "10"
author: savjani
ms.author: pariks
manager: ajayj
ms.workload: Inactive
ms.openlocfilehash: cfdd2caa03fdd12501580c2584d68f374ee54222
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/02/2018
---
# <a name="sysdmtranversionstorespaceusage-transact-sql"></a>sys.dm_tran_version_store_space_usage (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

返回一个表，版本存储记录用于每个数据库 tempdb 中显示总空间。 **sys.dm_tran_version_store_space_usage**高效，高性能来运行，因为它不会通过单个版本应用商店导航记录，并返回每个数据库 tempdb 中使用的聚合的版本存储空间。
  
每个有版本控制的记录均以二进制数据的形式与某些跟踪或状态信息存储在一起。 与数据库表中的记录相似，版本存储区记录存储在 8192 字节的页中。 如果记录超过 8192 字节，则该记录将拆分为两个不同的记录。  
  
由于有版本控制的记录以二进制数据的形式存储，因此不同的数据库可以采用不同的排序规则。 使用**sys.dm_tran_version_store_space_usage**为基于 SQL Server 实例中的数据库版本存储空间使用情况的监视和计划 tempdb 大小。
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|数据库的数据库 ID。|  
|**reserved_page_count**|**bigint**|保留版本 tempdb 中的页的总数存储的数据库记录。|  
|**reserved_space_kb**|**bigint**|用在 tempdb 中的千字节为单位的版本的总空间存储的数据库记录。|  
  
## <a name="permissions"></a>权限  
上[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`权限。   

## <a name="examples"></a>示例  
 以下查询可以用于确定在 tempdb 中使用的空间的每个数据库中的 SQL Server 实例的版本存储区。 
  
```sql  
SELECT 
  DB_NAME(database_id) as 'Database Name',
  reserved_page_count,
  reserved_space_kb 
FROM sys.dm_tran_version_store_space_usage;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Database Name            reserved_page_count reserved_space_kb  
------------------------ -------------------- -----------  
msdb                      0                    0             
AdventureWorks2016        10                   80             
AdventureWorks2016DW      0                    0             
WideWorldImporters        20                   160             
```
 
## <a name="see-also"></a>另请参阅  
 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [与事务相关的动态管理视图和函数 (Transact-SQL)](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
