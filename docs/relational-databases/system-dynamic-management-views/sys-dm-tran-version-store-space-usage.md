---
title: sys.dm_tran_version_store_space_usage (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 04/24/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_tran_version_store_space_usage_TSQL
- sys.dm_tran_version_store_space_usage
- dm_tran_version_store_space_usage
- dm_tran_version_store_space_usage_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_version_store_space_usage dynamic management view
ms.assetid: 7ab44517-0351-4f91-bdd9-7cf940f03c51
author: savjani
ms.author: pariks
manager: ajayj
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2a4fac732f784a401206f37fb2af9d3d8e0688ba
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2019
ms.locfileid: "68262664"
---
# <a name="sysdmtranversionstorespaceusage-transact-sql"></a>sys.dm_tran_version_store_space_usage (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-2016sp2-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-2016sp2-asdb-xxxx-xxx-md.md)]

返回一个表，显示使用的版本存储记录为每个数据库 tempdb 中总空间。 **sys.dm_tran_version_store_space_usage**高效且不昂贵而无法运行，不会浏览单个版本存储记录，并返回聚合每个数据库 tempdb 中使用的版本存储空间。
  
每个版本控制的记录存储为二进制数据，以及某些跟踪或状态信息。 与数据库表中的记录相似，版本存储区记录存储在 8192 字节的页中。 如果记录超过 8192 字节，则该记录将拆分为两个不同的记录。  
  
由于有版本控制的记录以二进制数据的形式存储，因此不同的数据库可以采用不同的排序规则。 使用**sys.dm_tran_version_store_space_usage**为基于 SQL Server 实例中的数据库版本存储空间使用情况的监视和规划 tempdb 大小。
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|数据库的数据库 ID。|  
|**reserved_page_count**|**bigint**|有关版本的 tempdb 中保留的页的总计数将存储的数据库记录。|  
|**reserved_space_kb**|**bigint**|用在 tempdb 中的千字节为单位的版本的总空间存储的数据库记录。|  
  
## <a name="permissions"></a>权限  
上[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`权限。   

## <a name="examples"></a>示例  
下面的查询可用于确定占用 tempdb 中空间中的每个数据库的版本存储区[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例。 
  
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
 
## <a name="see-also"></a>请参阅  
 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [与事务相关的动态管理视图和函数 (Transact-SQL)](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
