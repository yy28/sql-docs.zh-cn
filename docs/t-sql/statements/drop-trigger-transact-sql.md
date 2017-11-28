---
title: "DROP TRIGGER (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 05/12/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP TRIGGER
- DROP_TRIGGER_TSQL
dev_langs: TSQL
helpviewer_keywords:
- renaming triggers
- triggers [SQL Server], removing
- DDL triggers, removing
- DROP TRIGGER statement
- deleting triggers
- dropping triggers
- removing triggers
- DML triggers, removing
ms.assetid: 092d0d71-9f1e-4e38-a1c4-2487adfa5b4e
caps.latest.revision: "53"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 98f871f47674aeb4c5c3d2b0f55a3e7f8aebb4d7
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="drop-trigger-transact-sql"></a>DROP TRIGGER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  从当前数据库中删除一个或多个 DML 或 DDL 触发器。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Trigger on an INSERT, UPDATE, or DELETE statement to a table or view (DML Trigger)  
  
DROP TRIGGER [ IF EXISTS ] [schema_name.]trigger_name [ ,...n ] [ ; ]  
  
-- Trigger on a CREATE, ALTER, DROP, GRANT, DENY, REVOKE or UPDATE statement (DDL Trigger)  
  
DROP TRIGGER [ IF EXISTS ] trigger_name [ ,...n ]   
ON { DATABASE | ALL SERVER }   
[ ; ]  
  
-- Trigger on a LOGON event (Logon Trigger)  
  
DROP TRIGGER [ IF EXISTS ] trigger_name [ ,...n ]   
ON ALL SERVER  
```  

  
## <a name="arguments"></a>参数  
 *如果存在*  
 **适用于**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]通过[当前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658)， [!INCLUDE[sssds](../../includes/sssds-md.md)])。  
  
 有条件地删除该触发器，仅当它已存在。  
  
 *schema_name*  
 DML 触发器所属架构的名称。 DML 触发器的作用域是为其创建该触发器的表或视图的架构。 *schema_name*不能指定 DDL 或登录触发器。  
  
 *trigger_name*  
 要删除的触发器的名称。 若要查看当前创建触发器的列表，请使用[sys.server_assembly_modules](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md)或[sys.server_triggers](../../relational-databases/system-catalog-views/sys-server-triggers-transact-sql.md)。  
  
 DATABASE  
 指示 DDL 触发器的作用域应用于当前数据库。 如果在创建或修改触发器时也指定了 DATABASE，则必须指定 DATABASE。  
  
 ALL SERVER  
 **适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指示 DDL 触发器的作用域应用于当前服务器。 如果在创建或修改触发器时也指定了 ALL SERVER，则必须指定 ALL SERVER。 ALL SERVER 也适用于登录触发器。  
  
> [!NOTE]  
>  此选项在包含数据库中不可用。  
  
## <a name="remarks"></a>注释  
 可以通过删除 DML 触发器或删除触发器表来删除 DML 触发器。 删除表时，将同时删除与表关联的所有触发器。  
  
 触发器将被删除，从删除有关触发器的信息**sys.objects**， **sys.triggers**和**sys.sql_modules**目录视图。  
  
 仅当所有触发器均使用相同的 ON 子句创建时，才能使用一个 DROP TRIGGER 语句删除多个 DDL 触发器。  
  
 若要重命名触发器，可使用 DROP TRIGGER 和 CREATE TRIGGER。 若要更改触发器的定义，可使用 ALTER TRIGGER。  
  
 有关确定特定触发器的依赖关系的详细信息，请参阅[sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)， [sys.dm_sql_referenced_entities &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md)，和[sys.dm_sql_referencing_entities &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md).  
  
 有关查看触发器的文本的详细信息，请参阅[sp_helptext &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)和[sys.sql_modules &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md).  
  
 有关查看现有的触发器的列表的详细信息，请参阅[sys.triggers &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md)和[sys.server_triggers &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-server-triggers-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 若要删除 DML 触发器，请要求对表或视图在其定义该触发器的 ALTER 权限。  
  
 若要删除定义了服务器范围 (ON ALL SERVER) 的 DDL 触发器或删除登录触发器，需要对服务器拥有 CONTROL SERVER 权限。 若要删除定义了数据库范围 (ON DATABASE) 的 DDL 触发器，要求在当前数据库中具有 ALTER ANY DATABASE DDL TRIGGER 权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-dropping-a-dml-trigger"></a>A. 删除 DML 触发器  
 以下示例将删除 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库中的 `employee_insupd` 触发器。 (从[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]，可以使用删除触发器 IF EXISTS 语法。)  
  
```  
IF OBJECT_ID ('employee_insupd', 'TR') IS NOT NULL  
   DROP TRIGGER employee_insupd;  
```  
  
### <a name="b-dropping-a-ddl-trigger"></a>B. 删除 DDL 触发器  
 以下示例将删除 DDL 触发器 `safety`。  
  
> [!IMPORTANT]  
>  因为 DDL 触发器不是架构范围，并且，因此不显示在**sys.objects**目录视图，不能使用 OBJECT_ID 函数来查询它们是否存在于数据库。 必须使用相应的目录视图来查询架构范围以外的对象。 对于 DDL 触发器，使用**sys.triggers**。  
  
```  
DROP TRIGGER safety  
ON DATABASE;  
```  
  
## <a name="see-also"></a>另请参阅  
 [ALTER TRIGGER (Transact-SQL)](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [CREATE TRIGGER (Transact-SQL)](../../t-sql/statements/create-trigger-transact-sql.md)   
 [ENABLE TRIGGER (Transact-SQL)](../../t-sql/statements/enable-trigger-transact-sql.md)   
 [DISABLE TRIGGER (Transact-SQL)](../../t-sql/statements/disable-trigger-transact-sql.md)   
 [EVENTDATA (Transact-SQL)](../../t-sql/functions/eventdata-transact-sql.md)   
 [获取有关 DML 触发器的信息](../../relational-databases/triggers/get-information-about-dml-triggers.md)   
 [sp_help (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sp_helptrigger (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helptrigger-transact-sql.md)   
 [sys.triggers (Transact-SQL)](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md)   
 [sys.trigger_events (Transact-SQL)](../../relational-databases/system-catalog-views/sys-trigger-events-transact-sql.md)   
 [sys.sql_modules (Transact-SQL)](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.assembly_modules (Transact-SQL)](../../relational-databases/system-catalog-views/sys-assembly-modules-transact-sql.md)   
 [sys.server_triggers (Transact-SQL)](../../relational-databases/system-catalog-views/sys-server-triggers-transact-sql.md)   
 [sys.server_trigger_events (Transact-SQL)](../../relational-databases/system-catalog-views/sys-server-trigger-events-transact-sql.md)   
 [sys.server_sql_modules (Transact-SQL)](../../relational-databases/system-catalog-views/sys-server-sql-modules-transact-sql.md)   
 [sys.server_assembly_modules (Transact-SQL)](../../relational-databases/system-catalog-views/sys-server-assembly-modules-transact-sql.md)  
  
  
