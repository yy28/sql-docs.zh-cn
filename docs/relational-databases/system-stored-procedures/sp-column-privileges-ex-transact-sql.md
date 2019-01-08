---
title: sp_column_privileges_ex (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_column_privileges_ex
- sp_column_privileges_ex_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_column_privileges_ex
ms.assetid: 98cb6e58-4007-40fc-b048-449fb2e7e6be
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b79fbbd504f7294835e92401a2210e6acac3c440
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52514025"
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
 [  **@table_server =** ] **'**_table_server_  
 要返回信息的链接服务器的名称。 *table_server*是**sysname**，无默认值。  
  
 [  **@table_name =** ] **'**_table_name_  
 包含指定列的表的名称。 *table_name*是**sysname**，默认值为 NULL。  
  
 [  **@table_schema =** ] **'**_table_schema_  
 表架构。 *table_schema*是**sysname**，默认值为 NULL。  
  
 [  **@table_catalog =** ] **'**_table_catalog_  
 是在其中的数据库名称指定*table_name*驻留。 *table_catalog*是**sysname**，默认值为 NULL。  
  
 [  **@column_name =** ] **'**_column_name_  
 为其提供特权信息的列的名称。 *column_name*是**sysname**，默认值为 NULL （均相同）。  
  
## <a name="result-sets"></a>结果集  
 下表显示结果集列。 返回的结果按排序**TABLE_QUALIFIER**， **TABLE_OWNER**， **TABLE_NAME**， **COLUMN_NAME**，和**特权**。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**TABLE_CAT**|**sysname**|表限定符名称。 多种 DBMS 产品支持表的三部分命名 (_限定符_**。**_所有者_**。**_名称_)。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，此列表示数据库名称。 在某些产品中，该列表示表所在的数据库环境的服务器名。 此字段可以为 NULL。|  
|**按 TABLE_SCHEM**|**sysname**|表所有者名称。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，此列表示创建该表的数据库用户的名称。 此字段始终返回值。|  
|**TABLE_NAME**|**sysname**|表名。 此字段始终返回值。|  
|**COLUMN_NAME**|**sysname**|每个列的列名**TABLE_NAME**返回。 此字段始终返回值。|  
|**授权者**|**sysname**|已授予此权限的数据库用户名称**COLUMN_NAME**向列出**被授权者**。 在中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，此列始终是相同**TABLE_OWNER**。 此字段始终返回值。<br /><br /> **GRANTOR**列可以是数据库所有者 (**TABLE_OWNER**) 或人对其数据库所有者授予权限的 GRANT 语句中使用 WITH GRANT OPTION 子句。|  
|**被授权者**|**sysname**|已被授予此权限的数据库用户名称**COLUMN_NAME**按列出**GRANTOR**。 此字段始终返回值。|  
|**特权**|**varchar(** 32 **)**|可用列权限中的一个。 列权限可以是下列值中的一个（或定义实现时数据源支持的其他值）：<br /><br /> 选择 =**被授权者**可以检索列的数据。<br /><br /> INSERT =**被授权者**可以插入新行时为此列提供数据 (由**被授权者**) 到表。<br /><br /> UPDATE =**被授权者**可以修改列中的现有数据。<br /><br /> 引用 =**被授权者**可以引用外部表中主键/外键关系中的列。 主键/外键关系是使用表约束定义的。|  
|**IS_GRANTABLE**|**varchar (** 3 **)**|指示是否**被授权者**允许向其他用户 （通常称为"授予再授予"权限） 授予权限。 可以是 YES、NO 或 NULL。 未知值或 NULL 值表示不能使用“授予再授予”(grant with grant) 的数据源。|  
  
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
  
## <a name="see-also"></a>请参阅  
 [sp_table_privileges_ex &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-table-privileges-ex-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
