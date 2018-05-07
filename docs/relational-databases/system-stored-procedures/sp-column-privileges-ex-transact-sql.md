---
title: sp_column_privileges_ex (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_column_privileges_ex
- sp_column_privileges_ex_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_column_privileges_ex
ms.assetid: 98cb6e58-4007-40fc-b048-449fb2e7e6be
caps.latest.revision: 34
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 36e3f3c95614fda36c12309c1252b76cdc2da208
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="spcolumnprivilegesex-transact-sql"></a>sp_column_privileges_ex (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回指定链接服务器上的指定表的列特权。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_column_privileges_ex [ @table_server = ] 'table_server'   
     [ , [ @table_name = ] 'table_name' ]   
     [ , [ @table_schema = ] 'table_schema' ]   
     [ , [ @table_catalog = ] 'table_catalog' ]   
     [ , [ @column_name = ] 'column_name' ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@table_server =** ] *****table_server*****  
 要返回信息的链接服务器的名称。 *table_server*是**sysname**，无默认值。  
  
 [  **@table_name =** ] *****table_name*****  
 包含指定列的表的名称。 *table_name*是**sysname**，默认值为 NULL。  
  
 [  **@table_schema =** ] *****table_schema*****  
 表架构。 *table_schema*是**sysname**，默认值为 NULL。  
  
 [  **@table_catalog =** ] *****table_catalog*****  
 是在其中的数据库的名称指定*table_name*驻留。 *table_catalog*是**sysname**，默认值为 NULL。  
  
 [  **@column_name =** ] *****column_name*****  
 为其提供特权信息的列的名称。 *column_name*是**sysname**，默认值为 NULL （所有常见）。  
  
## <a name="result-sets"></a>结果集  
 下表显示结果集列。 返回对结果进行排序的**TABLE_QUALIFIER**， **TABLE_OWNER**， **TABLE_NAME**， **COLUMN_NAME**，和**特权**。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**TABLE_CAT**|**sysname**|表限定符名称。 各种 DBMS 产品支持三部分命名表 (*限定符***。***所有者***。***名称*)。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，此列表示的数据库名称。 在某些产品中，该列表示表所在的数据库环境的服务器名。 此字段可以为 NULL。|  
|**TABLE_SCHEM**|**sysname**|表所有者名称。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，此列表示创建该表的数据库用户的名称。 此字段始终返回值。|  
|**TABLE_NAME**|**sysname**|表名。 此字段始终返回值。|  
|**COLUMN_NAME**|**sysname**|列名称，为每个列的**TABLE_NAME**返回。 此字段始终返回值。|  
|**授权者**|**sysname**|已授予此权限的数据库用户名称**COLUMN_NAME**到列出**被授权者**。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，此列始终是相同**TABLE_OWNER**。 此字段始终返回值。<br /><br /> **授权者**列可以是数据库所有者 (**TABLE_OWNER**) 或人向其数据库所有者授予权限的 GRANT 语句中使用 WITH GRANT OPTION 子句。|  
|**被授权者**|**sysname**|已被授予此权限的数据库用户名称**COLUMN_NAME**通过列出**授权者**。 此字段始终返回值。|  
|**特权**|**varchar(** 32 **)**|可用列权限中的一个。 列权限可以是下列值中的一个（或定义实现时数据源支持的其他值）：<br /><br /> 选择 =**被授权者**可以检索的列的数据。<br /><br /> 插入 =**被授权者**插入新行时可以提供此列的数据 (通过**被授权者**) 到表。<br /><br /> 更新 =**被授权者**可以修改列中的现有数据。<br /><br /> 引用 =**被授权者**可以引用外部表中主键的键/外键关系中的列。 主键/外键关系是使用表约束定义的。|  
|**IS_GRANTABLE**|**varchar (** 3 **)**|指示是否**被授权者**允许权限授予其他用户 （通常称为"授予再授予"权限）。 可以是 YES、NO 或 NULL。 未知值或 NULL 值表示不能使用“授予再授予”(grant with grant) 的数据源。|  
  
## <a name="permissions"></a>权限  
 需要对架构的 SELECT 权限。  
  
## <a name="examples"></a>示例  
 以下示例返回 `HumanResources.Department` 链接服务器上 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库中 `Seattle1` 表的列特权信息。  
  
```  
EXEC sp_column_privileges_ex @table_server = 'Seattle1',   
   @table_name = 'Department',   
   @table_schema = 'HumanResources',  
   @table_catalog ='AdventureWorks2012';  
```  
  
## <a name="see-also"></a>另请参阅  
 [sp_table_privileges_ex &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-table-privileges-ex-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
