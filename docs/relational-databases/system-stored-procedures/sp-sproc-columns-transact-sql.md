---
title: sp_sproc_columns (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_sproc_columns
- sp_sproc_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_sproc_columns
ms.assetid: 62c18c21-35c5-4772-be0d-ffdcc19c97ab
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 6ecbe398a303b7e4cb75fd0eeedc4e7951cfb4fe
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="spsproccolumns-transact-sql"></a>sp_sproc_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  为当前环境中的单个存储过程或用户定义函数返回列信息。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
sp_sproc_columns [[@procedure_name = ] 'name']   
    [ , [@procedure_owner = ] 'owner']   
    [ , [@procedure_qualifier = ] 'qualifier']   
    [ , [@column_name = ] 'column_name']  
    [ , [@ODBCVer = ] 'ODBCVer']  
    [ , [@fUsePattern = ] 'fUsePattern']  
```  
  
## <a name="arguments"></a>参数  
 [ **@procedure_name =** ] **'***name***'**  
 用于返回目录信息的过程名。 *名称*是**nvarchar (** 390 **)**，默认值为 %，这意味着当前数据库中的所有表。 支持通配符模式匹配。  
  
 [  **@procedure_owner =**] *****所有者*****  
 过程所有者的名称。 *所有者*是**nvarchar (** 384 **)**，默认值为 NULL。 支持通配符模式匹配。 如果*所有者*未指定，则应用基础 DBMS 的默认过程可见性的规则。  
  
 如果当前用户拥有具有指定名称的过程，则返回有关该过程的信息。 如果*所有者*未指定当前用户不拥有一个具有指定名称、 过程和**sp_sproc_columns**查找具有指定名称是由数据库所有者拥有的过程。 如果存在该过程，则返回有关该过程的列信息。  
  
 [  **@procedure_qualifier =**] *****限定符*****  
 过程限定符的名称。 *限定符*是**sysname**，默认值为 NULL。 各种 DBMS 产品支持三部分命名表 (*qualifier.owner.name*)。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，此参数表示数据库名称。 在某些产品中，该列表示表所在的数据库环境的服务器名。  
  
 [ **@column_name =**] **'***column_name***'**  
 仅包含一列和所需的目录信息的一列时使用。 *column_name*是**nvarchar (** 384 **)**，默认值为 NULL。 如果*column_name*是省略，则返回所有列。 支持通配符模式匹配。 为了达到最佳的互操作性，网关客户端应只采用 ISO 标准模式匹配（% 和 _ 通配符）。  
  
 [  **@ODBCVer =**] *****ODBCVer*****  
 当前使用的 ODBC 版本。 *ODBCVer*是**int**，默认值为 2，表示 ODBC 版本 2.0。 有关 ODBC 版本 2.0 和 ODBC 版本 3.0 之间的差异的详细信息，请参阅 ODBC **SQLProcedureColumns** ODBC 3.0 版规范  
  
 [  **@fUsePattern =**] *****fUsePattern*****  
 确定下划线 (_)、百分号 (%) 和方括号 ([ ]) 字符是否解释为通配符。 有效值为 0（模式匹配为关闭状态）和 1（模式匹配为打开状态）。 *fUsePattern*是**位**，默认值为 1。  
  
## <a name="return-code-values"></a>返回代码值  
 InclusionThresholdSetting  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**PROCEDURE_QUALIFIER**|**sysname**|过程限定符名称。 该列可以为 NULL。|  
|**PROCEDURE_OWNER**|**sysname**|过程所有者名称。 该列始终返回值。|  
|**过程名称**|**nvarchar (** 134 **)**|过程名。 该列始终返回值。|  
|**COLUMN_NAME**|**sysname**|每一列的列名称**TABLE_NAME**返回。 该列始终返回值。|  
|**COLUMN_TYPE**|**int**|该字段始终返回值：<br /><br /> 0 = SQL_PARAM_TYPE_UNKNOWN<br /><br /> 1 = SQL_PARAM_TYPE_INPUT<br /><br /> 2 = SQL_PARAM_TYPE_OUTPUT<br /><br /> 3 = SQL_RESULT_COL<br /><br /> 4 = SQL_PARAM_OUTPUT<br /><br /> 5 = SQL_RETURN_VALUE|  
|**DATA_TYPE**|**int**|ODBC 数据类型的整数代码。 如果此数据类型无法映射到 ISO 类型，则值为 NULL。 在中返回的本机数据类型名称**TYPE_NAME**列。|  
|**TYPE_NAME**|**sysname**|数据类型的字符串表示形式。 这是由基础 DBMS 表示的数据类型名称。|  
|**PRECISION**|**int**|有效数字位数。 返回值**精度**列是以 10 为基数。|  
|**LENGTH**|**int**|数据的传输大小。|  
|**SCALE**|**int**|小数点右边的数字位数。|  
|**RADIX**|**int**|数值类型的基数。|  
|**可以为 NULL**|**int**|指定为空性：<br /><br /> 1 = 可创建允许空值的数据类型。<br /><br /> 0 = 不允许空值。|  
|**备注**|**varchar (** 254 **)**|对过程列的说明。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不为此列返回值。|  
|**COLUMN_DEF**|**nvarchar (** 4000 **)**|列的默认值。|  
|**SQL_DATA_TYPE**|**int**|它将出现在 SQL 数据类型的值**类型**字段的描述符。 此列等同于**DATA_TYPE**列中，除**datetime**和 ISO**间隔**数据类型。 该列始终返回值。|  
|**SQL_DATETIME_SUB**|**int**|**Datetime** ISO**间隔**如果子代码的值**SQL_DATA_TYPE**是**SQL_DATETIME**或**SQL_INTERVAL**. 数据类型以外**datetime**和 ISO**间隔**，此字段为 NULL。|  
|**CHAR_OCTET_LENGTH**|**int**|以字节为单位的最大长度**字符**或**二进制**数据类型列。 对于所有其他数据类型，此列返回 NULL。|  
|**ORDINAL_POSITION**|**int**|列在表中的序号位置。 表中的第一列为 1。 该列始终返回值。|  
|**IS_NULLABLE**|**varchar(254)**|表中的列的为 Null 性。 根据 ISO 规则确定为 Null 性。 遵从 ISO 标准的 DBMS 不能返回空字符串。<br /><br /> 如果列可包含 NULL，则显示 YES；如果列不能包含 NULL，则显示 NO。<br /><br /> 如果为 Null 性为未知，该列将返回零长度字符串。<br /><br /> 该列返回的值与 NULLABLE 列返回的值不同。|  
|**SS_DATA_TYPE**|**tinyint**|扩展存储过程使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型。 有关详细信息，请参阅[数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)。|  
  
## <a name="remarks"></a>注释  
 **sp_sproc_columns**等效于**SQLProcedureColumns** ODBC 中。 返回对结果进行排序的**PROCEDURE_QUALIFIER**， **PROCEDURE_OWNER**， **PROCEDURE_NAME**，以及参数在过程中出现的顺序定义。  
  
## <a name="permissions"></a>权限  
 需要对架构的 SELECT 权限。  
  
## <a name="see-also"></a>另请参阅  
 [目录存储的过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
