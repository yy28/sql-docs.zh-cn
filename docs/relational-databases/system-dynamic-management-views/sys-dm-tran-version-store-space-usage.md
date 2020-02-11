---
title: sys. dm_tran_version_store_space_usage （Transact-sql） |Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68262664"
---
# <a name="sysdm_tran_version_store_space_usage-transact-sql"></a>sys. dm_tran_version_store_space_usage （Transact-sql）
[!INCLUDE[tsql-appliesto-2016sp2-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-2016sp2-asdb-xxxx-xxx-md.md)]

返回一个表，该表显示每个数据库的版本存储记录使用的 tempdb 中的总空间。 **sys. dm_tran_version_store_space_usage**是高效的，运行效率不高，因为它不在各个版本存储记录之间导航，并返回每个数据库的 tempdb 中使用的聚合版本存储空间。
  
每个版本控制的记录均存储为二进制数据，以及某些跟踪或状态信息。 与数据库表中的记录相似，版本存储区记录存储在 8192 字节的页中。 如果记录超过 8192 字节，则该记录将拆分为两个不同的记录。  
  
由于有版本控制的记录以二进制数据的形式存储，因此不同的数据库可以采用不同的排序规则。 使用**dm_tran_version_store_space_usage**可以基于 SQL Server 实例中数据库的版本存储空间使用情况监视和计划 tempdb 大小。
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|database_id |**int**|数据库的数据库 ID。|  
|**reserved_page_count**|**bigint**|数据库的版本存储记录在 tempdb 中保留的总页数。|  
|**reserved_space_kb**|**bigint**|数据库的版本存储记录在 tempdb 中使用的总空间（kb）。|  
  
## <a name="permissions"></a>权限  
在[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]上， `VIEW SERVER STATE`需要权限。   

## <a name="examples"></a>示例  
下面的查询可用于通过[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例中每个数据库的版本存储来确定 tempdb 中使用的空间。 
  
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
  
