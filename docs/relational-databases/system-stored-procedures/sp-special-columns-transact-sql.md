---
title: "sp_special_columns (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_special_columns_TSQL
- sp_special_columns
dev_langs: TSQL
helpviewer_keywords: sp_special_columns
ms.assetid: 0b0993f8-73e0-402b-8c6c-1b0963956f5d
caps.latest.revision: "38"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6fee0eefa43553f1e942abc2c7797d2dd487891d
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="spspecialcolumns-transact-sql"></a>sp_special_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回一组唯一标识表中某个行的最优列。 如果事务更新了行中的某个值，则还将返回自动更新的列。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
sp_special_columns [ @table_name = ] 'table_name'     
     [ , [ @table_owner = ] 'table_owner' ]   
     [ , [ @qualifier = ] 'qualifier' ]   
     [ , [ @col_type = ] 'col_type' ]   
     [ , [ @scope = ] 'scope' ]  
     [ , [ @nullable = ] 'nullable' ]   
     [ , [ @ODBCVer = ] 'ODBCVer' ]   
[ ; ]  
```  
  
## <a name="arguments"></a>参数  
 [ @table_name=] '*table_name*  
 用于返回目录信息的表的名称。 *名称*是**sysname**，无默认值。 不支持通配符模式匹配。  
  
 [ @table_owner=] '*table_owner*  
 是用于返回目录信息的表所有者。 *所有者*是**sysname**，默认值为 NULL。 不支持通配符模式匹配。 如果*所有者*未指定，则应用基础 DBMS 的默认表的可见性规则。  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，如果当前用户拥有一个具有指定名称的表，则返回该表的列。 如果*所有者*未指定当前用户不拥有指定的表和*名称*，此过程看起来指定为表*名称*拥有的数据库所有者。 如果存在该表，则返回该表的列。  
  
 [ @qualifier=] '*限定符*  
 表限定符的名称。 *限定符*是**sysname**，默认值为 NULL。 各种 DBMS 产品支持三部分命名表 (*qualifier.owner.name*)。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，此列表示的数据库名称。 在某些产品中，它表示表所在数据库环境的服务器名称。  
  
 [ @col_type=] '*col_type*  
 是列类型。 *col_type*是**char (**1**)**，默认值为。 类型 R 最佳列集，通过返回的列或列中检索值，允许中指定的任意行无法唯一标识表。 列可以是为此目的专门设计的伪列，也可以是表的某个唯一索引的一个或多个列。 如果列类型为 V，则返回指定表中的列（如果有）。如果有事务更新了行中的某个值，则数据源将自动更新返回的列。  
  
 [ @scope=] '*作用域*  
 ROWID 要求的最小作用域。 *作用域*是**char (**1**)**，默认值为 t。 作用域 C 指定 ROWID 是仅在该行上定位时才有效。 如果作用域为 T，则指定 ROWID 对该事务有效。  
  
 [ @nullable=] '*可以为 null*  
 指示特殊列能否接受 Null 值。 *可以为 null*是**char (**1**)**，默认值为 u。 O 指定不允许空值的特殊列。 如果值为 U，则指定列可以部分为 Null 值。  
  
 [ @ODBCVer=] '*ODBCVer*  
 所使用的 ODBC 版本。 *ODBCVer*是**int (**4**)**，默认值为 2。 这指示 ODBC 版本 2.0。 有关 ODBC 版本 2.0 和 ODBC 版本 3.0 之间的差异的详细信息，请参阅 ODBC 版本 3.0 的 ODBC SQLSpecialColumns 规范。  
  
## <a name="return-code-values"></a>返回代码值  
 无  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|SCOPE|**int**|行 ID 的实际作用域。 可以为 0、1 或 2。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]始终返回 0。 此字段始终返回值。<br /><br /> 0 = SQL_SCOPE_CURROW。 行 ID 只有位于该行上时才能保证有效。 如果另一个事务更新或删除了该行，则以后使用该行 ID 重新选择时，可能无法返回一个行。<br /><br /> 1 = SQL_SCOPE_TRANSACTION。 行 ID 在当前事务期间保证有效。<br /><br /> 2 = SQL_SCOPE_SESSION。 行 ID 在会话（跨事务边界）期间保证有效。|  
|COLUMN_NAME|**sysname**|每一列的列名称*表*返回。 此字段始终返回值。|  
|DATA_TYPE|**int**|ODBC SQL 数据类型。|  
|TYPE_NAME|**sysname**|数据依赖于源的数据类型名称;例如， **char**， **varchar**， **money**，或**文本**。|  
|PRECISION|**Int**|数据源中的列的精度。 此字段始终返回值。|  
|LENGTH|**Int**|长度，以字节为单位，所需的数据源中其二进制形式的数据类型，如 10 **char (**10**)**、 4 的**整数**，和为 2 **smallint**.|  
|SCALE|**int**|数据源中列的小数位数。 对于不适用小数位数的数据类型，返回 NULL。|  
|PSEUDO_COLUMN|**int**|指示列是否为伪列。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 始终返回 1：<br /><br /> 0 = SQL_PC_UNKNOWN<br /><br /> 1 = SQL_PC_NOT_PSEUDO<br /><br /> 2 = SQL_PC_PSEUDO|  
  
## <a name="remarks"></a>注释  
 sp_special_columns 相当于 SQLSpecialColumns ODBC 中。 返回的结果按 SCOPE 排序。  
  
## <a name="permissions"></a>Permissions  
 需要对架构的 SELECT 权限。  
  
## <a name="examples"></a>示例  
 以下示例将返回有关特定列的信息，该列唯一标识了 `HumanResources.Department` 表中的行。  
  
```tsql  
USE AdventureWorks2012;  
GO  
EXEC sp_special_columns @table_name = 'Department'   
    ,@table_owner = 'HumanResources';  
```  
  
## <a name="see-also"></a>另请参阅  
 [目录存储的过程 &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
