---
title: sys.dm_exec_describe_first_result_set_for_object (TRANSACT-SQL) |Microsoft 文档
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
- sys.dm_exec_describe_first_result_set_for_object_TSQL
- sys.dm_exec_describe_first_result_set_for_object
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_describe_first_result_set_for_object catalog view
ms.assetid: 63b0fde7-95d7-4ad7-a219-a9feacf1bd89
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 8ac774a29be46e7be925141cd10b8dd7150e5724
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2018
ms.locfileid: "34467753"
---
# <a name="sysdmexecdescribefirstresultsetforobject-transact-sql"></a>sys.dm_exec_describe_first_result_set_for_object (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  此动态管理函数采用@object_id作为参数，并描述具有该 ID 的模块的第一个结果元数据 @object_id指定可以是的 ID[!INCLUDE[tsql](../../includes/tsql-md.md)]存储过程或[!INCLUDE[tsql](../../includes/tsql-md.md)]触发器。 如果它是其他任何对象（如视图、表、函数或 CLR 过程）的 ID，则会在结果的错误列中指定错误。  
  
 **sys.dm_exec_describe_first_result_set_for_object**具有相同的结果集与定义[sys.dm_exec_describe_first_result_set &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-transact-sql.md) ，它类似于[sp_describe_first_result_set &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sys.dm_exec_describe_first_result_set_for_object   
    ( @object_id , @include_browse_information )  
```  
  
## <a name="arguments"></a>参数  
 *@object_id*  
 @object_id的[!INCLUDE[tsql](../../includes/tsql-md.md)]存储过程或[!INCLUDE[tsql](../../includes/tsql-md.md)]触发器。 @object_id 是类型**int**。  
  
 *@include_browse_information*  
 @include_browse_information 是类型**位**。 如果设置为 1，则分析每个查询，就好像它在查询中使用 FOR BROWSE 选项。 返回其他键列和源表信息。  
  
## <a name="table-returned"></a>返回的表  
 此公共元数据作为结果集返回，结果元数据中的每列对应于一行。 每一行以下面一节所说明的格式描述列的类型和为 Null 性。 如果对于每个控制路径不存在第一个语句，则返回的结果集不包含任何行。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**is_hidden**|**bit**|指定列是否是出于浏览信息的目的而额外添加的，并不会实际出现在结果集中。|  
|**column_ordinal**|**int**|在结果集中包含列的序号位置。 第一个列的位置将指定为 1。|  
|**名称**|**sysname**|包含列的名称（如果可以确定名称）。 否则为 NULL。|  
|**is_nullable**|**bit**|如果列允许 null 值，如果列不允许使用 Null，则为 0 和 1，如果无法确定列允许 Null，则包含值 1。|  
|**system_type_id**|**int**|包含 sys.types 中指定的列的数据类型的 system_type_id。 对于 CLR 类型，即使 system_type_name 列返回 NULL，该列也会返回值 240。|  
|**system_type_name**|**nvarchar(256)**|包含数据类型名称。 包含为列数据类型指定的参数（例如，length、precision、scale）。 如果数据类型是用户定义的别名类型，则会在此处指定基本系统类型。 如果数据类型是 CLR 用户定义类型，则在此列中返回 NULL。|  
|**max_length**|**int**|列的最大长度（字节）。<br /><br /> 为-1 = 的列数据类型为**varchar （max)**， **nvarchar (max)**， **varbinary （max)**，或**xml**。<br /><br /> 有关**文本**列， **max_length**值将为 16 或设置的值**sp_tableoption 'text in row**。|  
|**精度**|**tinyint**|如果为基于数值的列，则为该列的精度。 否则，返回 0。|  
|**小数位数**|**tinyint**|如果基于数值，则为列的小数位数。 否则，返回 0。|  
|**collation_name**|**sysname**|如果列包含的是字符，则为该列的排序规则的名称。 否则返回 NULL。|  
|**user_type_id**|**int**|对于 CLR 和别名类型，包含在 sys.types 中指定的列数据类型的 user_type_id。 否则为 NULL。|  
|**user_type_database**|**sysname**|对于 CLR 和别名类型，包含在其中定义相应类型的数据库的名称。 否则为 NULL。|  
|**user_type_schema**|**sysname**|对于 CLR 和别名类型，包含在其中定义相应类型的架构的名称。 否则为 NULL。|  
|**user_type_name**|**sysname**|对于 CLR 和别名类型，包含类型的名称。 否则为 NULL。|  
|**assembly_qualified_type_name**|**nvarchar(4000)**|对于 CLR 类型，返回定义类型的程序集和类的名称。 否则为 NULL。|  
|**xml_collection_id**|**int**|包含 sys.columns 中指定的列数据类型的 xml_collection_id。 如果返回的类型与 XML 架构集合不关联，则该列将返回 NULL。|  
|**xml_collection_database**|**sysname**|包含定义与此类型关联的 XML 架构集合的数据库。 如果返回的类型与 XML 架构集合不关联，则该列将返回 NULL。|  
|**xml_collection_schema**|**sysname**|包含定义与此类型关联的 XML 架构集合的架构。 如果返回的类型与 XML 架构集合不关联，则该列将返回 NULL。|  
|**xml_collection_name**|**sysname**|包含与此类型关联的 XML 架构集合的名称。 如果返回的类型与 XML 架构集合不关联，则该列将返回 NULL。|  
|**is_xml_document**|**bit**|如果返回的数据类型为 XML，并且保证该类型是完整的 XML 文档（包含根节点，与 XML 片段相对），则返回 1。 否则，返回 0。|  
|**is_case_sensitive**|**bit**|如果列为区分大小写的字符串类型，则返回 1；否则，返回 0。|  
|**is_fixed_length_clr_type**|**bit**|如果列为固定长度 CLR 类型，则返回 1；否则，返回 0。|  
|**source_server**|**sysname**|此结果中的此列返回的源服务器的名称（如果结果源自远程服务器）。 在 sys.servers 中所示，未提供名称。  如果列源自本地服务器或无法确定它派自的服务器，则返回 NULL。 仅在请求浏览信息填充。|  
|**source_database**|**sysname**|此结果中的列返回的源数据库的名称。 如果无法确定该数据库，则返回 NULL。 仅在请求浏览信息填充。|  
|**source_schema**|**sysname**|此结果中的列返回的源架构的名称。 如果无法确定该架构，则返回 NULL。 仅在请求浏览信息填充。|  
|**source_table**|**sysname**|此结果中的列返回的源表的名称。 如果无法确定该表，则返回 NULL。 仅在请求浏览信息填充。|  
|**source_column**|**sysname**|此结果中的列返回的源列的名称。 如果无法确定该列，则返回 NULL。 仅在请求浏览信息填充。|  
|**is_identity_column**|**bit**|如果列是标识列，则返回 1；否则，返回 0。 如果无法确定列是否为标识列，则返回 NULL。|  
|**is_part_of_unique_key**|**bit**|如果列是唯一索引的一部分（包括唯一和主要的约束），则返回 1；否则，返回 0。 如果无法确定列是否为唯一索引的一部分，则返回 NULL。 仅在请求浏览信息时填充它。|  
|**is_updateable**|**bit**|如果可以更新列，则返回 1；否则，返回 0。 如果无法确定是否可以更新列，则返回 NULL。|  
|**is_computed_column**|**bit**|如果列是计算列，则返回 1；否则，返回 0。 如果无法确定列是计算的列，返回 NULL。|  
|**is_sparse_column_set**|**bit**|如果列是稀疏列，则返回 1；否则，返回 0。 如果无法确定列是否为稀疏列集的一部分，则返回 NULL。|  
|**ordinal_in_order_by_list**|**int**|此列在 ORDER BY 列表中的位置：如果在 ORDER BY 列表中不显示该列或无法唯一确定 ORDER BY 列表，则返回 NULL。|  
|**order_by_list_length**|**int**|ORDER BY 列表的长度。 如果没有 ORDER BY 列表，或者无法唯一确定 ORDER BY 列表，则返回 NULL。 请注意，对于 sp_describe_first_result_set 返回的所有行，该值是相同的。|  
|**order_by_is_descending**|**smallint NULL**|如果 ordinal_in_order_by_list 不为 NULL， **order_by_is_descending**列报告此列的 ORDER BY 子句的方向。 否则，它报告 NULL。|  
|**error_number**|**int**|包含函数返回的错误号。 如果列中未发生错误，则包含 NULL。|  
|**error_severity**|**int**|包含函数返回的严重性。 如果列中未发生错误，则包含 NULL。|  
|**error_state**|**int**|包含函数返回的状态消息。 如果未发生错误， 则该列包含 NULL。|  
|**error_message**|**nvarchar(4096)**|包含函数返回的消息。 如果未发生错误，则该列包含 NULL。|  
|**error_type**|**int**|包含一个整数，它表示返回的错误。 映射到 error_type_desc。 请参阅“备注”中的列表。|  
|**error_type_desc**|**nvarchar(60)**|包含一个简短的大写字符串，它表示返回的错误。 映射到 error_type。 请参阅“备注”中的列表。|  
  
## <a name="remarks"></a>注释  
 此函数使用相同的算法为**sp_describe_first_result_set**。 有关详细信息，请参阅[sp_describe_first_result_set &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md)。  
  
 下表列出了错误类型及其说明。  
  
|错误类型|错误类型|Description|  
|-----------------|-----------------|-----------------|  
|1|MISC|未描述的所有错误。|  
|2|SYNTAX|在批处理中发生语法错误。|  
|3|CONFLICTING_RESULTS|由于两个可能的第一个语句之间发生冲突，无法确定结果。|  
|4|DYNAMIC_SQL|由于动态 SQL 可能会返回第一个结果，无法确定结果。|  
|5|CLR_PROCEDURE|由于 CLR 存储过程可能会返回第一个结果，无法确定结果。|  
|6|CLR_TRIGGER|由于 CLR 触发器可能会返回第一个结果，无法确定结果。|  
|7|EXTENDED_PROCEDURE|由于扩展存储过程可能会返回第一个结果，无法确定结果。|  
|8|UNDECLARED_PARAMETER|由于结果集的一个或多个列的数据类型可能取决于未声明的参数，无法确定结果。|  
|9|RECURSION|由于批处理包含递归语句，无法确定结果。|  
|10|TEMPORARY_TABLE|无法确定结果，因为批处理包含临时表和不受**sp_describe_first_result_set** 。|  
|11|UNSUPPORTED_STATEMENT|由于批处理包含不支持的语句，无法确定结果**sp_describe_first_result_set** (例如，FETCH、 REVERT 等。)。|  
|12|OBJECT_ID_NOT_SUPPORTED|@object_id传递给函数不是支持 （即不是存储的过程）|  
|13|OBJECT_ID_DOES_NOT_EXIST|@object_id传递到系统目录中找不到函数。|  
  
## <a name="permissions"></a>权限  
 需要有权执行@tsql自变量。  
  
## <a name="examples"></a>示例  
  
### <a name="a-returning-metadata-with-and-without-browse-information"></a>A. 返回包含和不含浏览信息的元数据  
 下面的示例创建名为 TestProc2 返回两个结果集的存储的过程。 然后该示例演示**sys.dm_exec_describe_first_result_set**返回第一个结果集在过程中，不含浏览信息与有关的信息。  
  
```  
CREATE PROC TestProc2  
AS  
SELECT object_id, name FROM sys.objects ;  
SELECT name, schema_id, create_date FROM sys.objects ;  
GO  
  
SELECT * FROM sys.dm_exec_describe_first_result_set_for_object(OBJECT_ID('TestProc2'), 0) ;  
SELECT * FROM sys.dm_exec_describe_first_result_set_for_object(OBJECT_ID('TestProc2'), 1) ;  
GO  
```  
  
### <a name="b-combining-the-sysdmexecdescribefirstresultsetforobject-function-and-a-table-or-view"></a>B. 结合使用 sys.dm_exec_describe_first_result_set_for_object 函数和表或视图  
 下面的示例使用这两个与 sys.procedures 系统目录视图和**sys.dm_exec_describe_first_result_set_for_object**函数来显示中的所有存储过程的结果集的元数据[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]数据库。  
  
```  
USE AdventureWorks2012;  
GO  
  
SELECT p.name, r.*   
FROM sys.procedures AS p  
CROSS APPLY sys.dm_exec_describe_first_result_set_for_object(p.object_id, 0) AS r;  
GO  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [sp_describe_first_result_set &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md)   
 [sp_describe_undeclared_parameters &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-describe-undeclared-parameters-transact-sql.md)   
 [sys.dm_exec_describe_first_result_set &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-transact-sql.md)  
  
  
