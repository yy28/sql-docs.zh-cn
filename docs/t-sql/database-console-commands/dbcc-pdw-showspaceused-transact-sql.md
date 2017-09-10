---
title: "DBCC PDW_SHOWSPACEUSED (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/17/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.service: sql-data-warehouse
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 73f598cf-b02a-4dba-8d89-9fc0b55a12b8
caps.latest.revision: 10
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4a16d4a7a10eb4f36d0ead2a19f8e37d251e417f
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-pdwshowspaceused-transact-sql"></a>DBCC PDW_SHOWSPACEUSED (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

显示的行、 磁盘空间保留，以及用于特定的表，或用于中的所有表的磁盘空间数[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]数据库。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定 &#40;Transact SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
-- Show the space used for all user tables and system tables in the current database  
DBCC PDW_SHOWSPACEUSED  
[;]  
  
-- Show the space used for a table  
DBCC PDW_SHOWSPACEUSED ( " [ database_name . [ schema_name ] . ] | [ schema_name .] table_name  " )  
[;]  
```  
  
## <a name="arguments"></a>参数  
 [ *database_name* 。 [ *schema_name* ]。 | *schema_name* 。 ] *table_name*  
 一个、 两个，或要显示的表的由三部分名称。 对于两个或三部分的表名称，名称必须用双引号括起来 ("")。 使用一部分表名称周围的引号是可选的。 当指定未表名时，是当前数据库中显示的信息。  
  
## <a name="permissions"></a>Permissions  
需要 VIEW SERVER STATE 权限。
  
## <a name="result-sets"></a>结果集  
这是针对所有表的结果集。
  
|列|数据类型|Description|  
|------------|---------------|-----------------|  
|reserved_space|bigint|用于数据库，以 kb 为单位的总空间。|  
|data_space|bigint|用于数据，以 kb 为单位的空间。|  
|index_space|bigint|用于索引，以 kb 为单位的空间。|  
|unused_space|bigint|是保留的空间的一部分，未使用，以 kb 为单位的空间。|  
|pdw_node_id|int|正用于数据的计算节点。|  
  
这是针对一个表的结果集。
  
|列|数据类型|Description|范围|  
|------------|---------------|-----------------|-----------|  
|rows|bigint|行数。||  
|reserved_space|bigint|保留对象，以 kb 为单位的总空间。||  
|data_space|bigint|使用数据，以 kb 为单位的空间。||  
|index_space|bigint|用于索引，以 kb 为单位的空间。||  
|unused_space|bigint|是保留的空间的一部分，未使用，以 kb 为单位的空间。||  
|pdw_node_id|int|用于报告的空间使用情况的计算节点。||  
|distribution_id|int|用于报告的空间使用情况的分发。|值为-1 表示复制的表。|  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
### <a name="a-dbcc-pdwshowspaceused-basic-syntax"></a>A. DBCC PDW_SHOWSPACEUSED 基本语法  
下面的示例演示了多个方式显示的行数、 磁盘空间保留，并由 FactInternetSales 表已用磁盘空间[!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)]数据库。
  
```sql
-- Uses AdventureWorks  
  
DBCC PDW_SHOWSPACEUSED ( "AdventureWorksPDW2012.dbo.FactInternetSales" );  
DBCC PDW_SHOWSPACEUSED ( "AdventureWorksPDW2012..FactInternetSales" );  
DBCC PDW_SHOWSPACEUSED ( "dbo.FactInternetSales" );  
DBCC PDW_SHOWSPACEUSED ( FactInternetSales );  
```  
  
### <a name="b-show-the-disk-space-used-by-all-tables-in-the-current-database"></a>B. 显示当前数据库中的所有表都使用的磁盘空间  
 下面的示例演示保留和所有用户表和系统表中的都使用的磁盘空间[!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)]数据库。  
  
```sql
-- Uses AdventureWorks  
  
DBCC PDW_SHOWSPACEUSED;  
```  
 ## <a name="see-also"></a>另请参阅
[DBCC PDW_SHOWEXECUTIONPLAN &#40;Transact SQL &#41;](dbcc-pdw-showexecutionplan-transact-sql.md)  
[DBCC PDW_SHOWPARTITIONSTATS &#40;Transact SQL &#41;](dbcc-pdw-showpartitionstats-transact-sql.md)

  

