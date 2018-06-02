---
title: sp_datatype_info (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 05/25/2018
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_datatype_info_TSQL
- sp_datatype_info
dev_langs:
- TSQL
helpviewer_keywords:
- sp_datatype_info
ms.assetid: 045f3b5d-6bb7-4748-8b4c-8deb4bc44147
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 187b7969d46b6ab0a85779d108a66cbe8ae2d62b
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/02/2018
ms.locfileid: "34553747"
---
# <a name="spdatatypeinfo-transact-sql"></a>sp_datatype_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-xxx-md.md)]

  返回有关当前环境所支持的数据类型的信息。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_datatype_info [ [ @data_type = ] data_type ]   
     [ , [ @ODBCVer = ] odbc_version ]   
```  
  
## <a name="arguments"></a>参数  
 [ **@data_type=** ] *data_type*  
 所指定的数据类型的代码号。 若要获得所有数据类型的列表，请省略此参数。 *data_type*是**int**，默认值为 0。  
  
 [ **@ODBCVer=** ] *odbc_version*  
 所使用的 ODBC 的版本。 *odbc_version*是**tinyint**，默认值为 2。  
  
## <a name="return-code-values"></a>返回代码值  
 InclusionThresholdSetting  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|TYPE_NAME|**sysname**|与 DBMS 相关的数据类型。|  
|DATA_TYPE|**int**|此类型的所有列所映射到的 ODBC 类型代码。|  
|PRECISION|**int**|数据源中数据类型的最大精度。 数据类型的精度不适用时返回 NULL。 PRECISION 列的返回值以 10 为基数。|  
|LITERAL_PREFIX|**varchar(** 32 **)**|常量前使用的一个或多个字符。 例如，一个单引号 () 字符类型和 0x 为二进制文件。|  
|LITERAL_SUFFIX|**varchar(** 32 **)**|字符或字符用于终止常量。 例如，一个单引号 () 字符类型和二进制没有引号。|  
|CREATE_PARAMS|**varchar(** 32 **)**|此数据类型的创建参数的说明。 例如，**十进制**是"精度和小数位数"， **float**为 NULL，和**varchar**是"max_length"。|  
|NULLABLE|**int**|指定为 Null 性。<br /><br /> 1 = 允许 Null 值。<br /><br /> 0 = 不允许 Null 值。|  
|CASE_SENSITIVE|**int**|指定是否区分大小写。<br /><br /> 1 = 此类型的所有列都区分大小写（用于排序规则）。<br /><br /> 0 = 此类型的所有列都不区分大小写。|  
|SEARCHABLE|**int**|指定列类型的搜索能力：<br /><br /> 1 = 不能搜索。<br /><br /> 2 = 可以使用 LIKE 进行搜索。<br /><br /> 3 = 可以使用 WHERE 进行搜索。<br /><br /> 4 = 可以使用 WHERE 或 LIKE 进行搜索。|  
|UNSIGNED_ATTRIBUTE|**int**|指定数据类型的符号。<br /><br /> 1 = 数据类型没有符号。<br /><br /> 0 = 数据类型有符号。|  
|MONEY|**int**|指定**money**数据类型。<br /><br /> 1 = **money**数据类型。<br /><br /> 0 = 不**money**数据类型。|  
|AUTO_INCREMENT|**int**|指定自动递增。<br /><br /> 1 = 自动递增。<br /><br /> 0 = 不自动递增。<br /><br /> NULL = 属性不适用。<br /><br /> 应用程序可以将值插入具有此属性的列中，但应用程序不能更新列中的值。 除**位**数据类型，AUTO_INCREMENT 是仅为属于精确数字和近似数值数据类型类别的数据类型有效。|  
|LOCAL_TYPE_NAME|**sysname**|与数据源相关的数据类型名称的本地化版本。 例如，DECIMAL 的法语版本是 DECIMALE。 如果是数据源不支持的本地化名称，则返回 NULL。|  
|MINIMUM_SCALE|**int**|数据源中数据类型的最小小数位数。 如果数据类型的小数位数是固定的，则 MINIMUM_SCALE 和 MAXIMUM_SCALE 列将同时包含此值。 当小数位数不适用时，将返回 NULL。|  
|MAXIMUM_SCALE|**int**|数据源中数据类型的最大小数位数。 如果在数据源中没有单独定义最大小数位数，而是将其定义为与最大精度相同，则此列的值与 PRECISION 列的值相同。|  
|SQL_DATA_TYPE|**int**|SQL 数据类型在描述符的 TYPE 字段中显示的值。 此列等同于 DATA_TYPE 列中，除**datetime**和 ANSI**间隔**数据类型。 此字段始终返回值。|  
|SQL_DATETIME_SUB|**int**|**datetime**或 ANSI**间隔**SQL_DATA_TYPE 的值是否 SQL_DATETIME 或 SQL_INTERVAL 子代码。 数据类型以外**datetime**和 ANSI**间隔**，此字段为 NULL。|  
|NUM_PREC_RADIX|**int**|位数或计算列所能容纳的最大数量的数字的数。 如果数据类型是近似数字数据类型，则此列包含的值为 2，以指示几个位。 对于精确数字类型，此列包含的值为 10，以指示几个十进制数字。 否则，此列为 NULL。 通过将精度和基数相结合，应用程序可以计算出列所能容纳的最大数。|  
|INTERVAL_PRECISION|**int**|如果前导精度的间隔的值*data_type*是**间隔**; 否则为空。|  
|USERTYPE|**int**|**usertype** systypes 表中的值。|  
  
## <a name="remarks"></a>Remarks  
 sp_datatype_info 相当于 SQLGetTypeInfo ODBC 中。 返回的结果按 DATA_TYPE 排序，再按数据类型映射到相应 ODBC SQL 数据类型的紧密程度进行排序。  
  
## <a name="permissions"></a>权限  
 要求具有 public 角色的成员身份。  
  
## <a name="examples"></a>示例  
 下面的示例检索信息**sysname**和**nvarchar**通过指定的数据类型*data_type*值`-9`。  
  
```  
USE master;  
GO  
EXEC sp_datatype_info -9;  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [数据库引擎存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
