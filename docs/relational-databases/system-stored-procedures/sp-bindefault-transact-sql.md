---
title: "sp_bindefault (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 11/25/2015
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
- sp_bindefault
- sp_bindefault_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_bindefault
ms.assetid: 3da70c10-68d0-4c16-94a5-9e84c4a520f6
caps.latest.revision: "42"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b3e23435d6c0a2db3809722856b9daa6b2d66505
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="spbindefault-transact-sql"></a>sp_bindefault (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  将默认值绑定到列或绑定到别名数据类型。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]我们建议使用的 DEFAULT 关键字创建默认定义[ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)或[CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md)语句相反。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_bindefault [ @defname = ] 'default' ,   
    [ @objname = ] 'object_name'   
    [ , [ @futureonly = ] 'futureonly_flag' ]   
```  
  
## <a name="arguments"></a>参数  
 [  **@defname=** ] *默认*  
 由 CREATE DEFAULT 创建的默认值的名称。 *默认*是**nvarchar(776)**，无默认值。  
  
 [  **@objname=** ] *object_name*  
 将默认值绑定到的表名、列名或别名数据类型。 *object_name*是**nvarchar(776)**无默认值。 *object_name*不能使用定义**varchar （max)**， **nvarchar (max)**， **varbinary （max)**， **xml**，或 CLR用户定义的类型。  
  
 如果*object_name*是一个部分名称，它被解析为别名数据类型。 如果它是两个或三个部分名称，它是第一次解析为的表和列;并且，如果此解决方法失败，则将它解析为别名数据类型。 默认情况下，该别名数据类型的现有列继承*默认*，除非已直接到列绑定默认值。 默认值不能绑定到**文本**， **ntext**，**映像**， **varchar （max)**， **nvarchar (max)**，**varbinary （max)**， **xml**，**时间戳**，或 CLR 用户定义类型的列、 一个包含标识属性列、 计算的列或列，已有默认约束。  
  
> [!NOTE]  
>  *object_name*可以包含括号**[]**作为分隔标识符。 有关详细信息，请参阅 [Database Identifiers](../../relational-databases/databases/database-identifiers.md)。  
  
 [  **@futureonly=** ] *futureonly_flag*  
 仅当将默认值绑定到别名数据类型时才能使用。 *futureonly_flag*是**varchar(15)**默认值为 NULL。 当此参数设置为**futureonly**，该数据类型的现有列不能继承新的默认值。 将默认值绑定到列时，从不使用此参数。 如果*futureonly_flag*为 NULL，新的默认值绑定到当前具有无默认值或使用现有的默认值的别名数据类型别名数据类型的列。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="remarks"></a>注释  
 你可以使用**sp_bindefault**若要将绑定的新默认值为列，可使用默认约束是首选方法，尽管或别名数据类型必须先解除绑定现有的默认值。 原有默认值将被覆盖。 不能将默认值绑定到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系统数据类型或 CLR 用户定义类型。 如果默认值和要绑定到的列不兼容，那么在试图插入默认值时（不是在绑定时），[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 将返回错误消息。  
  
 别名数据类型的现有列继承新的默认值，除非的默认绑定直接到它们或*futureonly_flag*指定为**futureonly**。 别名数据类型的新列始终继承默认值。  
  
 当你将默认值绑定到列时，将相关的信息添加到**sys.columns**目录视图。 当你将默认值绑定到别名数据类型时，将相关的信息添加到**sys.types**目录视图。  
  
## <a name="permissions"></a>Permissions  
 用户必须拥有某个表，或者是的成员**sysadmin**固定服务器角色或**db_owner**和**db_ddladmin**固定数据库角色的成员。  
  
## <a name="examples"></a>示例  
  
### <a name="a-binding-a-default-to-a-column"></a>A. 将默认值绑定到列  
 已经使用 CREATE DEFAULT 在当前数据库中定义了名为 `today` 的默认值，以下示例将此默认值绑定到 `HireDate` 表的 `Employee` 列。 每当将行添加到 `Employee` 表而且没有提供 `HireDate` 列的数据时，列都取得默认值 `today` 的值。  
  
```  
USE master;  
GO  
EXEC sp_bindefault 'today', 'HumanResources.Employee.HireDate';  
```  
  
### <a name="b-binding-a-default-to-an-alias-data-type"></a>B. 将默认值绑定到别名数据类型  
 已经存在名为 `def_ssn` 的默认值和名为 `ssn` 的别名数据类型。 以下示例将默认值 `def_ssn` 绑定到 `ssn`。 创建表时，被赋予别名数据类型 `ssn` 的所有列都将继承此默认值。 类型的现有列**ssn**还继承的默认**def_ssn**，除非**futureonly**为指定*futureonly_flag*值，或，除非列具有直接向其绑定的默认值。 绑定到列的默认值始终优先于绑定到数据类型的默认值。  
  
```  
USE master;  
GO  
EXEC sp_bindefault 'def_ssn', 'ssn';  
```  
  
### <a name="c-using-the-futureonlyflag"></a>C. 使用 futureonly_flag  
 以下示例将默认值 `def_ssn` 绑定到别名数据类型 `ssn`。 因为**futureonly**指定，则类型没有现有列`ssn`会受到影响。  
  
```  
USE master;  
GO  
EXEC sp_bindefault 'def_ssn', 'ssn', 'futureonly';  
```  
  
### <a name="d-using-delimited-identifiers"></a>D. 使用分隔的标识符  
 下面的示例演示使用分隔的标识符`[t.1]`中*object_name*。  
  
```  
USE master;  
GO  
CREATE TABLE [t.1] (c1 int);   
-- Notice the period as part of the table name.  
EXEC sp_bindefault 'default1', '[t.1].c1' ;  
-- The object contains two periods;   
-- the first is part of the table name,   
-- and the second distinguishes the table name from the column name.  
```  
  
## <a name="see-also"></a>另请参阅  
 [数据库引擎存储过程 &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [CREATE DEFAULT (Transact-SQL)](../../t-sql/statements/create-default-transact-sql.md)   
 [删除默认 &#40;Transact SQL &#41;](../../t-sql/statements/drop-default-transact-sql.md)   
 [sp_unbindefault &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-unbindefault-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
