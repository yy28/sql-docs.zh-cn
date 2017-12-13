---
title: "创建分区方案 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 04/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE PARTITION SCHEME
- SCHEME
- PARTITION SCHEME
- CREATE_PARTITION_SCHEME_TSQL
- SCHEME_TSQL
- PARTITION_SCHEME_TSQL
dev_langs: TSQL
helpviewer_keywords:
- partitioned indexes [SQL Server], schemes
- partitioned tables [SQL Server], schemes
- CREATE PARTITION SCHEME statement
- partition schemes [SQL Server], creating
- filegroups [SQL Server], partitions
- partitioned indexes [SQL Server], filegroups
- partitioned tables [SQL Server], filegroups
- mapping partitions [SQL Server]
ms.assetid: 5b21c53a-b4f4-4988-89a2-801f512126e4
caps.latest.revision: "39"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 98abb06746c88d7876505033f5b209c30812fc5d
ms.sourcegitcommit: 721ad1cbc10e8147c087ae36b36296d72cbb0de8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2017
---
# <a name="create-partition-scheme-transact-sql"></a>CREATE PARTITION SCHEME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  在当前数据库中创建一个将已分区表或已分区索引的分区映射到文件组的方案。 已分区表或已分区索引的分区的个数和域在分区函数中确定。 首先必须在中创建分区函数[CREATE PARTITION FUNCTION](../../t-sql/statements/create-partition-function-transact-sql.md)的语句才能创建分区方案。  

>[!NOTE]
>在 Azure SQL 数据库支持仅对主文件组。  

 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
CREATE PARTITION SCHEME partition_scheme_name  
AS PARTITION partition_function_name  
[ ALL ] TO ( { file_group_name | [ PRIMARY ] } [ ,...n ] )  
[ ; ]  
```  
  
## <a name="arguments"></a>参数  
 *partition_scheme_name*  
 分区方案的名称。 分区方案名称必须在数据库中是唯一且符合的规则[标识符](../../relational-databases/databases/database-identifiers.md)。  
  
 *partition_function_name*  
 使用分区方案的分区函数的名称。 分区函数所创建的分区将映射到在分区方案中指定的文件组。 *partition_function_name*必须已存在于数据库。 单个分区不能同时包含 FILESTREAM 和非 FILESTREAM 文件组。  
  
 ALL  
 指定所有分区都映射到文件组中提供*file_group_name*，或主文件组到如果**[**主**]**指定。 如果指定 ALL，则只有一个*file_group_name*可以指定。  
  
 *file_group_name* | **[**主**]** [ **，***...n*]  
 指定要保存指定的分区的文件组的名称*partition_function_name*。 *file_group_name*必须已存在于数据库。  
  
 如果**[**主**]**分区存储在主文件组上的指定。 如果指定 ALL，则只有一个*file_group_name*可以指定。 分区分配给文件组，从在其中文件组中列出的顺序中的分区 1，[**，***...n*]。 相同*file_group_name*可以指定多个时间 [**，***...n*]。 如果 *n* 不足以容纳在指定的分区数*partition_function_name*，CREATE PARTITION SCHEME 失败并出现错误。  
  
 如果*partition_function_name*生成小于分区比文件组下, 一步使用标记的第一个未分配的文件组和信息消息显示命名 NEXT USED 文件组。 如果指定 ALL，则唯一*file_group_name*此维护其 NEXT USED 属性*partition_function_name*。 如果在 ALTER PARTITION FUNCTION 语句中创建了一个分区，则 NEXT USED 文件组将再接收一个分区。 若要再创建一个未分配的文件组来拥有新的分区，请使用 ALTER PARTITION SCHEME。  
  
 当指定主文件组中的*file_group_name* [1**，***...n*]，主必须进行分隔，如**[**主**]**，因为它是一个关键字。  
  
 对于 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]，只支持 PRIMARY。 请参阅示例 E 下面。 
  
## <a name="permissions"></a>Permissions  
 可以使用下列权限执行 CREATE PARTITION SCHEME：  
  
-   ALTER ANY DATASPACE 权限。 默认情况下，此权限授予 **sysadmin** 固定服务器角色和 **db_owner** 及 **db_ddladmin** 固定数据库角色的成员。  
  
-   对要在其中创建分区方案的数据库具有 CONTROL 或 ALTER 权限。  
  
-   对要在其中创建分区方案的数据库所在服务器具有 CONTROL SERVER 或 ALTER ANY DATABASE 权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-creating-a-partition-scheme-that-maps-each-partition-to-a-different-filegroup"></a>A. 创建用于将每个分区映射到不同文件组的分区方案  
 以下示例创建一个分区函数，将表或索引分为四个分区。 然后创建一个分区方案，在其中指定拥有这四个分区中每一个分区的文件组。 此示例假定数据库中已经存在文件组。  
  
```  
CREATE PARTITION FUNCTION myRangePF1 (int)  
AS RANGE LEFT FOR VALUES (1, 100, 1000);  
GO  
CREATE PARTITION SCHEME myRangePS1  
AS PARTITION myRangePF1  
TO (test1fg, test2fg, test3fg, test4fg);  
```  
  
 使用分区函数的表的分区`myRangePF1`上分区依据列**col1**下表中所示，将分配。  
  
||||||  
|-|-|-|-|-|  
|**文件组**|`test1fg`|`test2fg`|`test3fg`|`test4fg`|  
|**分区**|1|2|3|4|  
|**值**|**col1** <= `1`|**col1**  >  `1` AND **col1** <= `100`|**col1**  >  `100` AND **col1** <= `1000`|**col1** > `1000`|  
  
### <a name="b-creating-a-partition-scheme-that-maps-multiple-partitions-to-the-same-filegroup"></a>B. 创建将多个分区映射到同一个文件组的分区方案  
 如果所有分区都映射到同一个文件组，则使用 ALL 关键字。 但是，如果是多个（但不是全部）分区映射到同一个文件组，则文件组名称必须进行重复，如以下示例所示。  
  
```  
CREATE PARTITION FUNCTION myRangePF2 (int)  
AS RANGE LEFT FOR VALUES (1, 100, 1000);  
GO  
CREATE PARTITION SCHEME myRangePS2  
AS PARTITION myRangePF2  
TO ( test1fg, test1fg, test1fg, test2fg );  
```  
  
 使用分区函数的表的分区`myRangePF2`上分区依据列**col1**下表中所示，将分配。  
  
||||||  
|-|-|-|-|-|  
|**文件组**|`test1fg`|`test1fg`|`test1fg`|`test2fg`|  
|**分区**|1|2|3|4|  
|**值**|**col1** <= `1`|**col1** > 1 AND **col1** <= `100`|**col1**  >  `100` AND **col1** <= `1000`|**col1** > `1000`|  
  
### <a name="c-creating-a-partition-scheme-that-maps-all-partitions-to-the-same-filegroup"></a>C. 创建将所有分区映射到同一个文件组的分区方案  
 以下示例创建的分区函数与前面的示例相同，并且创建一个将所有分区映射到同一个文件组的分区方案。  
  
```  
CREATE PARTITION FUNCTION myRangePF3 (int)  
AS RANGE LEFT FOR VALUES (1, 100, 1000);  
GO  
CREATE PARTITION SCHEME myRangePS3  
AS PARTITION myRangePF3  
ALL TO ( test1fg );  
```  
  
### <a name="d-creating-a-partition-scheme-that-specifies-a-next-used-filegroup"></a>D. 创建指定“NEXT USED”文件组的分区方案  
 以下示例创建的分区函数与前面的示例相同，并且所创建的分区方案列出的文件组数超过了关联的分区函数所创建的分区数。  
  
```  
CREATE PARTITION FUNCTION myRangePF4 (int)  
AS RANGE LEFT FOR VALUES (1, 100, 1000);  
GO  
CREATE PARTITION SCHEME myRangePS4  
AS PARTITION myRangePF4  
TO (test1fg, test2fg, test3fg, test4fg, test5fg)  
```  
  
 执行语句将返回以下消息。  
  
已成功创建分区方案 myRangePS4。 test5fg 被标记为在分区方案 myRangePS4 下一步使用的文件组。  
  
  
 如果将分区函数 `myRangePF4` 更改为添加一个分区，则文件组 `test5fg` 将接收到新创建的分区。  

### <a name="e-creating-a-partition-schema-only-on-primary---only-primary-is-supported-for-includesqldbesaincludessqldbesa-mdmd"></a>E. 分区架构仅在主-只有主都支持创建[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]

 以下示例创建一个分区函数，将表或索引分为四个分区。 然后创建指定主文件组中创建的所有分区的分区方案。  
  
```  
CREATE PARTITION FUNCTION myRangePF1 (int)  
AS RANGE LEFT FOR VALUES (1, 100, 1000);  
GO  
CREATE PARTITION SCHEME myRangePS1  
AS PARTITION myRangePF1  
ALL TO ( [PRIMARY] );  
```
   
## <a name="see-also"></a>另请参阅  
 [CREATE PARTITION FUNCTION (Transact-SQL)](../../t-sql/statements/create-partition-function-transact-sql.md)   
 [ALTER 分区方案 &#40;Transact SQL &#41;](../../t-sql/statements/alter-partition-scheme-transact-sql.md)   
 [删除分区方案 &#40;Transact SQL &#41;](../../t-sql/statements/drop-partition-scheme-transact-sql.md)   
 [EVENTDATA (Transact-SQL)](../../t-sql/functions/eventdata-transact-sql.md)   
 [创建已分区的表和索引](../../relational-databases/partitions/create-partitioned-tables-and-indexes.md)   
 [sys.partition_schemes &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-partition-schemes-transact-sql.md)   
 [sys.data_spaces &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)   
 [sys.destination_data_spaces &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-destination-data-spaces-transact-sql.md)   
 [sys.partitions &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)   
 [sys.tables (Transact-SQL)](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)   
 [sys.indexes (Transact-SQL)](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns (Transact-SQL)](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)  
  
  
