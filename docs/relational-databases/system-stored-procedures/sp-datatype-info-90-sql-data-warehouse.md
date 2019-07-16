---
title: sp_datatype_info_90 （SQL 数据仓库） |Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.service: sql-data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 1d043964-dc6e-4c3e-ab61-bc444d5e25ae
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 7919dac422a0033d9bac02a928da2ff7445c6cc9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68108324"
---
# <a name="spdatatypeinfo90-sql-data-warehouse"></a>sp_datatype_info_90 （SQL 数据仓库）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  返回有关当前环境所支持的数据类型的信息。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [Transact-SQL 语法约定 (Transact-SQL)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_datatype_info_90 [ [ @data_type = ] data_type ]   
     [ , [ @ODBCVer = ] odbc_version ]   
```  
  
## <a name="arguments"></a>参数  
`[ @data_type = ] data_type` 是指定的数据类型的代码号。 若要获得所有数据类型的列表，请省略此参数。 *data_type*是**int**，默认值为 0。  
  
`[ @ODBCVer = ] odbc_version` 是使用的 ODBC 版本。 *odbc_version*是**tinyint**，默认值为 2。  
  
## <a name="return-code-values"></a>返回代码值  
 无  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|TYPE_NAME|**sysname**|与 DBMS 相关的数据类型。|  
|DATA_TYPE|**smallint**|此类型的所有列所映射到的 ODBC 类型代码。|  
|PRECISION|**int**|数据源中数据类型的最大精度。 数据类型的精度不适用时返回 NULL。 PRECISION 列的返回值以 10 为基数。|  
|LITERAL_PREFIX|**varchar(** 32 **)**|常量前使用的一个或多个字符。 例如，一个单引号 (  ) 的字符类型和二进制文件的 0x。|  
|LITERAL_SUFFIX|**varchar(** 32 **)**|字符或字符用于终止常量的一个。 例如，一个单引号 (  ) 的字符类型和二进制文件没有引号。|  
|CREATE_PARAMS|**varchar(** 32 **)**|此数据类型的创建参数的说明。 例如，**十进制**是"precision，scale"， **float**为 NULL，并且**varchar**为"max_length"。|  
|NULLABLE|**smallint**|指定为 Null 性。<br /><br /> 1 = 允许 Null 值。<br /><br /> 0 = 不允许 Null 值。|  
|CASE_SENSITIVE|**smallint**|指定是否区分大小写。<br /><br /> 1 = 此类型的所有列都区分大小写（用于排序规则）。<br /><br /> 0 = 此类型的所有列都不区分大小写。|  
|SEARCHABLE|**smallint**|指定列类型的搜索能力：<br /><br /> 1 = 不能搜索。<br /><br /> 2 = 可以使用 LIKE 进行搜索。<br /><br /> 3 = 可以使用 WHERE 进行搜索。<br /><br /> 4 = 可以使用 WHERE 或 LIKE 进行搜索。|  
|UNSIGNED_ATTRIBUTE|**smallint**|指定数据类型的符号。<br /><br /> 1 = 数据类型没有符号。<br /><br /> 0 = 数据类型有符号。|  
|MONEY|**smallint**|指定**资金**数据类型。<br /><br /> 1 =**资金**数据类型。<br /><br /> 0 = 未**资金**数据类型。|  
|AUTO_INCREMENT|**smallint**|指定自动递增。<br /><br /> 1 = 自动递增。<br /><br /> 0 = 不自动递增。<br /><br /> NULL = 属性不适用。<br /><br /> 应用程序可以将值插入具有此属性的列中，但应用程序不能更新列中的值。 除**位**数据类型，AUTO_INCREMENT 是仅对属于精确数字和近似数字数据类型类别的数据类型有效。|  
|LOCAL_TYPE_NAME|**sysname**|与数据源相关的数据类型名称的本地化版本。 例如，DECIMAL 的法语版本是 DECIMALE。 如果是数据源不支持的本地化名称，则返回 NULL。|  
|MINIMUM_SCALE|**smallint**|数据源中数据类型的最小小数位数。 如果数据类型的小数位数是固定的，则 MINIMUM_SCALE 和 MAXIMUM_SCALE 列将同时包含此值。 当小数位数不适用时，将返回 NULL。|  
|MAXIMUM_SCALE|**smallint**|数据源中数据类型的最大小数位数。 如果在数据源中没有单独定义最大小数位数，而是将其定义为与最大精度相同，则此列的值与 PRECISION 列的值相同。|  
|SQL_DATA_TYPE|**smallint**|SQL 数据类型在描述符的 TYPE 字段中显示的值。 此列是与 DATA_TYPE 列相同除外**datetime**和 ANSI**间隔**数据类型。 此字段始终返回值。|  
|SQL_DATETIME_SUB|**smallint**|**日期时间**或 ANSI**间隔**如果 SQL_DATA_TYPE 的值为 SQL_DATETIME 或 SQL_INTERVAL 子代码。 对于数据类型以外**datetime**和 ANSI**间隔**，此字段为 NULL。|  
|NUM_PREC_RADIX|**int**|数的计算列所能容纳的最大数目位数或数字。 如果数据类型是近似数字数据类型，则此列包含的值为 2，以指示几个位。 对于精确数字类型，此列包含的值为 10，以指示几个十进制数字。 否则，此列为 NULL。 通过将精度和基数相结合，应用程序可以计算出列所能容纳的最大数。|  
|INTERVAL_PRECISION|**smallint**|间隔起始精度，如果的值*data_type*是**间隔**; 否则为 NULL。|  
|USERTYPE|**smallint**|**usertype**来自 systypes 表的值。|  
  
## <a name="remarks"></a>备注  
 sp_datatype_info 等价于 ODBC 中的 SQLGetTypeInfo。 返回的结果按 DATA_TYPE 排序，再按数据类型映射到相应 ODBC SQL 数据类型的紧密程度进行排序。  
  
## <a name="permissions"></a>权限  
 要求具有 public 角色的成员身份。  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 下面的示例检索有关的信息**sysname**并**nvarchar**通过指定的数据类型*data_type*的值`-9`。  
  
```  
USE master;  
GO  
EXEC sp_datatype_info_90 -9;  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [SQL 数据仓库存储的过程](../../relational-databases/system-stored-procedures/sql-data-warehouse-stored-procedures.md)   
 [数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)  
  
  

