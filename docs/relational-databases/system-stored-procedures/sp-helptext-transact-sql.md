---
title: "sp_helptext (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_helptext
- sp_helptext_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helptext
ms.assetid: 24135456-05f0-427c-884b-93cf38dd47a8
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 126654c4c651b57d7739baf6c3b25667c3bd6225
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2017
---
# <a name="sphelptext-transact-sql"></a>sp_helptext (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  显示用户定义规则的定义、默认值、未加密的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存储过程、用户定义 [!INCLUDE[tsql](../../includes/tsql-md.md)] 函数、触发器、计算列、CHECK 约束、视图或系统对象（如系统存储过程）。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_helptext [ @objname = ] 'name' [ , [ @columnname = ] computed_column_name ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@objname =** ] *名称*  
 架构范围内的用户定义对象的限定名称和非限定名称。 仅当指定限定对象时才需要引号。 如果提供的是完全限定名称（包括数据库名称），则数据库名称必须是当前数据库的名称。 对象必须在当前数据库中。 *名称*是**nvarchar(776)**，无默认值。  
  
 [  **@columnname =** ] *computed_column_name*  
 要显示其定义信息的计算列的名称。 包含列的表必须指定为*名称*。 *column_name*是**sysname**，无默认值。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**Text**|**nvarchar(255)**|对象定义|  
  
## <a name="remarks"></a>注释  
 sp_helptext 显示用于在多行中创建对象的定义。 每行包含 255 个字符的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 定义。 定义驻留在**定义**中的列[sys.sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)目录视图。  
  
## <a name="permissions"></a>Permissions  
 要求 **公共** 角色具有成员身份。 系统对象定义对所有用户可见。 用户对象的定义对于对象所有者或具有下列任一权限的被授权者可见：ALTER、CONTROL、TAKE OWNERSHIP 或 VIEW DEFINITION。  
  
## <a name="examples"></a>示例  
  
### <a name="a-displaying-the-definition-of-a-trigger"></a>A. 显示触发器的定义  
 以下示例将显示 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库中的 `dEmployee` 触发器的定义。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_helptext 'HumanResources.dEmployee';  
GO  
```  
  
### <a name="b-displaying-the-definition-of-a-computed-column"></a>B. 显示计算列的定义  
 以下示例将显示 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库的 `TotalDue` 表中计算列 `SalesOrderHeader` 的定义。  
  
```  
USE AdventureWorks2012;  
GO  
sp_helptext @objname = N'AdventureWorks2012.Sales.SalesOrderHeader', @columnname = TotalDue ;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `Text`  
  
 `---------------------------------------------------------------------`  
  
 `(isnull(([SubTotal]+[TaxAmt])+[Freight],(0)))`  
  
## <a name="see-also"></a>另请参阅  
 [数据库引擎存储过程 &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [OBJECT_DEFINITION (Transact-SQL)](../../t-sql/functions/object-definition-transact-sql.md)   
 [sp_help (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sys.sql_modules (Transact-SQL)](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
