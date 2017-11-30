---
title: "sp_addtype (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_addtype
- sp_addtype_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_addtype
ms.assetid: ed72cd8e-5ff7-4084-8458-2d8ed279d817
caps.latest.revision: "34"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 61a5e94d0e57bdaaac63181c9257defdfd87d8eb
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2017
---
# <a name="spaddtype-transact-sql"></a>sp_addtype (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  创建别名数据类型。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]使用[CREATE TYPE](../../t-sql/statements/create-type-transact-sql.md)相反。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_addtype [ @typename = ] type,   
    [ @phystype = ] system_data_type   
    [ , [ @nulltype = ] 'null_type' ] ;  
```  
  
## <a name="arguments"></a>参数  
 [  **@typename=** ]*类型*  
 别名数据类型的名称。 别名数据类型名称必须遵循的规则[标识符](../../relational-databases/databases/database-identifiers.md)和在每个数据库中必须唯一。 *类型*是**sysname**，无默认值。  
  
 [  **@phystype=**] *system_data_type*  
 为物理、 或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]提供，该别名数据类型所基于的数据类型。*system_data_type*是**sysname**，无默认值，并且可为这些值之一：  
  
||||  
|-|-|-|  
|**bigint**|**binary(n)**|**bit**|  
|**char(n)**|**datetime**|**decimal**|  
|**float**|**image**|**int**|  
|**money**|**nchar （n)**|**ntext**|  
|**numeric**|**nvarchar （n)**|**real**|  
|**smalldatetime**|**int**|**smallmoney**|  
|**sql_variant**|**text**|**tinyint**|  
|**uniqueidentifier**|**varbinary(n)**|**varchar(n)**|  
  
 如果参数中嵌入有空格或标点符号，则必须用引号将该参数引起来。 有关可用的数据类型的详细信息，请参阅[数据类型 &#40;Transact SQL &#41;](../../t-sql/data-types/data-types-transact-sql.md).  
  
 *n*  
 非负整数，指示所选数据类型的长度。  
  
 *P*  
 非负整数，指示可保留的最大十进制位数，包括小数点前面和后面的数字。 有关详细信息，请参阅[小数和数值 &#40;Transact SQL &#41;](../../t-sql/data-types/decimal-and-numeric-transact-sql.md).  
  
 *s*  
 非负整数，指示小数点后面的小数数字可保留的最大十进制位数，它必须小于或等于精度值。 有关详细信息，请参阅[小数和数值 &#40;Transact SQL &#41;](../../t-sql/data-types/decimal-and-numeric-transact-sql.md).  
  
 [  **@nulltype =** ] *null_type*  
 指示别名数据类型处理空值的方式。 *null_type*是**varchar (**8**)**，默认值为 NULL，并且必须括在单引号 （'NULL'、 'NOT NULL'，或 NONULL）。 如果*null_type*未显式定义**sp_addtype**，设置为当前默认为空。 使用 GETANSINULL 系统函数可确定当前默认的为空性。 可以使用 SET 语句或 ALTER DATABASE 对该为空性进行调整。 应显式定义为空性。 如果 **@phystype** 是**位**，和 **@nulltype** 未指定，则默认值不是 NULL。  
  
> [!NOTE]  
>  *Null_type*参数仅定义此数据类型的默认值为 null。 如果在创建表的过程中使用别名数据类型时显式地定义了为空性，那么该为空性优先于已定义的为空性。 有关详细信息，请参阅[ALTER TABLE &#40;Transact SQL &#41;](../../t-sql/statements/alter-table-transact-sql.md)和[创建 TABLE &#40;Transact SQL &#41;](../../t-sql/statements/create-table-transact-sql.md).  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
 无  
  
## <a name="remarks"></a>注释  
 别名数据类型名称在数据库中必须是唯一的，但是名称不同的别名数据类型可以有相同的定义。  
  
 执行**sp_addtype**创建别名数据类型中显示**sys.types**目录视图针对特定数据库。 如果该别名数据类型必须可用于用户定义的所有新数据库中，将其添加到**模型**。 创建了别名数据类型之后，可以在 CREATE TABLE 或 ALTER TABLE 中使用它，也可以将默认值和规则绑定到别名数据类型。 通过使用创建的所有标量别名数据类型**sp_addtype**中包含**dbo**架构。  
  
 别名数据类型继承数据库的默认排序规则。 中的列的排序规则和别名类型的变量的定义[!INCLUDE[tsql](../../includes/tsql-md.md)]CREATE TABLE、 ALTER TABLE 和 DECLARE @*local_variable*语句。 对数据库默认排序规则的更改仅应用于该类型的新列和新变量；它不会更改现有列和变量的排序规则。  
  
> [!IMPORTANT]  
>  为了向后兼容，**公共**数据库角色中自动授予 REFERENCES 权限通过使用创建的别名数据类型**sp_addtype**。 请注意中使用 CREATE TYPE 语句而不是创建别名数据类型时**sp_addtype**，没有此类自动授予发生。  
  
 别名数据类型不能定义使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**时间戳**，**表**， **xml**， **varchar （max)**， **nvarchar (max)**或**varbinary （max)**数据类型。  
  
## <a name="permissions"></a>Permissions  
 要求的成员身份**db_owner**或**db_ddladmin**固定的数据库角色。  
  
## <a name="examples"></a>示例  
  
### <a name="a-creating-an-alias-data-type-that-does-not-allow-for-null-values"></a>A. 创建不允许空值的别名数据类型  
 下面的示例创建名为别名数据类型`ssn`（身份证号），它基于[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-提供**varchar**数据类型。 `ssn` 数据类型用于那些保存 11 位数字的社会保障号 (999-99-9999) 的列。 该列不能为 NULL。  
  
 请注意，`varchar(11)` 由单引号引了起来，这是因为它包含了标点符号（括号）。  
  
```  
USE master;  
GO  
EXEC sp_addtype ssn, 'varchar(11)', 'NOT NULL';  
GO  
```  
  
### <a name="b-creating-an-alias-data-type-that-allows-for-null-values"></a>B. 创建允许空值的别名数据类型  
 以下示例创建允许空值并且名为 `datetime` 的别名数据类型（基于 `birthday`）。  
  
```  
USE master;  
GO  
EXEC sp_addtype birthday, datetime, 'NULL';  
```  
  
### <a name="c-creating-additional-alias-data-types"></a>C. 创建其他别名数据类型  
 以下示例为国内及国际电话和传真号码另外创建两个别名数据类型，分别为 `telephone` 和 `fax`。  
  
```  
USE master;  
GO  
EXEC sp_addtype telephone, 'varchar(24)', 'NOT NULL';  
GO  
EXEC sp_addtype fax, 'varchar(24)', 'NULL';  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [数据库引擎存储过程 &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [CREATE TYPE (Transact-SQL)](../../t-sql/statements/create-type-transact-sql.md)   
 [CREATE DEFAULT (Transact-SQL)](../../t-sql/statements/create-default-transact-sql.md)   
 [CREATE RULE (Transact-SQL)](../../t-sql/statements/create-rule-transact-sql.md)   
 [sp_bindefault &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-bindefault-transact-sql.md)   
 [sp_bindrule &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-bindrule-transact-sql.md)   
 [sp_droptype &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-droptype-transact-sql.md)   
 [sp_rename (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)   
 [sp_unbindefault &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-unbindefault-transact-sql.md)   
 [sp_unbindrule &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-unbindrule-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
