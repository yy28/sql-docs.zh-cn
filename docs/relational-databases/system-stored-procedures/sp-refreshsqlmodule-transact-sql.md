---
title: sp_refreshsqlmodule (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 07/25/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_refreshsqlmodule_TSQL
- sp_refreshsqlmodule
dev_langs:
- TSQL
helpviewer_keywords:
- metadata [SQL Server], stored procedures
- metadata [SQL Server], triggers
- metadata [SQL Server], views
- triggers [SQL Server], refreshing metadata
- views [SQL Server], refreshing metadata
- sp_refreshsqlmodule
- metadata [SQL Server], functions
- stored procedures [SQL Server], refreshing metadata
- user-defined functions [SQL Server], refreshing metadata
ms.assetid: f0022a05-50dd-4620-961d-361b1681d375
caps.latest.revision: 21
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b64e93e6ad5bbcadde77e356cbae72c7f545291e
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43064562"
---
# <a name="sprefreshsqlmodule-transact-sql"></a>sp_refreshsqlmodule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

  更新当前数据库中指定的非绑定到架构的存储过程、用户定义函数、视图、DML 触发器、数据库级 DDL 触发器或服务器级 DDL 触发器的元数据。 如果更改这些对象的基础对象，则这些对象的持久元数据（如参数的数据类型）将会过时。
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sys.sp_refreshsqlmodule [ @name = ] 'module_name'   
    [ , [ @namespace = ] ' <class> ' ]  
  
<class> ::=  
{  
  | DATABASE_DDL_TRIGGER  
  | SERVER_DDL_TRIGGER  
}  
  
```  
  
## <a name="arguments"></a>参数  
 [  **@name=** ] **'***module_name*****  
 是存储过程、用户定义函数、视图、DML 触发器、数据库级 DDL 触发器或服务器级 DDL 触发器的名称。 *module_name*不能为公共语言运行时 (CLR) 存储过程或 CLR 函数。 *module_name*不能为绑定到架构的。 *module_name*是**nvarchar**，无默认值。 *module_name*可以是多个部分组成的标识符，但只能引用当前数据库中的对象。  
  
 [ **，** @**命名空间**=] **'** \<类 >   
 是指定模块的类。 当*module_name*是 DDL 触发器，\<类 > 是必需的。 *\<类 >* 是**nvarchar**(20)。 有效输入为：  
  
|||  
|-|-|  
|DATABASE_DDL_TRIGGER||  
|SERVER_DDL_TRIGGER|**适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或非零数字（失败）  
  
## <a name="remarks"></a>Remarks  
 **sp_refreshsqlmodule**模块会影响其定义的对象发生更改时，应运行。 否则，查询或调用该模块时，可能会产生意外结果。 若要刷新视图，可以使用任一**sp_refreshsqlmodule**或**sp_refreshview**使用相同的结果。  
  
 **sp_refreshsqlmodule**不会影响任何权限、 扩展的属性或与对象相关联的 SET 选项。  
  
 若要刷新服务器级 DDL 触发器，可以在任何数据库的上下文中执行此存储过程。  
  
> [!NOTE]  
>  在运行时，将删除所有与对象相关联的签名**sp_refreshsqlmodule**。  
  
## <a name="permissions"></a>Permissions  
 需要对相应模块拥有 ALTER 权限，对该对象引用的任何 CLR 用户定义类型和 XML 架构集合拥有 REFERENCES 权限。 当指定的模块是数据库级 DDL 触发器时，需要在当前数据库中拥有 ALTER ANY DATABASE DDL TRIGGER 权限。 当指定的模块是服务器级 DDL 触发器时，需要拥有 CONTROL SERVER 权限。  
  
 此外，对于使用 EXECUTE AS 子句定义的模块，要求对指定主体拥有 IMPERSONATE 权限。 通常，刷新对象不会更改其 EXECUTE AS 主体，除非模块是使用 EXECUTE AS USER 定义的，并且主体的用户名现在解析为与创建模块时的用户不同的用户。  
  
## <a name="examples"></a>示例  
  
### <a name="a-refreshing-a-user-defined-function"></a>A. 刷新用户定义函数  
 以下示例刷新用户定义函数。 此示例创建别名数据类型 `mytype` 和使用 `to_upper` 的用户定义函数 `mytype`。 然后，`mytype` 将重命名为 `myoldtype`，并将创建具有不同定义的 `mytype`。 刷新了 `dbo.to_upper` 函数，以使它引用 `mytype` 的新实现，而非其旧实现。  
  
```  
-- Create an alias type.  
USE AdventureWorks2012;  
GO  
IF EXISTS (SELECT 'mytype' FROM sys.types WHERE name = 'mytype')  
DROP TYPE mytype;  
GO  
  
CREATE TYPE mytype FROM nvarchar(5);  
GO  
  
IF OBJECT_ID ('dbo.to_upper', 'FN') IS NOT NULL  
DROP FUNCTION dbo.to_upper;  
GO  
  
CREATE FUNCTION dbo.to_upper (@a mytype)  
RETURNS mytype  
WITH ENCRYPTION  
AS  
BEGIN  
RETURN upper(@a)  
END;  
GO  
  
SELECT dbo.to_upper('abcde');  
GO  
  
-- Increase the length of the alias type.  
sp_rename 'mytype', 'myoldtype', 'userdatatype';  
GO  
  
CREATE TYPE mytype FROM nvarchar(10);  
GO  
  
-- The function parameter still uses the old type.  
SELECT name, type_name(user_type_id)   
FROM sys.parameters   
WHERE object_id = OBJECT_ID('dbo.to_upper');  
GO  
  
SELECT dbo.to_upper('abcdefgh'); -- Fails because of truncation  
GO  
  
-- Refresh the function to bind to the renamed type.  
EXEC sys.sp_refreshsqlmodule 'dbo.to_upper';  
  
-- The function parameters are now bound to the correct type and the statement works correctly.  
SELECT name, type_name(user_type_id) FROM sys.parameters  
WHERE object_id = OBJECT_ID('dbo.to_upper');  
GO  
  
SELECT dbo.to_upper('abcdefgh');  
GO  
```  
  
### <a name="b-refreshing-a-database-level-ddl-trigger"></a>B. 刷新数据库级 DDL 触发器  
 下例刷新一个数据库级 DDL 触发器。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sys.sp_refreshsqlmodule @name = 'ddlDatabaseTriggerLog' , @namespace = 'DATABASE_DDL_TRIGGER';  
GO  
```  
  
### <a name="c-refreshing-a-server-level-ddl-trigger"></a>C. 刷新服务器级 DDL 触发器  
 下例刷新一个服务器级 DDL 触发器。  
  
||  
|-|  
|**适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
  
```  
USE master;  
GO  
EXEC sys.sp_refreshsqlmodule @name = 'ddl_trig_database' , @namespace = 'SERVER_DDL_TRIGGER';  
GO  
  
```  
  
## <a name="see-also"></a>请参阅  
 [sp_refreshview (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-refreshview-transact-sql.md)   
 [数据库引擎存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)  
  
  
