---
title: "ALTER 分区方案 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER PARTITION SCHEME
- ALTER_PARTITION_SCHEME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER PARTITION SCHEME statement
- partition schemes [SQL Server], modifying
- modifying partition schemes
- adding filegroups
- NEXT USED filegroups
ms.assetid: f01d6880-9800-4cfb-8d11-d4be21efc8ca
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 545fe3da48f0d0c98d72b32e5a82d9fd55579d00
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="alter-partition-scheme-transact-sql"></a>ALTER PARTITION SCHEME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  向分区方案中添加文件组或更改分区方案中 NEXT USED 文件组的指定。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
ALTER PARTITION SCHEME partition_scheme_name   
NEXT USED [ filegroup_name ] [ ; ]  
```  
  
## <a name="arguments"></a>参数  
 *partition_scheme_name*  
 是要更改的分区方案的名称。  
  
 *filegroup_name*  
 指定要由分区方案标记为 NEXT USED 的文件组。 这意味着该文件组将接受通过创建一个新分区[ALTER PARTITION FUNCTION](../../t-sql/statements/alter-partition-function-transact-sql.md)语句。  
  
 在一个分区方案中，只能将一个文件组指定为 NEXT USED。 可以指定非空文件组。 如果*filegroup_name*指定和当前没有任何文件组标记为下一步使用*filegroup_name*标记下一步使用。 如果*filegroup_name*指定，并且具有 NEXT USED 属性的文件组已存在，则 NEXT USED 属性将从现有的文件组到传输*filegroup_name*。  
  
 如果*filegroup_name*未指定并且具有 NEXT USED 属性的文件组已存在，则该文件组将失去其下一步使用状态，以便在任何 NEXT USED 文件组*partition_scheme_name*.  
  
 如果*filegroup_name*未指定，并且有任何文件组标记下一步使用，ALTER PARTITION SCHEME 返回一条警告。  
  
## <a name="remarks"></a>注释  
 受 ALTER PARTITION SCHEME 影响的所有文件组都必须处于联机状态。  
  
## <a name="permissions"></a>Permissions  
 用于执行 ALTER PARTITION SCHEME Tthe 以下权限：  
  
-   ALTER ANY DATASPACE 权限。 默认情况下，此权限授予 **sysadmin** 固定服务器角色和 **db_owner** 及 **db_ddladmin** 固定数据库角色的成员。  
  
-   对创建分区方案时所在数据库的 CONTROL 或 ALTER 权限。  
  
-   对承载了创建分区方案时所在数据库的服务器的 CONTROL SERVER 或 ALTER ANY DATABASE 权限。  
  
## <a name="examples"></a>示例  
 以下示例假设当前数据库中已存在分区方案 `MyRangePS1` 和文件组 `test5fg`。  
  
```  
ALTER PARTITION SCHEME MyRangePS1  
NEXT USED test5fg;  
```  
  
 作为 ALTER PARTITION FUNCTION 语句的结果，文件组 `test5fg` 将接收已分区表或索引的所有其他分区。  
  
## <a name="see-also"></a>另请参阅  
 [CREATE PARTITION SCHEME (Transact-SQL)](../../t-sql/statements/create-partition-scheme-transact-sql.md)   
 [删除分区方案 &#40;Transact SQL &#41;](../../t-sql/statements/drop-partition-scheme-transact-sql.md)   
 [CREATE PARTITION FUNCTION (Transact-SQL)](../../t-sql/statements/create-partition-function-transact-sql.md)   
 [ALTER PARTITION FUNCTION &#40;Transact SQL &#41;](../../t-sql/statements/alter-partition-function-transact-sql.md)   
 [删除分区函数 &#40;Transact SQL &#41;](../../t-sql/statements/drop-partition-function-transact-sql.md)   
 [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)   
 [CREATE INDEX (Transact-SQL)](../../t-sql/statements/create-index-transact-sql.md)   
 [EVENTDATA (Transact-SQL)](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.partition_schemes &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-partition-schemes-transact-sql.md)   
 [sys.data_spaces &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)   
 [sys.destination_data_spaces &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-destination-data-spaces-transact-sql.md)   
 [sys.partitions &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)   
 [sys.tables (Transact-SQL)](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)   
 [sys.indexes (Transact-SQL)](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns (Transact-SQL)](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)  
  
  

